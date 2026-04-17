# Presentasi Modul 2: Pemrograman ESP32 dengan Arduino IDE

## Slide 1: Cover
**Judul**: Modul 2 - Pemrograman ESP32 dengan Arduino IDE  
**Subjudul**: Integrasi Hardware & Software  
**Pemateri**: [Nama Pemateri]  
**Waktu**: 12:30 - 15:00

## Slide 2: Teori Mikrokontroler
**Apa itu Mikrokontroler?**
- Komputer mini dalam chip tunggal
- Memiliki CPU, memory, I/O dalam satu package
- Dirancang untuk embedded applications

**ESP32 vs Arduino**
- **ESP32**: Dual-core Xtensa LX7, WiFi/BT 5.0, lebih powerful
- **Arduino Uno**: Single-core ATmega328, lebih sederhana
- **Kelebihan ESP32**: Processing power, wireless capabilities, lebih banyak GPIO

**Spesifikasi ESP32S3**:
- Dual-core processor @ 240MHz
- 512KB SRAM, 384KB ROM
- WiFi 4 & Bluetooth 5.0
- 45x GPIO pins, ADC, DAC, I2C, SPI, UART

## Slide 3: Teori Pemrograman Embedded
**Embedded Systems**
- Sistem komputer dalam device khusus
- Contoh: Smartwatch, IoT devices, robot controllers
- Karakteristik: Real-time constraints, resource constraints

**Firmware vs Software**
- **Firmware**: Software yang berjalan di hardware embedded
- **Software**: Aplikasi yang berjalan di general-purpose computers

**GPIO (General Purpose Input/Output)**
- **Output**: Mengontrol devices (LED, buzzer, motor)
- **Input**: Membaca sensors (button, temperature, light)
- **Digital**: Nilai 0/1 (LOW/HIGH)
- **Analog**: Nilai kontinu (0-4095 untuk ESP32 ADC)

## Slide 4: Arduino IDE & Setup
**Arduino IDE**
- Integrated Development Environment untuk mikrokontroler
- Bahasa: C/C++ dengan simplifikasi untuk pemula
- Fitur: Code editor, compiler, serial monitor

**Setup ESP32 di Arduino IDE**
1. **Install Arduino IDE** dari arduino.cc
2. **Add ESP32 Board URL**: `https://espressif.github.io/arduino-esp32/package_esp32_index.json`
3. **Install ESP32 Board** via Boards Manager
4. **Select Board**: ESP32 Dev Module
5. **Select Port**: COM port ESP32 Anda

**Install Library AHT21**
- Library Manager → Search "Adafruit AHTx"
- Install "Adafruit AHT21" library
- Include di code: `#include <Adafruit_AHTX0.h>`

## Slide 5: Program 1 - GPIO Output (LED Control)
**Konsep Digital Output**
- `pinMode(pin, OUTPUT)`: Set pin sebagai output
- `digitalWrite(pin, HIGH/LOW)`: Set pin ke 3.3V atau 0V
- `delay(ms)`: Tunggu dalam milliseconds

**LED Blinking Code**:
```cpp
void setup() {
  pinMode(2, OUTPUT);  // LED di GPIO2
}

void loop() {
  digitalWrite(2, HIGH);  // LED ON
  delay(1000);            // Tunggu 1 detik
  digitalWrite(2, LOW);   // LED OFF
  delay(1000);            // Tunggu 1 detik
}
```

**Running LED Pattern**:
- 3 LED dengan pola berjalan
- Gunakan array untuk pin LED: `int ledPins[] = {2, 4, 5};`
- Loop melalui array untuk pattern

## Slide 6: Program 2 - GPIO Input (Button dengan Pull-up)
**Konsep Digital Input**
- `pinMode(pin, INPUT_PULLUP)`: Set pin sebagai input dengan internal pull-up
- `digitalRead(pin)`: Baca nilai pin (HIGH/LOW)

**Pull-up Resistor**
- Tanpa pull-up: Pin "floating" (nilai tidak stabil)
- Dengan pull-up: Pin default HIGH, button tekan membuat LOW

**Button Control Code**:
```cpp
void setup() {
  pinMode(15, INPUT_PULLUP);  // Button di GPIO15
  pinMode(2, OUTPUT);         // LED di GPIO2
}

void loop() {
  if (digitalRead(15) == LOW) {  // Button ditekan
    digitalWrite(2, HIGH);       // LED ON
  } else {
    digitalWrite(2, LOW);        // LED OFF
  }
}
```

**Debouncing**: Tambahkan `delay(50)` setelah membaca button

## Slide 7: Program 3 - I2C Communication (Sensor AHT21)
**Teori I2C (Inter-Integrated Circuit)**
- 2-wire communication protocol: SDA (Data), SCL (Clock)
- Multiple devices pada bus yang sama (dengan address berbeda)
- ESP32 sebagai master, sensor sebagai slave

**Sensor AHT21**
- Temperature & humidity sensor
- I2C address: 0x38
- Accuracy: ±0.3°C, ±2% RH

**AHT21 Reading Code**:
```cpp
#include <Adafruit_AHTX0.h>
Adafruit_AHTX0 aht;

void setup() {
  Serial.begin(115200);
  if (!aht.begin()) {
    Serial.println("Sensor AHT21 not found!");
    while (1);
  }
}

void loop() {
  sensors_event_t humidity, temp;
  aht.getEvent(&humidity, &temp);
  
  Serial.print("Temperature: ");
  Serial.print(temp.temperature);
  Serial.println(" °C");
  
  Serial.print("Humidity: ");
  Serial.print(humidity.relative_humidity);
  Serial.println(" %");
  
  delay(2000);
}
```

## Slide 8: Program 4 - Integrasi Project Lengkap
**System Design**
1. **Input**: Button untuk kontrol mode
2. **Processing**: ESP32 menjalankan program
3. **Output**: LED pattern, buzzer feedback, serial monitor
4. **Sensor**: AHT21 untuk temperature/humidity

**Project Flow**:
- Mode 1: LED blinking normal
- Mode 2: Running LED pattern
- Mode 3: Display sensor data
- Button: Switch antara mode

**Integrasi Semua Komponen**:
- LED: GPIO 2, 4, 5
- Button: GPIO 15 (INPUT_PULLUP)
- Buzzer: GPIO 18
- Sensor AHT21: GPIO 21 (SDA), GPIO 22 (SCL)

## Slide 9: Koneksi dengan Standar Warna Kabel
**Review Standar Warna** (dari Modul 1):
- Merah: VCC (3.3V) → Sensor, LED, Buzzer
- Hitam: GND → Semua komponen
- Kuning: SDA (GPIO 21) → Sensor AHT21
- Hijau: SCL (GPIO 22) → Sensor AHT21
- Biru: GPIO Output → LED, Buzzer
- Orange: GPIO Input → Button

**Debugging Tips**:
1. Cek koneksi dengan multimeter
2. Pastikan warna kabel sesuai fungsi
3. Test komponen satu per satu
4. Gunakan Serial Monitor untuk debugging

## Slide 10: Q&A & Next Steps
**Review Apa yang Sudah Dipelajari**:
1. Dasar pemrograman ESP32 dengan Arduino IDE
2. GPIO control (input & output)
3. I2C communication dengan sensor
4. Integrasi multiple components

**Bonus: GitHub Portfolio** (jika waktu memungkinkan):
- Upload code ke GitHub
- Buat README.md untuk dokumentasi
- Portfolio untuk CV dan kolaborasi

**Resources**:
- ESP32 Documentation: docs.espressif.com
- Arduino Reference: arduino.cc/reference
- Adafruit AHT21 Library: github.com/adafruit/Adafruit_AHTX0

**Q&A Session**:
- Pertanyaan tentang programming?
- Troubleshooting issues?
- Ide untuk project lanjutan?