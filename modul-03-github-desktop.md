# Modul 3: Pengenalan GitHub dan GitHub Desktop untuk Windows

## Tujuan
1. Memahami konsep version control system (VCS) dan manfaatnya
2. Mampu menginstall dan menggunakan GitHub Desktop untuk Windows
3. Mampu membuat repository GitHub untuk menyimpan kode Arduino praktikum
4. Mampu membuat README.md yang informatif dan menarik
5. Memahami workflow dasar Git: clone, commit, push

## Konsep Dasar Version Control

### Apa itu Git?
Git adalah distributed version control system yang digunakan untuk melacak perubahan dalam kode sumber selama pengembangan perangkat lunak.

### Apa itu GitHub?
GitHub adalah platform hosting untuk repository Git yang menyediakan fitur kolaborasi, code review, dan project management.

### Mengapa perlu Version Control?
1. **Backup**: Menyimpan history semua perubahan
2. **Kolaborasi**: Multiple developer bisa bekerja pada project yang sama
3. **Experiment**: Bisa membuat branch untuk fitur baru tanpa mengganggu main code
4. **Documentation**: Setiap perubahan memiliki pesan commit yang menjelaskan apa yang diubah

## Instalasi GitHub Desktop untuk Windows

### Step 1: Download GitHub Desktop
1. Buka https://desktop.github.com/
2. Klik "Download for Windows"
3. Jalankan installer yang didownload

### Step 2: Setup Akun GitHub
1. Buka GitHub Desktop setelah instalasi
2. Login dengan akun GitHub Anda
   - Jika belum punya akun, buat di https://github.com/signup
3. Konfigurasi identitas (nama dan email)
   - Nama: Nama lengkap Anda
   - Email: Email yang digunakan untuk akun GitHub

### Step 3: Konfigurasi Awal
1. Pilih default editor (Visual Studio Code direkomendasikan)
2. Pilih shell default (Git Bash atau PowerShell)
3. Selesaikan setup wizard

## Prosedur Praktikum

### Step 1: Membuat Repository Baru di GitHub

#### Via GitHub Website:
1. Login ke https://github.com
2. Klik tombol "+" di pojok kanan atas → "New repository"
3. Isi form:
   - Repository name: `esp32-praktikum-lab-stasrg`
   - Description: `Kode Arduino untuk praktikum ESP32 Lab STAS-RG`
   - Visibility: Public (gratis) atau Private (perlu GitHub Pro)
   - Initialize with README: **CHECK** (penting!)
   - Add .gitignore: Pilih "Arduino"
   - Choose a license: MIT License (rekomendasi)
4. Klik "Create repository"

#### Via GitHub Desktop:
1. Buka GitHub Desktop
2. Klik "File" → "New repository"
3. Isi form:
   - Name: `esp32-praktikum-lab-stasrg`
   - Description: `Kode Arduino untuk praktikum ESP32 Lab STAS-RG`
   - Local path: Pilih folder untuk menyimpan project
   - Initialize with README: **CHECK**
   - Git ignore: Pilih "Arduino"
   - License: Pilih "MIT License"
4. Klik "Create repository"
5. Klik "Publish repository" untuk upload ke GitHub

### Step 2: Clone Repository ke Komputer Lokal

Jika repository sudah dibuat di website GitHub:

1. Buka GitHub Desktop
2. Klik "File" → "Clone repository"
3. Pilih tab "URL"
4. Masukkan URL repository: `https://github.com/username/esp32-praktikum-lab-stasrg.git`
5. Pilih local path
6. Klik "Clone"

### Step 3: Menyusun Struktur Folder

Setelah repository di-clone, buat struktur folder yang rapi:

```
esp32-praktikum-lab-stasrg/
├── README.md
├── .gitignore
├── LICENSE
├── src/
│   ├── led_blinking/
│   │   └── led_blinking.ino
│   ├── button_control/
│   │   └── button_control.ino
│   ├── running_led/
│   │   └── running_led.ino
│   ├── aht21_sensor/
│   │   └── aht21_sensor.ino
│   └── complete_project/
│       └── complete_project.ino
├── docs/
│   ├── pinout.md
│   └── circuit_diagram.md
└── images/
    └── (placeholder untuk screenshot)
```

### Step 4: Upload Kode Arduino Praktikum

1. Buka folder repository di File Explorer
2. Copy semua kode Arduino dari Modul 2 ke folder `src/` sesuai kategori
3. Buka GitHub Desktop
4. Anda akan melihat semua file baru di panel "Changes"
5. Untuk setiap file, tambahkan "Summary" dan "Description":
   - Summary: Deskripsi singkat perubahan
   - Description: Detail perubahan yang dilakukan

Contoh commit message yang baik:
```
Summary: Add LED blinking example code

Description:
- Implement basic LED blinking with 1 second interval
- Include serial monitor output for debugging
- Add comments for pin configuration
```

### Step 5: Membuat README.md yang Baik

README.md adalah halaman utama repository Anda. Berikut template yang baik:

```markdown
# ESP32 Praktikum - Lab STAS-RG

![ESP32](images/esp32-board.jpg)

Repository ini berisi kode Arduino untuk praktikum ESP32 di Lab STAS-RG.

## 📋 Daftar Isi
- [Deskripsi](#deskripsi)
- [Fitur](#fitur)
- [Hardware Requirements](#hardware-requirements)
- [Software Requirements](#software-requirements)
- [Instalasi](#instalasi)
- [Struktur Project](#struktur-project)
- [Cara Menggunakan](#cara-menggunakan)
- [Hasil Praktikum](#hasil-praktikum)
- [Kontribusi](#kontribusi)
- [Lisensi](#lisensi)

## 🎯 Deskripsi
Project ini merupakan implementasi praktikum ESP32 yang meliputi:
1. LED Blinking dasar
2. Push button control LED
3. Running LED pattern
4. Pembacaan sensor AHT21 (temperature & humidity)

## ✨ Fitur
- ✅ LED control dengan berbagai pattern
- ✅ Input dari push button dengan debouncing
- ✅ Sensor AHT21 via I2C communication
- ✅ Serial monitor output dengan format yang rapi
- ✅ Buzzer feedback untuk user interaction

## 🔧 Hardware Requirements
1. ESP32 Development Board
2. 3x LED dengan resistor 330Ω
3. Push button tactile switch
4. Buzzer 3.3V
5. Sensor AHT21
6. Kabel jumper dan breadboard

## 💻 Software Requirements
1. Arduino IDE 2.0+
2. ESP32 Board Package
3. Adafruit AHT21 Library

## 📁 Instalasi
1. Clone repository ini:
   ```bash
   git clone https://github.com/username/esp32-praktikum-lab-stasrg.git
   ```
2. Buka Arduino IDE
3. Install library Adafruit AHT21 via Library Manager
4. Pilih board: ESP32 Dev Module
5. Upload kode ke ESP32

## 🗂️ Struktur Project
```
esp32-praktikum-lab-stasrg/
├── src/                    # Source code Arduino
├── docs/                   # Dokumentasi
├── images/                 # Gambar dan diagram
├── README.md              # File ini
├── .gitignore            # Git ignore file
└── LICENSE               # MIT License
```

## 🚀 Cara Menggunakan
1. **LED Blinking**: Buka `src/led_blinking/led_blinking.ino`
2. **Button Control**: Buka `src/button_control/button_control.ino`
3. **Running LED**: Buka `src/running_led/running_led.ino`
4. **Sensor AHT21**: Buka `src/aht21_sensor/aht21_sensor.ino`
5. **Complete Project**: Buka `src/complete_project/complete_project.ino`

## 📊 Hasil Praktikum
### Screenshot Serial Monitor
![Serial Output](images/serial-output.png)

### Circuit Diagram
![Circuit](images/circuit-diagram.png)

## 👥 Kontribusi
1. Fork repository ini
2. Buat branch fitur baru (`git checkout -b feature/amazing-feature`)
3. Commit perubahan (`git commit -m 'Add amazing feature'`)
4. Push ke branch (`git push origin feature/amazing-feature`)
5. Buat Pull Request

## 📄 Lisensi
Distributed under MIT License. See `LICENSE` for more information.
```

### Step 6: Commit dan Push Changes

1. Di GitHub Desktop, pastikan semua file yang ingin di-upload ada di panel "Changes"
2. Isi commit message yang deskriptif
3. Klik "Commit to main"
4. Klik "Push origin" untuk mengupload ke GitHub
5. Buka browser dan cek repository Anda di https://github.com/username/esp32-praktikum-lab-stasrg

### Step 7: Best Practices GitHub

#### Commit Message Guidelines
- Gunakan imperative mood: "Add feature" bukan "Added feature"
- Ringkas di summary (max 50 karakter)
- Detail di description jika perlu
- Reference issue/ticket jika ada: "Fix #12: LED not blinking"

#### Branch Strategy
- `main`: Stable production code
- `develop`: Development branch
- `feature/`: Untuk fitur baru
- `bugfix/`: Untuk perbaikan bug

#### .gitignore untuk Arduino
```
# Arduino
*.elf
*.hex
*.eep
*.bin
*.lst
*.lss
*.sym
*.tmp
*.cpp
*.s
*.d
*.o
*.su
*.ino
*.pde
*.a
*.so
*.so.*
*.dylib

# Compiled Object files
*.slo
*.lo
*.o
*.obj

# Precompiled Headers
*.gch
*.pch

# Compiled Dynamic libraries
*.so
*.dylib
*.dll

# Fortran module files
*.mod
*.smod

# Compiled Static libraries
*.lai
*.la
*.a
*.lib

# Executables
*.exe
*.out
*.app
```

## Troubleshooting

### Masalah Umum dan Solusi

1. **"Authentication failed"**
   - Pastikan login di GitHub Desktop benar
   - Coba generate personal access token

2. **"Repository not found"**
   - Periksa URL repository
   - Pastikan repository ada dan Anda memiliki akses

3. **File tidak muncul di GitHub**
   - Pastikan file sudah di-commit dan di-push
   - Cek panel "History" di GitHub Desktop

4. **Conflict saat merge**
   - Gunakan "Resolve conflicts" di GitHub Desktop
   - Pilih perubahan yang ingin dipertahankan

## Kesimpulan
1. GitHub Desktop memudahkan penggunaan Git untuk pemula
2. README.md yang baik meningkatkan usability repository
3. Commit message yang deskriptif membantu tracking perubahan
4. Struktur folder yang rapi memudahkan maintenance
5. Version control adalah skill essential untuk developer

## Referensi
1. GitHub Desktop Documentation: https://docs.github.com/en/desktop
2. Git Handbook: https://guides.github.com/introduction/git-handbook/
3. Markdown Guide: https://www.markdownguide.org/
4. Arduino .gitignore Template: https://github.com/github/gitignore/blob/main/Arduino.gitignore