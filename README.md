# Worm.py — Petunjuk Instalasi dan Menjalankan

Panduan singkat untuk menginstal dan menjalankan skrip Python pada Termux (Android), terminal desktop (Windows), dan Linux.

## Persyaratan Umum

- Python 3.8 atau lebih baru
- pip (biasanya sudah tersedia bersama Python)
- Library Python: `requests`, `colorama`

Disarankan menggunakan virtual environment (virtualenv / venv) untuk isolasi.

---

## Instalasi Dependensi (semua platform)

1. Buat virtual environment (opsional tapi direkomendasikan):

```
python -m venv venv
source venv/bin/activate   # Linux / Termux (bash)
venv\Scripts\activate    # Windows (PowerShell/CMD)
```

2. Instal paket yang diperlukan:

```
pip install --upgrade pip
pip install requests colorama
```

Jika ingin menyimpan daftar dependensi ke file:

```
pip freeze > requirements.txt
```

---

## Termux (Android)

1. Buka Termux dan install Python:

```
pkg update && pkg upgrade
pkg install python
```

2. (Opsional) Buat virtualenv:

```
python -m venv venv
source venv/bin/activate
```

3. Instal dependensi:

```
pip install --upgrade pip
pip install requests colorama
```

4. Pindah ke lokasi skrip (mis. folder tempat `worm.py` berada) lalu jalankan:

```
python worm.py
```

Catatan: Termux PATH biasanya sudah mendukung `python` setelah instalasi paket.

---

## Desktop (Windows)

1. Install Python dari https://python.org dan centang "Add Python to PATH" saat instalasi.

2. Buka PowerShell atau Command Prompt.

3. (Opsional) Buat virtualenv dan aktifkan:

PowerShell:

```
python -m venv venv
venv\Scripts\Activate.ps1
```

Command Prompt:

```
python -m venv venv
venv\Scripts\activate.bat
```

4. Instal dependensi:

```
pip install --upgrade pip
pip install requests colorama
```

5. Jalankan skrip (pastikan berada di folder yang sama dengan worm.py):

```
python worm.py
```

Jika muncul error "requests not found" atau "colorama not found", ulangi langkah instalasi pip di virtualenv atau gunakan `pip show requests` untuk memverifikasi.

---

## Linux (Debian/Ubuntu, Fedora, etc.)

1. Pasang Python jika belum ada:

Debian/Ubuntu:

```
sudo apt update
sudo apt install python3 python3-venv python3-pip
```

Fedora/CentOS:

```
sudo dnf install python3 python3-venv python3-pip
```

2. Buat virtualenv dan aktifkan:

```
python3 -m venv venv
source venv/bin/activate
```

3. Instal dependensi dan jalankan:

```
pip install --upgrade pip

# README — `worm.py`

Panduan ringkas untuk memasang dependensi dan menjalankan skrip `worm.py` pada Termux (Android), Windows (desktop), dan Linux.

**Ringkasan:** skrip menggunakan modul eksternal `requests` dan `colorama`. Semua modul lain (`json`, `os`, `sys`, `time`) adalah modul bawaan Python.

**Versi Python yang disarankan:** Python 3.8+

---

## Dependensi (spesifik)
- `requests` — untuk melakukan HTTP POST ke API eksternal
- `colorama` — untuk pewarnaan teks terminal

Instalasi cepat (dalam virtual environment direkomendasikan):

```

python -m venv venv
source venv/bin/activate # Linux / Termux (bash)
venv\Scripts\activate # Windows (PowerShell/CMD)
pip install --upgrade pip
pip install requests colorama

```

Untuk menyimpan dependensi:

```

pip freeze > requirements.txt

```

---

## Instruksi Termux (Android)

1. Update paket dan pasang Python:

```

pkg update && pkg upgrade
pkg install python

```

2. (Opsional) Aktifkan virtualenv:

```

python -m venv venv
source venv/bin/activate

```

3. Instal dependensi dan jalankan:

```

pip install --upgrade pip
pip install requests colorama
python worm.py

```

Catatan: pada beberapa instalasi Termux, `python` menunjuk ke Python 3, jika tidak gunakan `python3`.

---

## Instruksi Windows (PowerShell / CMD)

1. Unduh dan pasang Python dari https://python.org. Saat pemasangan centang "Add Python to PATH".

2. Buka PowerShell atau Command Prompt, buat dan aktifkan virtualenv:

PowerShell:

```

python -m venv venv
venv\Scripts\Activate.ps1

```

Command Prompt:

```

python -m venv venv
venv\Scripts\activate.bat

```

3. Instal dependensi dan jalankan:

```

pip install --upgrade pip
pip install requests colorama
python worm.py

```

Jika PowerShell menolak menjalankan skrip aktivasi, jalankan sebagai Administrator:

```

Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

```

---

## Instruksi Linux (Debian/Ubuntu, Fedora, dll.)

Debian/Ubuntu:

```

sudo apt update
sudo apt install python3 python3-venv python3-pip

```

Fedora/CentOS:

```

sudo dnf install python3 python3-venv python3-pip

```

Setelah Python terpasang:

```

python3 -m venv venv
source venv/bin/activate
pip install --upgrade pip
pip install requests colorama
python3 worm.py

```

---

## Menjalankan `worm.py`

Pastikan Anda berada di direktori yang berisi file `worm.py` (mis. Desktop jika itu lokasi Anda), lalu jalankan:

```

python worm.py

```

Jika environment Anda menggunakan `python3` sebagai perintah utama, ganti `python` dengan `python3`.

---

## Troubleshooting singkat
- ModuleNotFoundError untuk `requests` atau `colorama`: aktifkan virtualenv lalu jalankan `pip install requests colorama`.
- Jika `pip` mengarah ke Python 2, gunakan `pip3` atau `python3 -m pip`.
- Jika skrip mengeluh soal koneksi/timeout, cek nilai `API_URL` di `worm.py` dan koneksi internet.

---

## Keamanan & catatan penting
- `worm.py` mengirim persona awal (variabel `AI_PERSONA`) ke API dan menampilkan output mentah dari server eksternal. Tinjau isi `AI_PERSONA` di `worm.py` jika Anda perlu mengubah gaya atau menghapus konten ofensif.
- Jangan jalankan skrip ini di lingkungan produksi tanpa meninjau dan memahami panggilan keluar ke `API_URL`.

---

Jika Anda ingin, saya bisa:
- Membuat file `requirements.txt` lengkap dan menambahkannya di Desktop, atau
- Menambahkan contoh service/systemd unit untuk menjalankan `worm.py` di background pada Linux.
```
