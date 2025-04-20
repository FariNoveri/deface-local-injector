## ⚠️ Peringatan: Hanya untuk Bersenang-Senang! ⚠️

Proyek ini hanya untuk **bersenang-senang**. Tidak ada niat serius di sini. 😎

Silakan bereksperimen, bermain, dan nikmati prosesnya — tapi ingat, **jangan merusak apa pun**! 🎉

Jika kamu sedang bersenang-senang, berarti kamu melakukannya dengan benar. Tetap ringan, tetap menyenankan! 🚀

---

## **Langkah 1: Menyiapkan File HTML Lokal**

1. **Buat File HTML yang Akan Digunakan**
   - Pertama, buat file HTML dengan tampilan yang ingin kamu tampilkan. Ini adalah file yang akan menggantikan tampilan website yang ingin kamu ubah. Kamu bisa menggunakan teks editor seperti **Notepad++**, **VSCode**, atau **Sublime Text** untuk membuat file HTML.
   - Misalnya, buat file bernama `deface.html` di folder lokal kamu (misalnya di **D:/Script/deface.html**).

   Berikut contoh **kode HTML** untuk file `deface.html`:

   ```html
   <!-- Contoh file HTML (deface.html) -->
   <html>
       <head>
           <title>Tampilan Kustom</title>
       </head>
       <body>
           <h1>Selamat datang di halaman kustom saya!</h1>
       </body>
   </html>
   ```

   - Simpan file ini di folder lokal yang mudah diakses.

---

## **Langkah 2: Menjalankan Server Lokal menggunakan Python**

Untuk menjalankan file HTML kamu di server lokal, kita membutuhkan server yang bisa mengakses file di sistem lokal dan melayani permintaan HTTP. **Python** adalah pilihan terbaik untuk ini.

### **1. Install Python**
Jika Python belum terpasang, kamu perlu menginstalnya terlebih dahulu. Kamu bisa mengunduhnya di [https://www.python.org/downloads/](https://www.python.org/downloads/).

Setelah terinstal, pastikan Python bisa diakses dari terminal dengan menjalankan perintah ini:

```bash
python --version
```

Jika Python sudah terinstal dengan benar, kamu akan melihat versi Python yang terpasang.

### **2. Menjalankan Server Lokal dengan Python**
Setelah Python terinstal, buka **Command Prompt (Windows)** atau **Terminal (Mac/Linux)**, lalu ikuti langkah berikut:

#### 2.1 Masuk ke Direktori Tempat File HTML Tersimpan
Misalnya file `deface.html` kamu ada di folder `D:/Script`, gunakan perintah **cd** untuk masuk ke folder tersebut:

```bash
cd D:/Script
```

#### 2.2 Menjalankan Server Lokal dengan Python
Setelah berada di folder yang benar, jalankan server HTTP menggunakan Python dengan perintah berikut:

```bash
python -m http.server
```

Jika menggunakan Python versi 3, gunakan perintah ini:

```bash
python3 -m http.server
```

Server ini akan berjalan di alamat **http://127.0.0.1:8000**. Artinya, file kamu dapat diakses di alamat berikut:

```
http://127.0.0.1:8000/deface.html
```

Jangan tutup terminal atau command prompt ini karena server sedang berjalan.

---

## **Langkah 3: Menyusun Skrip Tampermonkey untuk Mengganti Tampilan Website**

**Tampermonkey** adalah ekstensi browser yang memungkinkan kamu untuk menjalankan **UserScript** di halaman web tertentu. Dengan ini, kamu bisa mengganti tampilan website sesuai dengan yang kamu inginkan.

### **1. Install Tampermonkey**

Jika belum terpasang, **install Tampermonkey** di browser kamu (Chrome, Firefox, Edge, dll.). Kamu bisa mengunduhnya di [https://www.tampermonkey.net/](https://www.tampermonkey.net/).

### **2. Membuat UserScript Baru di Tampermonkey**

Setelah Tampermonkey terpasang di browser, ikuti langkah berikut:

#### 2.1 Buka Dashboard Tampermonkey
Klik ikon **Tampermonkey** di toolbar browser kamu, lalu pilih **Create a new script**.

#### 2.2 Salin Kode Berikut ke dalam Skrip Baru

Di editor Tampermonkey, salin dan tempel kode berikut:

```javascript
// ==UserScript==
// @name         Ganti Tampilan Website ke HTML Lokal
// @namespace    http://tampermonkey.net/
// @version      0.1
// @description  Ganti tampilan website dengan HTML lokal
// @author       You
// @match        https://spada.teknokrat.ac.id/*  // Ganti dengan URL yang sesuai
// @grant        GM_xmlhttpRequest
// ==/UserScript==

(function() {
    // Ambil file HTML dari server lokal
    var xhr = new XMLHttpRequest();
    xhr.open('GET', 'http://127.0.0.1:8000/deface.html', true);  // Ganti dengan URL server lokal kamu
    xhr.onreadystatechange = function() {
        if (xhr.readyState == 4 && xhr.status == 200) {
            document.open();
            document.write(xhr.responseText);  // Tulis HTML lokal ke halaman
            document.close();
        }
    };
    xhr.send();
})();
```

#### 2.3 Menyesuaikan URL
Pastikan URL `http://127.0.0.1:8000/deface.html` sesuai dengan alamat file HTML yang kamu jalankan di server lokal kamu. Jika kamu menggunakan server lain atau port yang berbeda, sesuaikan URL tersebut.

---

## **Langkah 4: Menjalankan dan Menguji Skrip**

### **1. Jalankan Server Lokal**
Pastikan server Python kamu masih berjalan di **http://127.0.0.1:8000/deface.html**.

### **2. Aktifkan Skrip Tampermonkey**
Pastikan skrip Tampermonkey yang baru saja kamu buat dalam keadaan aktif.

### **3. Buka Website yang Ingin Diubah**
Buka website **https://spada.teknokrat.ac.id/** di browser kamu. Skrip akan dijalankan otomatis dan mengubah tampilan halaman sesuai dengan HTML lokal kamu.

---

## **Langkah 5: Mengatasi Masalah CORS**

Jika kamu mendapatkan error **CORS** (Cross-Origin Resource Sharing) saat mencoba memuat file HTML dari server lokal kamu, browser akan memblokir permintaan tersebut. Errornya akan terlihat seperti ini:

```
Access to XMLHttpRequest at 'http://127.0.0.1:8000/deface.html' from origin 'https://spada.teknokrat.ac.id' has been blocked by CORS policy
```

### **Solusi untuk CORS**
Untuk mengatasi masalah CORS, kamu bisa melakukan beberapa hal berikut:

### **1. Gunakan `http-server` dengan CORS**

Gunakan **`http-server`** (dari Node.js) yang secara otomatis mengaktifkan **CORS**. Jika kamu belum menginstal **Node.js** dan **npm**, kamu bisa mengunduhnya di [https://nodejs.org/](https://nodejs.org/).

Setelah itu, install **http-server** dengan perintah:

```bash
npm install -g http-server
```

Jalankan server dengan CORS diaktifkan:

```bash
http-server --cors
```

Server akan berjalan di alamat **http://127.0.0.1:8080**. Update URL pada skrip Tampermonkey kamu menjadi `http://127.0.0.1:8080/deface.html`.

### **2. Matikan CORS di Browser (Hanya untuk Testing)**
Kamu bisa menonaktifkan CORS di browser, namun ini **hanya untuk tujuan pengujian**. Tidak disarankan untuk penggunaan sehari-hari.

---

Dengan langkah-langkah ini, kamu bisa mengganti tampilan website **hanya untuk diri sendiri** menggunakan **Tampermonkey**, **Python** sebagai server lokal, dan file HTML yang sudah kamu buat!

![GIF](https://img.wattpad.com/41c9345d63a13b6e112f04f3946bc4f3a58063b8/68747470733a2f2f73332e616d617a6f6e6177732e636f6d2f776174747061642d6d656469612d736572766963652f53746f7279496d6167652f786c46503948593063656a6373773d3d2d3239363933343039322e313437366131393238383631326566373139333235353433363333372e676966)
