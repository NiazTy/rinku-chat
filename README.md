<div align="center" id="trendradar">

<strong>AIMOTO RINKU, SEBUAH AI YANG SANGAT POSITIF</strong>

[![GitHub Stars](https://img.shields.io/github/stars/NiazTy/rinku-chat?style=flat-square&logo=github&color=yellow)](https://github.com/NiazTy/rinku-chat/stargazers)
[![GitHub Forks](https://img.shields.io/github/forks/NiazTy/kupas-tuntas?style=flat-square&logo=github&color=blue)](https://github.com/NiazTy/rinku-chat/network/members)
[![License](https://img.shields.io/badge/license-MIT--3.0-blue.svg?style=flat-square)](LICENSE)
[![Version](https://img.shields.io/badge/version-v3.4.0-blue.svg)](https://github.com/NiazTy/rinku-chat)

[![GitHub Pages](https://img.shields.io/badge/GitHub_Pages-Deployment-4285F4?style=flat-square&logo=github&logoColor=white)](https://rinku-chat.vercel.app)

</div>

---

# 🌿 Rinku Chat

Rinku Chat adalah aplikasi chat berbasis **Vue 3 + TailwindCSS** dengan tampilan personal dan hangat.

UI dibuat seperti aplikasi chat personal yang lembut—bubble melengkung, avatar karakter Rinku, background grid hijau pastel, dan typing indicator yang hidup.

---

## ✨ Fitur Utama

### 💬 Sistem Chat Real-Time
- Bubble chat untuk **Kamu** (user)
- Bubble chat lengkap avatar untuk **Rinku** (AI)
- Pesan ditampilkan dengan animasi halus

### 🌈 UI Lembut & Responsive
- Tampilan grid hijau pastel
- Bubble chat melengkung
- Avatar karakter Rinku di sisi kanan

### 🌟 Rinku yang sudah dipersonalisasi
- Memiliki jawaban yang sangat manusiawi

---

## 🧩 Teknologi yang Digunakan

- **Vue 3** (`<script setup>`)
- **TailwindCSS**
- **Vite**

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

6. Deploy 🎉

---

## 🖼️ Preview Tampilan

<img src="/public/beranda.png" alt="Beranda" width="80%">

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