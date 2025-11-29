# 🌿 Rinku Chat

Rinku Chat adalah aplikasi chat berbasis **Vue 3 + TailwindCSS** dengan tampilan personal dan hangat.  
Frontend ini terhubung langsung dengan backend **Subaru Awa**, sebuah AI Chatbot yang menangani login dan generasi balasan.  

UI dibuat seperti aplikasi chat personal yang lembut—bubble melengkung, avatar karakter Rinku, background grid hijau pastel, dan typing indicator yang hidup.

---

## ✨ Fitur Utama

### 🔐 Autentikasi
- Login dengan endpoint `/auth/login`
- Validasi username & password
- Token JWT disimpan di state dan digunakan untuk aksi chat

### 💬 Sistem Chat Real-Time
- Bubble chat untuk **Kamu** (user)
- Bubble chat lengkap avatar untuk **Rinku** (AI)
- Pesan ditampilkan dengan animasi halus

### 🟢 Typing Indicator
- Tiga titik animasi yang menandakan Rinku sedang mengetik
- Muncul otomatis saat request sedang diproses

### 📜 Auto-scroll
- Selalu scroll ke pesan terbaru setelah pesan masuk/keluar
- Tidak mengganggu scroll manual di tengah chat

### 📌 Input Tetap di Bawah
- Kotak input fixed di bagian bawah layar
- Tetap nyaman dipakai meskipun percakapan sudah panjang

### 🌈 UI Lembut & Responsive
- Tampilan grid hijau pastel
- Bubble chat melengkung
- Avatar karakter Rinku di sisi kanan
- Tab menu: **Beranda · Chat · Tentang Rinku**

---

## 🧩 Teknologi yang Digunakan

- **Vue 3** (`<script setup>`)
- **TailwindCSS**
- **Vite**
- **lucide-vue-next** (ikon tombol kirim)
- **Fetch API** (komunikasi backend)
- **TransitionGroup** (animasi bubble chat)

---

## 📁 Struktur Folder

```txt
src/
 ├─ components/
 │   ├─ ChatApp.vue
 │   ├─ ChatHeader.vue
 │   ├─ ChatMessages.vue
 │   └─ ChatInput.vue
 ├─ assets/
 │   └─ Rinku-avatar.png
 ├─ App.vue
 └─ main.js
````

---

## 🧠 Cara Kerja Sistem

### 1. Login

User memasukkan username & password → dikirim ke `/auth/login`
Jika benar → backend mengirim token JWT → disimpan di state Vue.

### 2. Mengirim Pesan

Saat user Kirim Pesan:

* Pesan user ditampilkan
* Input dikunci
* Typing indicator muncul
* Pesan dikirim ke `/noa/chat` menggunakan token
* Balasan AI ditampilkan sebagai bubble Rinku

### 3. UI

* Pesan Rinku muncul di kanan lengkap avatar
* Pesan user muncul di kiri
* Smooth scroll otomatis

---

## 🔧 Konfigurasi Backend

Ubah `API_BASE_URL` di `ChatApp.vue`:

```js
const API_BASE_URL = "http://localhost:3000"
// atau
// const API_BASE_URL = "https://sa1-w.vercel.app"
```

Endpoint yang digunakan:

| Endpoint      | Method | Fungsi                          |
| ------------- | ------ | ------------------------------- |
| `/auth/login` | POST   | Login & ambil token             |
| `/noa/chat`   | POST   | Kirim pesan & terima jawaban AI |

---

## 🛠 Instalasi & Menjalankan

### 1. Clone Repo

```bash
git clone <url-repo>
cd Rinku-chat
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Jalankan Dev Server

```bash
npm run dev
```

### 4. Build untuk Produksi

```bash
npm run build
npm run preview
```

---

## 🚀 Deploy ke Vercel

1. Push project ke GitHub
2. Buka Vercel → **New Project**
3. Import repository
4. Pilih framework: **Vue**
5. Tambahkan environment variable:

```
VITE_API_BASE_URL = https://backend-kamu.vercel.app
```

6. Deploy 🎉

---

## 🖼️ Preview Tampilan

> *(Tambahkan screenshot kamu sendiri)*

```
public/Rinku-chat-preview.png
```

---

## 📝 Changelog

### **v1.0.0 — Release Awal**

* Login JWT + integrasi backend Subaru Awa
* UI chat hijau pastel
* Typing indicator
* Avatar Rinku
* Auto scroll
* Input fixed bottom
* Bubble animasi dengan `<TransitionGroup>`

---

## 📣 Deskripsi Singkat

**Rinku Chat adalah aplikasi chat AI berbasis Vue dengan tampilan lembut bernuansa hijau pastel. Terhubung ke backend Subaru Awa untuk login dan percakapan real-time, dilengkapi avatar karakter, bubble chat melengkung, dan animasi typing yang membuat percakapan terasa hidup dan personal.**

---

## 📄 Lisensi

Apache