# Modul 1: Pengenalan Soldering Breadboard-style

## Tujuan
1. Memahami teknik dasar soldering pada PCB matrix hole
2. Mampu membuat pinheader grid untuk pendekatan breadboard-style
3. Memahami prinsip safety dalam soldering
4. Mampu menggunakan standarisasi warna kabel untuk debugging mudah

## Konsep Breadboard-style Assembly
**Traditional vs Breadboard-style**:
- **Traditional**: Komponen disolder langsung ke PCB (permanen, sulit debugging)
- **Breadboard-style**: Hanya pinheader yang disolder, komponen dihubungkan dengan jumper (fleksibel, mudah debugging)

**Manfaat Pendekatan Ini**:
1. **Mudah debugging**: Cukup ganti kabel jika ada masalah koneksi
2. **Prototyping cepat**: Komponen bisa dipindah-pindah dengan mudah
3. **Reusable**: PCB bisa digunakan untuk multiple projects
4. **Learning friendly**: Memahami koneksi rangkaian dengan jelas

## Standarisasi Warna Kabel
**Sistem Warna untuk Debugging Mudah**:
- **Merah**: VCC (3.3V Power Supply)
- **Hitam**: GND (Ground)
- **Kuning**: SDA (I2C Data Line)
- **Hijau**: SCL (I2C Clock Line)
- **Biru**: GPIO Output (untuk LED, Buzzer)
- **Orange**: GPIO Input (untuk Button, Sensor)
- **Putih/Kuning**: GPIO lainnya

**Manfaat Standarisasi**:
1. Identifikasi fungsi kabel dengan cepat
2. Memudahkan troubleshooting
3. Konsistensi antar kelompok
4. Professional look

## Alat dan Bahan

### Alat:
1. Solder station dengan pengatur suhu (rekomendasi: 350°C)
2. Mata solder tip conical atau chisel
3. Penjepit (tweezers)
4. Pemotong kawat (wire cutter)
5. Penyedot timah (solder sucker) atau solder wick
6. Multimeter untuk testing

### Bahan:
1. ESP32 development board (ESP32 DevKit)
2. Push button tactile switch
3. Buzzer 3.3V
4. 3x LED (warna bebas) dengan resistor 330Ω masing-masing
5. Sensor AHT21 untuk temperature dan humidity
6. PCB matrix hole (protoboard)
7. Kabel jumper dupont 2.54mm (berwarna sesuai standar)
8. Pinheader male (1x40) - untuk grid dan rails
9. Pinheader female (1x40) - untuk socket ESP32 dan sensor
10. Timah solder (lead-free, diameter 0.8mm)
11. Fluks (flux) jika diperlukan

## Teori

### Soldering
Soldering adalah proses penyambungan komponen elektronik menggunakan logam pengisi (timah) yang meleleh pada suhu tertentu (180-250°C). Soldering berbeda dengan welding karena tidak melelehkan logam dasar.

#### Komponen Soldering:
- **Timah**: Campuran timah (Sn) dan timbal (Pb) atau timah murni untuk lead-free
- **Fluks**: Bahan kimia yang membersihkan permukaan logam dan mencegah oksidasi
- **Mata Solder**: Ujung besi solder yang menghantarkan panas

### Safety ketika Soldering
1. **Kacamata safety**: Lindungi mata dari percikan timah
2. **Ventilasi baik**: Hindari menghirup asap flux
3. **Penanganan solder**: Jangan sentuh mata solder saat panas
4. **Solder holder**: Letakkan solder pada holder saat tidak digunakan
5. **Cuci tangan**: Setelah praktikum, terutama jika menggunakan timah mengandung timbal

## Layout PCB Breadboard-style

### Desain Pinheader Grid:
1. **VCC Rails**: 2 baris pinheader untuk distribusi 3.3V (gunakan kabel merah)
2. **GND Rails**: 2 baris pinheader untuk ground (gunakan kabel hitam)
3. **GPIO Grid**: Multiple pinheader untuk koneksi komponen
4. **ESP32 Socket**: Pinheader female untuk mudah pasang/lepas ESP32
5. **Sensor Header**: Pinheader female khusus untuk sensor AHT21

### Visual Layout:
![Layout PCB Breadboard-style](placeholder-layout-pcb-breadboard.jpg)
*Gambar 1: Layout pinheader grid pada PCB matrix hole*

## Prosedur Praktikum

### Persiapan
1. Siapkan semua alat dan bahan di meja kerja
2. Nyalakan solder station dan set suhu ke 350°C
3. Bersihkan mata solder dengan sponge basah
4. Siapkan kabel jumper dengan warna sesuai standar

### Step 1: Solder VCC & GND Rails
1. Potong pinheader male untuk rails VCC dan GND
2. Pasang di PCB: 2 baris untuk VCC (atas), 2 baris untuk GND (bawah)
3. Solder dengan hati-hati, pastikan joint mengkilap
4. **Tips**: Gunakan kabel merah dan hitam sebagai visual guide

### Step 2: Solder GPIO Grid
1. Buat grid pinheader untuk koneksi komponen
2. Spacing konsisten (2.54mm standard)
3. Solder setiap pinheader dengan waktu 2-3 detik per joint
4. **Quality check**: Tidak ada solder bridge, semua joint mengkilap

### Step 3: Solder ESP32 Socket
1. Gunakan pinheader female untuk socket ESP32
2. Pasang di area tengah PCB, align dengan pinout ESP32
3. Solder dengan presisi (pin female lebih kecil)
4. **Testing**: Coba pasang ESP32, pastikan fitting baik

### Step 4: Solder Sensor Header
1. Pinheader female untuk sensor AHT21
2. 4-pin header: VCC, GND, SDA, SCL
3. Solder dengan orientasi yang benar
4. **Labeling**: Gunakan marker untuk identifikasi pin

### Step 5: Quality Check & Testing
1. **Visual inspection**: Joint mengkilap, tidak buram
2. **Multimeter test**: 
   - Cek continuity setiap sambungan
   - Test short circuit antara VCC dan GND
   - Pastikan tidak ada solder bridge
3. **ESP32 test**: Pasang ESP32, pastikan semua pin terkoneksi
4. **Kabel test**: Test kabel jumper dengan multimeter

## Tips Soldering yang Baik
1. **Waktu**: 2-3 detik per joint (jangan terlalu lama)
2. **Suhu**: 320-350°C untuk timah lead-free
3. **Jumlah Timah**: Cukup untuk menutupi joint, tidak berlebihan
4. **Kualitas Joint**: Mengkilap seperti kaca, tidak buram (cold joint)
5. **Solder Bridge**: Pastikan tidak ada sambungan tidak sengaja antara pin

## Persiapan untuk Modul 2
**Setelah Soldering Selesai**:
1. ESP32 sudah terpasang di socket
2. Siapkan kabel jumper dengan warna sesuai standar:
   - Merah: VCC ke sensor, LED, buzzer
   - Hitam: GND ke semua komponen
   - Kuning: SDA (GPIO 21) ke sensor
   - Hijau: SCL (GPIO 22) ke sensor
   - Biru: GPIO output ke LED dan buzzer
   - Orange: GPIO input dari button
3. Test semua koneksi dengan multimeter

## Kesimpulan
1. Pendekatan breadboard-style memudahkan debugging dan prototyping
2. Standarisasi warna kabel meningkatkan efisiensi troubleshooting
3. Quality soldering adalah keterampilan yang perlu latihan
4. Safety selalu menjadi prioritas utama
5. PCB yang dibuat reusable untuk project lainnya

## Referensi
1. IPC-A-610: Acceptability of Electronic Assemblies
2. NASA Workmanship Standards
3. "The Art of Electronics" - Paul Horowitz
4. Panduan soldering dari produsen solder station
5. ESP32 Official Documentation: docs.espressif.com
