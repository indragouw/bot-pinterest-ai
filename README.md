# Bot Auto-Pin Pinterest Canggih (Pexels & RSS)

Selamat datang di Bot Auto-Pin Pinterest! Skrip ini adalah solusi otomasi lengkap yang dirancang untuk membantu Anda menumbuhkan akun Pinterest dan meningkatkan *traffic* ke website Anda secara konsisten dan otomatis.

Bot ini berjalan sepenuhnya di cloud menggunakan **GitHub Actions**, sehingga tidak memerlukan server pribadi dan komputer Anda tidak perlu menyala. Cukup atur sekali, dan biarkan bot bekerja untuk Anda 24/7.

## ✨ Fitur Utama

* **🤖 Dua Mode Otomatisasi:** Dapat berjalan dalam mode **Pexels** (konten dari kata kunci) atau mode **RSS** (konten dari blog/website Anda).
* **🧠 Konten Cerdas (Google Gemini AI):** Membuat judul dan deskripsi yang unik dan menarik untuk setiap Pin secara otomatis.
* **🖼️ Sumber Gambar Fleksibel:** Mengambil gambar dari **Pexels** atau langsung dari artikel **RSS feed** Anda. Jika artikel tidak memiliki gambar, bot akan otomatis mencarikan gambar di Pexels.
* **☁️ 100% Berbasis Cloud (GRATIS):** Dijalankan menggunakan GitHub Actions, sehingga Anda tidak perlu membayar biaya server/VPS.
* **🎯 Anti-Duplikat Cerdas:** Memastikan setiap gambar Pexels dan link artikel RSS hanya diposting satu kali.
* **🔐 Login Aman & Andal:** Menggunakan metode *cookies* untuk login yang aman dan menghindari *captcha*.
* **🔧 Konfigurasi Mudah:** Semua pengaturan utama dilakukan melalui file `.json` yang sederhana.

---

## 🔧 File Konfigurasi & Penjelasannya

Anda akan mengedit **salah satu** dari dua file konfigurasi ini, tergantung bot mana yang ingin Anda jalankan.

### 1. `config.json` (Untuk `bot.js` - Mode Pexels Saja)

Gunakan file ini jika Anda hanya ingin menjalankan bot yang memposting konten dari Pexels berdasarkan kata kunci.

```json
{
  "pexels": {
    "keywordFile": "keywords.txt"
  },
  "pinterest": {
    "boardUrl": "[https://www.pinterest.com/username/nama-board-anda/](https://www.pinterest.com/username/nama-board-anda/)"
  },
  "gemini": {
    "prompt": "Buat judul dan deskripsi singkat...",
    "fallbackTitle": "Inspirasi Keren untuk Anda",
    "fallbackDescription": "Temukan lebih banyak ide..."
  },
  "settings": {
    "destinationLink": "[https://website-atau-blog-anda.com](https://website-atau-blog-anda.com)"
  }
}
```
* **`pexels.keywordFile`**: Arahkan ke file `.txt` yang berisi daftar kata kunci Anda. **(Wajib diubah)**
* **`pinterest.boardUrl`**: URL lengkap dari board Pinterest tujuan. **(Wajib diubah)**
* **`settings.destinationLink`**: Link website/blog tujuan Anda untuk setiap Pin. **(Wajib diubah)**

### 2. `config2.json` (Untuk `both.js` - Mode Pexels & RSS)

Gunakan file ini jika Anda ingin menjalankan bot yang bisa mode Pexels, RSS, atau keduanya.

```json
{
  "runMode": "both",
  "pexels": {
    "keywordFile": "keywords.txt"
  },
  "rss": {
    "feedUrl": "[https://website-anda.com/feed.xml](https://website-anda.com/feed.xml)",
    "startFromLink": "[https://website-anda.com/artikel-patokan.html](https://website-anda.com/artikel-patokan.html)",
    "descriptionMode": "AI_WITH_TITLE"
  },
  "pinterest": {
    "boardUrl": "[https://www.pinterest.com/username/nama-board-anda/](https://www.pinterest.com/username/nama-board-anda/)"
  },
  "gemini": {
    "prompt": "Buat judul...",
    "rssPrompt": "Buat deskripsi pin..."
  },
  "settings": {
    "destinationLink": "[https://website-atau-blog-anda.com](https://website-atau-blog-anda.com)"
  }
}
```
* **`runMode`**: Atur mode bot: `"pexels"`, `"rss"`, atau `"both"`. **(Wajib diubah)**
* **`pexels.keywordFile`**: Sama seperti di atas. **(Wajib diubah)**
* **`rss.feedUrl`**: URL RSS Feed dari blog/website Anda. **(Wajib diubah)**
* **`rss.startFromLink`**: URL artikel spesifik sebagai titik awal. Bot hanya akan memposting artikel yang lebih baru dari ini. **(Wajib diubah)**
* **`pinterest.boardUrl`**: Sama seperti di atas. **(Wajib diubah)**
* **`settings.destinationLink`**: Link tujuan *default* jika mode Pexels berjalan. **(Wajib diubah)**

### 3. `keywords.txt`

File ini digunakan oleh **kedua bot** untuk mode Pexels.
* **Edit file ini** dan isi dengan daftar kata kunci yang Anda inginkan, **satu per baris**. Bot akan membacanya secara berurutan dan berulang (loop).

---

## 🚀 Panduan Penggunaan Lengkap

Ikuti langkah-langkah di bawah ini untuk mengaktifkan bot Anda.

### Langkah 1: Mendapatkan Cookies Pinterest

1.  **Install Ekstensi:** Pasang ekstensi **Cookie-Editor** di browser Google Chrome atau Firefox.
2.  **Login ke Pinterest:** Buka [pinterest.com](https://www.pinterest.com) dan login ke akun Anda.
3.  **Export Cookies:**
    * Klik ikon ekstensi **Cookie-Editor**.
    * Klik tombol **"Export"** -> **"Export as JSON"**. Ini akan menyalin data *cookies* ke *clipboard* Anda.
4.  **Simpan Teks:** Simpan teks JSON ini di Notepad untuk digunakan pada langkah berikutnya.

### Langkah 2: Pengaturan di GitHub

1.  **Impor Repository:**
    * Pergi ke halaman [Impor Repository GitHub](https://github.com/new/import).
    * Pada bagian **"Your old repository’s clone URL"**, masukkan URL repository bot yang Anda dapatkan.
    * Beri nama repository baru Anda (misalnya, `bot-pinterest-saya`).
    * Pastikan Anda memilih opsi **"Private"** untuk menjaga kerahasiaan kode.
    * Klik **"Begin import"** dan tunggu hingga selesai.

2.  **Atur Secrets:**
    * Di repository **PRIVATE** baru Anda, navigasi ke **Settings** > **Secrets and variables** > **Actions**.
    * Klik **"New repository secret"** dan buat 4 *secret* berikut:
        * **`PEXELS_API_KEY`**: Isi dengan API Key Pexels Anda.
        * **`GEMINI_API_KEY`**: Isi dengan API Key Google Gemini Anda.
        * **`BOT_LICENSE_EMAIL`**: Isi dengan email yang Anda gunakan saat pembelian lisensi.
        * **`PINTEREST_COOKIES`**: Tempel (**paste**) seluruh teks JSON yang Anda dapatkan dari **Langkah 1**.

### Langkah 3: Konfigurasi & Jalankan Bot

1.  **Edit File Konfigurasi:** Di repository Anda, edit file `config.json` atau `config2.json` sesuai kebutuhan Anda (lihat penjelasan file di atas). Edit juga `keywords.txt`.
2.  **Jalankan Bot:**
    * **Otomatis:** Bot akan berjalan sesuai jadwal yang diatur di file `.yml` (default setiap beberapa jam).
    * **Manual:** Pergi ke tab **"Actions"**, pilih *workflow* yang sesuai (`bot-pexels` atau `bot-both`), lalu klik **"Run workflow"**.

### Langkah 4: Memeriksa Hasil & Debugging

* Anda bisa melihat log eksekusi bot secara *real-time* di tab **"Actions"**.
* Jika terjadi kegagalan (❌), buka ringkasan eksekusi tersebut dan cari bagian **"Artifacts"** untuk mengunduh `error-screenshot.png`.

---

## 📝 Kebijakan Lisensi

Dengan membeli dan menggunakan bot ini, Anda menyetujui ketentuan lisensi berikut.

* **Pemberian Lisensi:** Anda diberikan lisensi non-eksklusif dan tidak dapat dipindahtangankan untuk menggunakan perangkat lunak ini untuk tujuan pribadi atau komersial, yang divalidasi melalui `BOT_LICENSE_EMAIL` Anda.
* **Penggunaan Multi-Akun:** Anda diperbolehkan untuk menggunakan perangkat lunak ini pada **semua akun Pinterest yang Anda miliki secara pribadi atau kelola secara profesional untuk klien**.
* **Larangan Distribusi Ulang:** Anda **dilarang keras** untuk membagikan, menjual kembali, mendistribusikan, atau memberikan kode sumber bot ini dalam bentuk apa pun kepada pihak lain. Pelanggaran akan mengakibatkan pencabutan lisensi tanpa pengembalian dana.
* **Penafian:** Perangkat lunak ini disediakan "sebagaimana adanya". Anda menanggung semua risiko yang terkait dengan penggunaan perangkat lunak ini, termasuk kemungkinan penangguhan akun oleh Pinterest.

---

## ⚠️ Peringatan

Penggunaan segala bentuk otomatisasi atau bot memiliki risiko terhadap akun media sosial. Bot ini dirancang untuk meminimalkan risiko, namun pihak Pinterest dapat mengubah kebijakannya kapan saja. Tanggung jawab penuh atas penggunaan bot ini ada pada Anda. Gunakan dengan bijak.
