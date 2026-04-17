# Modul 2: Pengenalan ESP32 dengan Arduino IDE

## Tujuan
1. Memahami dasar pemrograman ESP32 menggunakan Arduino IDE
2. Mampu membuat program untuk kontrol LED dan buzzer
3. Mampu membaca input dari push button
4. Mampu membaca data dari sensor AHT21 (temperature dan humidity)
5. Mampu menampilkan data ke Serial Monitor dengan format yang baik

## Alat dan Bahan

### Hardware:
1. ESP32 yang sudah dirakit pada modul 1
2. Komputer/laptop dengan USB port
3. Kabel USB Type-C untuk programming

### Software:
1. Arduino IDE (download: https://www.arduino.cc/en/software)
2. Driver USB untuk ESP32
3. Library AHT21 oleh Adafruit
   - Install via Library Manager: Search "Adafruit AHTx"

### Link Referensi:
- ESP32 Pinout: https://docs.espressif.com/projects/esp-idf/en/latest/esp32/hw-reference/esp32/user-guide-devkitc-1.html
- Arduino ESP32 Board Package: https://docs.espressif.com/projects/arduino-esp32/en/latest/installing.html

## Teori

### Arduino IDE
Arduino IDE adalah Integrated Development Environment untuk pemrograman mikrokontroler berbasis Arduino dan kompatibel seperti ESP32. IDE ini menggunakan bahasa C/C++ yang disederhanakan.

### Void Setup dan Loop
```cpp
void setup() {
  // Kode di sini dieksekusi sekali saat board dinyalakan atau reset
}

void loop() {
  // Kode di sini dieksekusi berulang-ulang selamanya
}
```

### LED dan Buzzer sebagai OUTPUT
- LED dan buzzer adalah komponen output
- Menggunakan fungsi `digitalWrite(pin, HIGH/LOW)` untuk mengontrol
- Menggunakan fungsi `pinMode(pin, OUTPUT)` untuk inisialisasi

### Push Button dan Sensor AHT21
- Push button adalah input digital
- Sensor AHT21 adalah sensor I2C untuk temperature dan humidity
- Menggunakan komunikasi I2C (SDA, SCL pins)

### Komunikasi I2C
- I2C (Inter-Integrated Circuit) adalah protokol komunikasi serial
- Menggunakan 2 kabel: SDA (data) dan SCL (clock)
- ESP32 memiliki multiple I2C interfaces

#### Workflow Cara Inisialisasi Pin di Arduino IDE
1. Deklarasi pin constant di awal program
2. Inisialisasi pin di `setup()` dengan `pinMode()`
3. Gunakan pin di `loop()` dengan `digitalRead()`, `digitalWrite()`, atau `analogRead()`

## Prosedur Praktikum

### Step 1: Instalasi Arduino IDE dan Board ESP32
1. Download dan install Arduino IDE
2. Buka Preferences → Additional Boards Manager URLs
3. Tambahkan: `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
4. Buka Tools → Board → Boards Manager, cari "esp32" dan install
5. Pilih board: "ESP32 Dev Module"

### Step 2: LED Blinking
```cpp
const int LED_PIN = 2;  // GPIO2 untuk LED

void setup() {
  pinMode(LED_PIN, OUTPUT);
  Serial.begin(115200);
}

void loop() {
  digitalWrite(LED_PIN, HIGH);
  delay(1000);
  digitalWrite(LED_PIN, LOW);
  delay(1000);
  Serial.println("LED Blinking...");
}
```

### Step 3: Push Button Control LED
```cpp
const int BUTTON_PIN = 4;  // GPIO4 untuk push button
const int LED_PIN = 2;     // GPIO2 untuk LED

void setup() {
  pinMode(LED_PIN, OUTPUT);
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  Serial.begin(115200);
}

void loop() {
  int buttonState = digitalRead(BUTTON_PIN);
  
  if (buttonState == LOW) {  // Button ditekan (active LOW dengan pull-up)
    digitalWrite(LED_PIN, HIGH);
    Serial.println("Button pressed - LED ON");
  } else {
    digitalWrite(LED_PIN, LOW);
  }
  
  delay(50);  // Debouncing
}
```

### Step 4: Running LED Pattern dengan 3 LED
```cpp
const int LED1_PIN = 2;
const int LED2_PIN = 3;
const int LED3_PIN = 4;
const int BUTTON_PIN = 5;

int currentLED = 0;
int leds[] = {LED1_PIN, LED2_PIN, LED3_PIN};
bool running = false;

void setup() {
  for (int i = 0; i < 3; i++) {
    pinMode(leds[i], OUTPUT);
  }
  pinMode(BUTTON_PIN, INPUT_PULLUP);
  Serial.begin(115200);
}

void loop() {
  // Cek button untuk start/stop running pattern
  if (digitalRead(BUTTON_PIN) == LOW) {
    running = !running;
    Serial.println(running ? "Running pattern STARTED" : "Running pattern STOPPED");
    delay(300);  // Debouncing
  }
  
  if (running) {
    // Matikan semua LED
    for (int i = 0; i < 3; i++) {
      digitalWrite(leds[i], LOW);
    }
    
    // Nyalakan LED saat ini
    digitalWrite(leds[currentLED], HIGH);
    
    // Update LED berikutnya
    currentLED = (currentLED + 1) % 3;
    
    delay(500);  // Delay antara LED
  }
}
```

### Step 5: Membaca Sensor AHT21
```cpp
#include <Adafruit_AHTX0.h>

Adafruit_AHTX0 aht;
const int BUZZER_PIN = 6;

void setup() {
  Serial.begin(115200);
  pinMode(BUZZER_PIN, OUTPUT);
  
  if (!aht.begin()) {
    Serial.println("Could not find AHT21 sensor!");
    while (1) {
      digitalWrite(BUZZER_PIN, HIGH);
      delay(100);
      digitalWrite(BUZZER_PIN, LOW);
      delay(100);
    }
  }
  Serial.println("AHT21 sensor found!");
}

void loop() {
  sensors_event_t humidity, temp;
  aht.getEvent(&humidity, &temp);
  
  // Format output ke Serial Monitor
  Serial.println("=================================");
  Serial.print("Temperature: ");
  Serial.print(temp.temperature);
  Serial.println(" °C");
  
  Serial.print("Humidity: ");
  Serial.print(humidity.relative_humidity);
  Serial.println(" %");
  Serial.println("=================================");
  
  // Buzzer beep setiap pembacaan
  digitalWrite(BUZZER_PIN, HIGH);
  delay(50);
  digitalWrite(BUZZER_PIN, LOW);
  
  delay(2000);  // Baca setiap 2 detik
}
```

### Step 6: Program Lengkap dengan Semua Fitur
```cpp
#include <Adafruit_AHTX0.h>

// Pin Definitions
const int LED1_PIN = 2;
const int LED2_PIN = 3;
const int LED3_PIN = 4;
const int BUTTON1_PIN = 5;  // Untuk mode control
const int BUTTON2_PIN = 6;  // Untuk start/stop
const int BUZZER_PIN = 7;

// Global Variables
Adafruit_AHTX0 aht;
int mode = 0;  // 0: LED Blink, 1: Button Control, 2: Running LED, 3: Sensor Read
bool running = false;
int currentLED = 0;
int leds[] = {LED1_PIN, LED2_PIN, LED3_PIN};

void setup() {
  // Initialize pins
  for (int i = 0; i < 3; i++) {
    pinMode(leds[i], OUTPUT);
  }
  pinMode(BUTTON1_PIN, INPUT_PULLUP);
  pinMode(BUTTON2_PIN, INPUT_PULLUP);
  pinMode(BUZZER_PIN, OUTPUT);
  
  // Initialize Serial
  Serial.begin(115200);
  Serial.println("ESP32 Practical Module Started");
  
  // Initialize AHT21 sensor
  if (aht.begin()) {
    Serial.println("AHT21 Sensor: OK");
  } else {
    Serial.println("AHT21 Sensor: FAILED");
  }
  
  // Welcome beep
  for (int i = 0; i < 3; i++) {
    digitalWrite(BUZZER_PIN, HIGH);
    delay(100);
    digitalWrite(BUZZER_PIN, LOW);
    delay(100);
  }
}

void loop() {
  // Check mode button
  if (digitalRead(BUTTON1_PIN) == LOW) {
    mode = (mode + 1) % 4;
    Serial.print("Mode changed to: ");
    Serial.println(mode);
    delay(300);
  }
  
  // Check start/stop button
  if (digitalRead(BUTTON2_PIN) == LOW) {
    running = !running;
    Serial.println(running ? "Started" : "Stopped");
    delay(300);
  }
  
  // Execute based on mode
  switch(mode) {
    case 0: // LED Blink
      if (running) {
        digitalWrite(LED1_PIN, !digitalRead(LED1_PIN));
        delay(500);
      }
      break;
      
    case 1: // Button Control (simplified)
      digitalWrite(LED2_PIN, running ? HIGH : LOW);
      break;
      
    case 2: // Running LED
      if (running) {
        digitalWrite(leds[currentLED], LOW);
        currentLED = (currentLED + 1) % 3;
        digitalWrite(leds[currentLED], HIGH);
        delay(300);
      }
      break;
      
    case 3: // Sensor Read
      if (running) {
        sensors_event_t humidity, temp;
        if (aht.getEvent(&humidity, &temp)) {
          Serial.print("Temp: ");
          Serial.print(temp.temperature);
          Serial.print("°C, Hum: ");
          Serial.print(humidity.relative_humidity);
          Serial.println("%");
        }
        delay(1000);
      }
      break;
  }
  
  delay(50); // Main loop delay
}
```

## Kesimpulan
1. Arduino IDE menyediakan environment yang mudah untuk pemrograman ESP32
2. ESP32 memiliki kemampuan GPIO yang powerful untuk kontrol LED, button, dan sensor
3. Library management di Arduino IDE memudahkan penggunaan sensor seperti AHT21
4. Serial Monitor penting untuk debugging dan menampilkan data sensor
5. Pemahaman dasar void setup() dan loop() adalah kunci pemrograman Arduino

## Referensi
1. Arduino Language Reference: https://www.arduino.cc/reference/en/
2. ESP32 Arduino Core Documentation: https://github.com/espressif/arduino-esp32
3. Adafruit AHT21 Library: https://github.com/adafruit/Adafruit_AHTX0
4. ESP32 Datasheet: https://www.espressif.com/sites/default/files/documentation/esp32_datasheet_en.pdf
