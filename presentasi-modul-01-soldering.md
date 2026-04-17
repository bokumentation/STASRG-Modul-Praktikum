# Presentasi Modul 1: Pengenalan Soldering Breadboard-style

## Slide 1: Cover
**Judul**: Modul 1 - Pengenalan Soldering Breadboard-style  
**Subjudul**: Praktikum Hardware Lab STAS-RG  
**Pemateri**: [Nama Pemateri]  
**Waktu**: 9:00 - 11:30

## Slide 2: Apa Itu Soldering?
**Definisi**: Proses penyambungan komponen elektronik menggunakan timah yang meleleh (180-250°C)

**Perbedaan Soldering vs Welding**:
- Soldering: Tidak melelehkan logam dasar, hanya timah pengisi
- Welding: Melelehkan logam dasar untuk penyambungan

**Komponen Soldering**:
- Timah: Campuran Sn/Pb atau timah lead-free
- Fluks: Membersihkan permukaan, mencegah oksidasi
- Mata solder: Menghantarkan panas ke joint

## Slide 3: Safety First!
**Protect Yourself**:
1. **Kacamata safety**: Lindungi mata dari percikan timah
2. **Ventilasi baik**: Hindari menghirup asap flux
3. **Penanganan solder**: Jangan sentuh mata solder panas
4. **Solder holder**: Letakkan solder di holder saat tidak digunakan
5. **Cuci tangan**: Setelah praktikum, terutama jika pakai timah mengandung timbal

**Suhu Optimal**: 350°C untuk timah lead-free

## Slide 4: Konsep Breadboard-style Assembly
**Traditional vs Breadboard-style**:
- **Traditional**: Komponen disolder langsung ke PCB
- **Breadboard-style**: Hanya pinheader yang disolder, komponen dihubungkan dengan jumper

**Manfaat Breadboard-style**:
1. **Mudah debugging**: Cukup ganti kabel jika ada masalah
2. **Prototyping cepat**: Komponen bisa dipindah-pindah
3. **Reusable**: PCB bisa digunakan untuk project lain
4. **Learning friendly**: Memahami koneksi dengan jelas

## Slide 5: Standarisasi Warna Kabel
**Sistem Warna untuk Debugging Mudah**:
- **Merah**: VCC (3.3V Power)
- **Hitam**: GND (Ground)
- **Kuning**: SDA (I2C Data Line)
- **Hijau**: SCL (I2C Clock Line)
- **Biru**: GPIO Output (LED, Buzzer)
- **Orange**: GPIO Input (Button, Sensor)

**Visual**: Diagram warna kabel dengan fungsi masing-masing

## Slide 6: Layout Pinheader Grid
**Desain PCB Breadboard-style**:
1. **VCC Rails**: Baris pinheader untuk distribusi 3.3V (kabel merah)
2. **GND Rails**: Baris pinheader untuk ground (kabel hitam)
3. **GPIO Grid**: Pinheader untuk koneksi komponen
4. **ESP32 Socket**: Pinheader female untuk mudah pasang/lepas ESP32
5. **Sensor Header**: Pinheader female khusus untuk sensor AHT21

**Visual**: Layout PCB dengan penandaan warna

## Slide 7: Langkah Praktikum Soldering
**Step 1: Solder VCC & GND Rails**
- Pasang pinheader untuk power distribution
- Gunakan kabel merah (VCC) dan hitam (GND) sebagai referensi

**Step 2: Solder GPIO Grid**
- Pinheader untuk koneksi komponen (LED, button, buzzer)
- Susun rapi dengan spacing yang konsisten

**Step 3: Solder ESP32 Socket**
- Pinheader female untuk socket ESP32
- Pastikan alignment dengan pinout ESP32

**Step 4: Solder Sensor Header**
- Pinheader female untuk sensor AHT21
- Siapkan untuk koneksi I2C (SDA, SCL)

## Slide 8: Tips & Quality Check
**Tips Soldering yang Baik**:
1. **Waktu**: 2-3 detik per joint (jangan terlalu lama)
2. **Suhu**: 320-350°C untuk timah lead-free
3. **Jumlah Timah**: Cukup menutupi joint, tidak berlebihan
4. **Kualitas Joint**: Mengkilap seperti kaca, tidak buram

**Quality Check**:
1. **Visual inspection**: Joint mengkilap, tidak ada solder bridge
2. **Multimeter test**: Cek continuity, no short circuit
3. **ESP32 test**: Pastikan socket bekerja dengan baik

## Slide 9: Persiapan untuk Modul 2
**Apa Selanjutnya?**:
- Modul 2: Pemrograman ESP32 dengan Arduino IDE (12:30-15:00)
- **Bawa**: Laptop dengan Arduino IDE terinstall
- **Siapkan**: ESP32 yang sudah dirakit, kabel jumper berwarna

**Q&A Session**:
- Pertanyaan tentang soldering technique?
- Clarifikasi standar warna kabel?
- Persiapan hardware untuk programming?