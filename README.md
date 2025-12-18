# Cara Instalasi dan Menjalankan `worm_fixed_termux.py`

File ini menjelaskan langkah instalasi dan menjalankan skrip Python pada tiga lingkungan: Termux (Android), Terminal desktop (Windows PowerShell), dan Linux. Juga mencantumkan dependensi yang diperlukan.

PENTING — KEAMANAN & ETIKA

- Skrip berisi variabel `AI_PERSONA` yang saat ini mengandung teks berbahaya/menyinggung. Jangan menjalankan skrip tanpa menyunting dan menghapus atau mengganti `AI_PERSONA` menjadi persona yang aman/etis. Contoh persona aman disertakan di bawah.

Persyaratan umum

- Python 3.8 atau lebih baru
- koneksi internet (skrip memanggil API eksternal)
- `pip` untuk menginstall paket Python

Dependensi Python (lihat `requirements.txt`):

- requests
- colorama

File tambahan yang direkomendasikan:

- `dos2unix` (untuk konversi line endings jika file berasal dari Windows)

---

1. Termux (Android)

Langkah singkat:

```bash
pkg update && pkg upgrade -y
pkg install python git -y
pkg install dos2unix -y    # opsional, jika tersedia
pip install --upgrade pip
pip install -r /sdcard/Download/requirements.txt
termux-setup-storage       # sekali untuk mengizinkan akses storage
```

Memindahkan file dari PC ke Termux (opsi ADB atau copy):

Dari PC (jika pakai ADB):

```bash
adb push C:\\path\\to\\worm_fixed_termux.py /sdcard/Download/
```

Di Termux pindah ke home dan perbaiki line endings:

```bash
cp /sdcard/Download/worm_fixed_termux.py $HOME/
cd $HOME
dos2unix worm_fixed_termux.py   # atau: sed -i 's/\r$//' worm_fixed_termux.py
export LANG=en_US.UTF-8
python worm_fixed_termux.py
```

Catatan Termux:

- Pastikan `LANG` diset ke UTF-8 agar ASCII art tampil benar.
- Jika modul `colorama` tidak berfungsi, instal ulang dengan `pip install colorama`.

---

2. Windows (PowerShell)

Langkah singkat (PowerShell):

1. Install Python dari https://python.org (pastikan Add to PATH dicentang).
2. Buka PowerShell dan jalankan:

```powershell
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip
pip install -r C:\\Users\\<username>\\Downloads\\requirements.txt
python C:\\Users\\<username>\\Downloads\\worm_fixed_termux.py
```

Jika karakter ASCII tampak rusak di PowerShell: jalankan `chcp 65001` untuk set encoding UTF-8 (sementara), dan pastikan font terminal menggunakan monospaced font.

---

3. Linux (Debian/Ubuntu contoh)

```bash
sudo apt update && sudo apt upgrade -y
sudo apt install python3 python3-venv python3-pip dos2unix -y
python3 -m venv .venv
source .venv/bin/activate
pip install --upgrade pip
pip install -r ~/Downloads/requirements.txt
dos2unix ~/Downloads/worm_fixed_termux.py
export LANG=en_US.UTF-8
python3 ~/Downloads/worm_fixed_termux.py
```

---

Contoh `requirements.txt` (lokasi: `C:\\Users\\<user>\\Downloads\\requirements.txt` atau `~/Downloads/requirements.txt`):

```
requests
colorama
```

---

Sanitasi `AI_PERSONA` (WAJIB sebelum menjalankan)

- Buka file `worm_fixed_termux.py` di editor teks.
- Temukan variabel `AI_PERSONA = """ ... """` dan ganti isinya dengan persona yang tidak berbahaya, misalnya:

```python
AI_PERSONA = """
You are a helpful and safe assistant. Give concise, accurate, and legal advice. Do not provide instructions for illegal activity or harmful behavior.
"""
```

Jangan hanya menghapus beberapa kata; sebaiknya ganti keseluruhan teks persona dengan versi aman seperti di atas.

---

Tips pemecahan masalah

- Jika mendapat error ModuleNotFoundError: jalankan `pip install <module>` di environment yang aktif.
- Jika ASCII art tidak sejajar: pastikan file menggunakan line endings LF, terminal memakai font monospace, dan encoding UTF-8 (set `LANG` atau gunakan `chcp 65001` di Windows).
- Jika koneksi API gagal: periksa variabel `API_URL`, koneksi internet, atau firewall.

---

Catatan akhir

- Saya sengaja tidak memasukkan kembali atau mendorong penggunaan persona berbahaya yang ada di file aslinya. Anda bertanggung jawab memastikan konten yang dimasukkan aman dan mematuhi hukum serta aturan platform tempat Anda menjalankan aplikasi.

Jika mau, saya bisa buatkan contoh file `worm_safe.py` yang sudah mengganti `AI_PERSONA` menjadi persona aman dan sedikit membersihkan output agar layak dipakai — mau saya buatkan?

# Hand Wave Detector — README

Script ini mendeteksi "lambaian/gerakan tangan" lewat webcam dan akan membuka sebuah URL di browser ketika lambaian terdeteksi.
Script tersedia di `hand_open_google.py` dan menggunakan MediaPipe + OpenCV.

URL default yang dibuka: https://portofolio-delta-hazel.vercel.app/about.html

## Konten folder

- `hand_open_google.py` — script deteksi tangan / lambaian.
- `requirements_hand.txt` — daftar dependensi (mediapipe, opencv-python).

## Persyaratan

- Python 3.8 — 3.11 direkomendasikan.
- Webcam yang berfungsi dan permission akses kamera.
- Koneksi internet untuk menginstal paket dan membuka URL.

> Catatan: MediaPipe memiliki beberapa persyaratan platform; pada Windows terkadang butuh Python versi tertentu (3.8–3.10) jika pemasangan wheel tidak tersedia untuk versi terbaru.

## Instalasi (Linux / macOS / WSL)

Buka terminal dan jalankan (misal di folder `~/Downloads`):

```bash
cd ~/Downloads
python3 -m venv .venv
source .venv/bin/activate
python3 -m pip install --upgrade pip setuptools wheel
python3 -m pip install -r requirements_hand.txt
```

## Instalasi (Windows — PowerShell)

Buka PowerShell dan jalankan:

```powershell
cd $env:USERPROFILE\Downloads
python -m venv .venv
.\.venv\Scripts\Activate.ps1
python -m pip install --upgrade pip setuptools wheel
python -m pip install -r requirements_hand.txt
```

Jika PowerShell menolak menjalankan script, jalankan satu kali (administrator jika perlu):

```powershell
Set-ExecutionPolicy -Scope CurrentUser -ExecutionPolicy RemoteSigned
```

## Menjalankan script

Contoh menjalankan dengan pengaturan default (Linux/macOS/WSL):

```bash
python3 hand_open_google.py
```

Contoh menjalankan di Windows (PowerShell/CMD):

```powershell
python hand_open_google.py
```

Opsi CLI yang tersedia:

- `--camera` : index kamera (default 0)
- `--frames` : jumlah frame berturut-turut di mana tangan terlihat sebelum mulai cek lambaian (default 6)
- `--debounce` : detik sebelum trigger boleh terjadi lagi (default 4.0)
- `--url` : URL yang akan dibuka saat lambaian terdeteksi
- `--buffer` : banyak posisi x terakhir untuk mengukur gerak (default 12)
- `--threshold` : ambang piksel horizontal untuk dianggap lambaian (default 100)

Contoh menjalankan dengan parameter:

```bash
python3 hand_open_google.py --threshold 80 --buffer 12 --frames 6 --url "https://example.com"
```

## Cara menghentikan

- Klik jendela OpenCV (jendela kamera) lalu tekan `q` atau `Esc`.
- Jika jendela tidak merespon, hentikan dengan `Ctrl+C` di terminal.

Jika Anda menjalankan dari IDE, jalankan dari terminal sistem agar input keyboard di jendela OpenCV diterima.

## Troubleshooting

- ModuleNotFoundError: cv2

  - Pastikan paket `opencv-python` terinstal di environment yang sama dengan interpreter yang Anda gunakan.
  - Verifikasi dengan:
    ```bash
    python -c "import cv2; print(cv2.__version__)"
    python -m pip show opencv-python
    ```

- Error saat menginstal `mediapipe` di Windows

  - Perbarui pip/setuptools/wheel, gunakan Python 3.8–3.10 jika pemasangan gagal.
  - Lihat dokumentasi MediaPipe untuk pilihan wheel yang cocok.

- Jendela OpenCV tidak merespon/kunci

  - Pastikan jendela OpenCV aktif (klik), lalu tekan `q`.
  - Pada WSL tanpa GUI, `cv2.imshow()` tidak akan bekerja — gunakan Windows atau Linux asli, atau jalankan di WSLg.

- Kamera tidak terbuka (cap.isOpened() False)
  - Pastikan kamera tidak dipakai aplikasi lain.
  - Coba index kamera lain: `--camera 1`.
  - Di Linux periksa `/dev/video*` dan izin akses.

## Menyesuaikan sensitivitas

- Jika terlalu sering false positive (terbuka walau tidak melambaikan): naikkan `--threshold` (lebih besar berarti perlu rentang gerak lebih luas), atau kurangi `--buffer`/menaikkan `--frames`.
- Jika tidak sensitif: turunkan `--threshold` atau kurangi `--frames` / perbesar `--buffer`.

## Notes untuk WSL

- Untuk menampilkan jendela GUI di WSL, gunakan WSLg atau jalankan script di Windows atau di mesin Linux.

## Menyesuaikan URL yang dibuka

- Ubah argumen `--url` saat menjalankan, atau edit default `url` di header script.

## Request saya bantu lagi?

Saya bisa membuatkan:

- skrip `.bat` (Windows) dan `.sh` (Linux) untuk otomatis membuat virtualenv dan menginstall dependensi,
- script kecil untuk membuka browser tertentu (mis. Chrome) dengan opsi membuka di tab baru, atau
- versi "headless" yang hanya mengekspor event log (tidak membuka GUI).

Jika Anda ingin, saya bisa membuat file `start_windows.bat` dan `start_linux.sh` sekarang.
