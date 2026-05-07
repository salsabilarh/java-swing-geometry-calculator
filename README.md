# 📐 Program Menghitung Luas & Keliling Bangun Datar

> **Tugas Akhir Praktikum Dasar Komputer dan Pemrograman**
> Aplikasi Desktop berbasis Java Swing yang menghitung luas dan keliling 8 jenis bangun datar secara interaktif.

# 📑 Daftar Isi

- [📌 Project Description](#-project-description)
- [🛠️ Tech Stack](#️-tech-stack)
- [✨ Key Features](#-key-features)
- [📁 Project Structure](#-project-structure)
- [⚙️ Installation & Running](#️-installation--running)
- [📡 API Documentation](#-api-documentation)
- [📚 Learning Outcomes](#-learning-outcomes)
- [👩‍💻 Author](#%E2%80%8D-author)
- [📄 License](#-license)

---

## 📌 Project Description

**Program Menghitung Luas dan Keliling Bangun Datar** adalah aplikasi desktop yang dikembangkan sebagai **Tugas Akhir Praktikum Dasar Komputer dan Pemrograman (DKP)**. Proyek ini merupakan bukti penguasaan dasar-dasar pemrograman berorientasi objek menggunakan Java, sekaligus pengenalan pertama pada pembuatan **Graphical User Interface (GUI)** dengan Java Swing.

Aplikasi ini memungkinkan pengguna memilih jenis bangun datar dari menu utama, memasukkan parameter yang diperlukan, lalu mendapatkan hasil perhitungan luas dan keliling secara instan melalui antarmuka grafis yang intuitif.

---

## 🛠️ Tech Stack

| Komponen | Teknologi | Keterangan |
|---|---|---|
| Language | **Java SE (JDK 1.8 / Java 8)** | Bahasa pemrograman utama |
| GUI Framework | **Java Swing** | Toolkit GUI bawaan Java Standard Library |
| IDE | **NetBeans IDE** | IDE utama (dengan Swing Form Designer) |
| Build Tool | **Apache Ant** (`build.xml`) | Build automation bawaan NetBeans |
| Look & Feel | **Nimbus Look and Feel** | Tema UI modern dari Java SE 6+ |
| Tipe Aplikasi | **Desktop Application (.jar)** | Standalone executable JAR |

---

## ✨ Key Features

### 1. Menu Utama dengan Radio Button Selection
`FormUtama` menyediakan antarmuka pemilihan bangun datar menggunakan **JRadioButton**. Saat satu bangun dipilih, pilihan lain otomatis di-disable untuk mencegah seleksi ganda — mengimplementasikan logika UI state management secara manual.

### 2. Kalkulasi 8 Bangun Datar
Aplikasi mendukung perhitungan lengkap (luas dan keliling) untuk 8 bangun datar:

| No | Bangun Datar | Rumus Luas | Rumus Keliling |
|---|---|---|---|
| 1 | **Persegi** | s × s | 4 × s |
| 2 | **Persegi Panjang** | p × l | 2 × (p + l) |
| 3 | **Segitiga** | a × t / 2 | a + b + c |
| 4 | **Lingkaran** | π × r² | 2 × π × r |
| 5 | **Belah Ketupat** | d1 × d2 / 2 | 4 × s |
| 6 | **Trapesium** | (a + b) × t / 2 | a + b + c + d |
| 7 | **Jajar Genjang** | a × t | 2 × (a + b) |
| 8 | **Layang-layang** | d1 × d2 / 2 | 2 × (a + b) |

### 3. Input Validation dengan JFormattedTextField
Semua field input menggunakan `JFormattedTextField` dengan `NumberFormatter` — hanya menerima input numerik, mencegah crash akibat input karakter non-numerik.

### 4. Tombol Hitung, Reset, dan Navigasi
Setiap form bangun datar memiliki:
- **Hitung** (atau Hitung Luas / Hitung Keliling): Memproses kalkulasi dan menampilkan hasil
- **Reset**: Mengosongkan semua field dan hasil (hanya aktif setelah dihitung)
- **Kembali**: Kembali ke `FormUtama` menggunakan navigasi antar-JFrame dengan `dispose()`
- **Keluar**: Menutup aplikasi dengan `System.exit(0)`

### 5. Event-Driven Programming dengan ActionListener
Seluruh interaksi pengguna dikelola melalui **ActionListener** yang di-attach ke setiap komponen GUI, memperkenalkan konsep event-driven programming — paradigma fundamental dalam pengembangan aplikasi GUI.

### 6. Nimbus Look and Feel
Aplikasi menggunakan **Nimbus Look and Feel** dengan penanganan exception menggunakan try-catch multi-exception: `ClassNotFoundException`, `InstantiationException`, `IllegalAccessException`, dan `UnsupportedLookAndFeelException`.

### 7. Multi-Window Navigation (JFrame ke JFrame)
Navigasi antar form menggunakan pola: buat instance baru → `setVisible(true)` → `this.dispose()`. Ini memperkenalkan konsep manajemen siklus hidup window dalam aplikasi desktop.

### 8. Pemisahan Luas dan Keliling (Beberapa Bangun)
Bangun datar dengan parameter input berbeda antara luas dan keliling (seperti Segitiga, Belah Ketupat, Trapesium, Jajar Genjang, Layang-layang) memiliki **tombol Hitung terpisah** — memisahkan concern kalkulasi secara logis.

---

## 📁 Project Structure

```
java-swing-geometry-calculator/
├── src/
│   └── tugasakhir/                    # Package utama aplikasi
│       ├── FormUtama.java             # Entry point GUI: menu pemilihan bangun datar
│       ├── FormUtama.form             # NetBeans Swing Form Designer file
│       ├── Persegi.java               # Form kalkulasi Persegi
│       ├── PersegiPanjang.java        # Form kalkulasi Persegi Panjang
│       ├── Segitiga.java              # Form kalkulasi Segitiga
│       ├── Lingkaran.java             # Form kalkulasi Lingkaran
│       ├── BelahKetupat.java          # Form kalkulasi Belah Ketupat
│       ├── Trapesium.java             # Form kalkulasi Trapesium
│       ├── JajarGenjang.java          # Form kalkulasi Jajar Genjang
│       └── Layanglayang.java          # Form kalkulasi Layang-layang
│
├── build/
│   └── classes/tugasakhir/            # Compiled .class files (auto-generated)
│
├── nbproject/
│   ├── project.xml                    # Konfigurasi proyek NetBeans
│   └── project.properties            # Properties: Java source/target version, main class
│
├── build.xml                          # Apache Ant build script
├── manifest.mf                        # JAR manifest file
└── README.md
```

### Pola Arsitektur: Single-Package Modular GUI

Setiap bangun datar direpresentasikan oleh **satu class JFrame terpisah**, mencerminkan prinsip **Single Responsibility** di level sederhana — satu class, satu tugas kalkulasi. `FormUtama` berperan sebagai **controller/navigator** yang menginisialisasi dan menampilkan form yang tepat berdasarkan pilihan pengguna.

```
[FormUtama - Menu Utama]
        |
        | (pilih bangun & klik Pilih)
        ↓
[Form Bangun Datar Terpilih]
  ├── Input: JFormattedTextField (numerik)
  ├── Proses: Kalkulasi dengan variabel double
  └── Output: JLabel (tampilkan hasil)
        |
        | (klik Kembali)
        ↓
[FormUtama - Menu Utama]
```

---

## ⚙️ Installation & Running

### Prerequisites
- [Java Development Kit (JDK) 8 atau lebih tinggi](https://www.oracle.com/java/technologies/downloads/)
- [NetBeans IDE 12+](https://netbeans.apache.org/) (opsional, untuk membuka dan mengedit project)

### Cara 1: Jalankan via NetBeans IDE

1. **Clone atau download repository:**
   ```bash
   git clone https://github.com/SalsabilaRafifah/java-swing-geometry-calculator.git
   ```

2. **Buka NetBeans IDE**, pilih `File → Open Project`

3. **Arahkan ke folder** `java-swing-geometry-calculator` dan klik **Open**

4. **Klik kanan pada project** di panel Projects → pilih **Run** (atau tekan `F6`)

### Cara 2: Build & Run via Command Line (Apache Ant)

```bash
# Masuk ke direktori project
cd java-swing-geometry-calculator

# Build project menggunakan Ant
ant clean build

# Jalankan aplikasi
ant run
```

### Cara 3: Jalankan dari file JAR (setelah di-build)

```bash
# Build JAR terlebih dahulu via NetBeans atau Ant
# File JAR akan tersedia di folder dist/

java -jar "dist/TA_DKP_Salsabila_Rafifah_Handifa_21120121130042_Program_Menghitung_Luas_dan_Keliling_Bangun_Datar.jar"
```

### Alur Penggunaan Aplikasi

```
1. Jalankan aplikasi → Form Menu Utama muncul
2. Pilih salah satu bangun datar menggunakan Radio Button
3. Klik tombol "Pilih" (otomatis aktif setelah memilih)
4. Form kalkulasi bangun terpilih terbuka
5. Masukkan nilai parameter yang diperlukan
6. Klik "Hitung" (atau "Hitung Luas" / "Hitung Keliling")
7. Hasil tampil di label output
8. Klik "Reset" untuk kalkulasi ulang atau "Kembali" ke menu
```

---

## 🧮 Rumus & Logika Kalkulasi

### Implementasi dalam Kode Java

```java
// Persegi: Luas = s × s, Keliling = 4 × s
panjangSisi = Double.parseDouble(TFPanjangSisi.getText());
luas = panjangSisi * panjangSisi;
keliling = 4 * panjangSisi;

// Lingkaran: Luas = π × r², Keliling = 2 × π × r
final double PHI = 3.14159;
r = Double.parseDouble(TFr.getText());
luas = PHI * r * r;
keliling = 2 * PHI * r;

// Segitiga: Luas = a × t / 2, Keliling = a + b + c
luas = aLuas * t / 2;
keliling = aKeliling + b + c;

// Trapesium: Luas = (a + b) × t / 2, Keliling = a + b + c + d
luas = (aLuas + bLuas) / 2 * t;
keliling = aKeliling + bKeliling + c + d;
```

**Tipe data yang digunakan:** `double` — untuk mendukung input desimal dan hasil perhitungan yang akurat.

---

## 📚 Learning Outcomes

Proyek ini membekali penguasaan konsep fundamental Java dan pemrograman:

**Dasar Pemrograman Java**
- Deklarasi variabel dengan tipe data `double` untuk presisi kalkulasi matematika
- Penggunaan konstanta (`final double PHI = 3.14159`) untuk nilai tetap
- Parsing string ke double: `Double.parseDouble(textField.getText())`
- Konversi double ke string: `String.valueOf(hasil)`
- Operasi aritmatika dasar: penjumlahan, perkalian, pembagian

**Object-Oriented Programming (OOP)**
- Setiap bangun datar adalah **class tersendiri** yang extends `JFrame`
- Pemahaman **inheritance**: semua form mewarisi properti dan method dari `JFrame`
- **Encapsulation**: variabel kalkulasi dideklarasikan sebagai field class (bukan lokal)
- **Constructor**: `initComponents()` dipanggil di constructor untuk inisialisasi GUI

**Java Swing & GUI Programming**
- Penggunaan komponen utama: `JFrame`, `JPanel`, `JLabel`, `JButton`, `JRadioButton`, `JFormattedTextField`, `JSeparator`
- **Event Handling**: implementasi `ActionListener` dengan anonymous inner class
- **Layout Management**: `GroupLayout` (dikelola otomatis oleh NetBeans Form Designer)
- **Look and Feel**: Nimbus LnF dengan penanganan multi-exception
- **Window Management**: navigasi antar JFrame dengan `setVisible()` dan `dispose()`

**Exception Handling**
- Penggunaan try-catch untuk 4 jenis checked exception pada UIManager
- Memahami mengapa UI initialization perlu error handling yang robust

**Practical Development Skills**
- Menggunakan NetBeans **Swing Form Designer** (drag-and-drop GUI builder)
- Memahami file `.form` sebagai representasi XML dari desain GUI
- Build project dengan **Apache Ant** (`build.xml`)
- Distribusi aplikasi sebagai executable **JAR file**
- Penggunaan `EventQueue.invokeLater()` dan **Runnable** untuk thread-safety pada Swing

---

## 👩‍💻 Author

**Salsabila Rafifah Handifa**
NIM: 21120121130042
Praktikum Dasar Komputer dan Pemrograman

---

## 📄 License

This project is built for academic purposes as a final assignment for the Dasar Komputer dan Pemrograman (DKP) Practicum.
