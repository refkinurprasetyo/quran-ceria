# 🌙 Al-Qur'an Ceria

Aplikasi belajar membaca Al-Qur'an untuk anak — ramah anak, penuh warna, dengan **murottal qari asli**. Dilengkapi **akun Guru & Murid**: murid belajar dan mengumpulkan bintang, guru memantau progres semua murid lewat **dashboard real-time**.

Semuanya satu file (`index.html`) — cukup di-host di **GitHub Pages**, gratis.

---

## ✨ Fitur

- **Iqra** — 28 huruf hijaiyah bersuara + latihan harakat (fathah/kasrah/dhammah)
- **Game Cocokkan Huruf** — permainan mencocokkan huruf & namanya
- **Hafalan** — 11 surah pendek dengan **murottal asli** (6 pilihan qari) + mode uji hafalan
- **Tajwid** — kartu hukum bacaan warna-warni + kuis
- **Tilawah, Tafsir anak, Kenali Qari, Aktivitas Islami** (doa harian, wudhu, adab)
- **Akun Murid** — progres tersimpan & tersinkron
- **Dashboard Guru** — pantau bintang, huruf, hafalan, kuis, dll. tiap murid secara langsung

> Tanpa Firebase, aplikasi tetap berjalan dalam **Mode Offline** (progres hanya tersimpan di perangkat itu). Untuk memantau murid lintas perangkat, aktifkan Firebase (Langkah B).

---

## 🚀 A. Menaruh Online di GitHub Pages

1. Masukkan file **`index.html`** (dan `README.md`) ke repository GitHub Anda — lewat tombol **Add file → Upload files**, lalu **Commit**.
2. Buka **Settings** repo → menu **Pages** (kiri).
3. Bagian **Build and deployment → Source**, pilih **Deploy from a branch**.
4. Pilih branch **`main`** dan folder **`/ (root)`**, lalu **Save**.
5. Tunggu ±1 menit. Situs Anda akan online di:
   `https://<username-github-anda>.github.io/<nama-repo>/`

> Nama file **harus `index.html`** agar otomatis terbuka sebagai halaman utama.

---

## ☁️ B. Mengaktifkan Sinkron Antar-Perangkat (Firebase)

Agar guru bisa memantau murid yang belajar di HP/komputer lain, aktifkan database gratis Firebase.

### 1. Buat project Firebase
1. Buka https://console.firebase.google.com → **Add project** → beri nama (mis. `quran-ceria`) → lanjut sampai selesai.
2. Di menu kiri, buka **Build → Firestore Database** → **Create database** → pilih **Start in production mode** → pilih lokasi terdekat (mis. `asia-southeast2` Jakarta) → **Enable**.

### 2. Daftarkan Web App & salin config
1. Di **Project Overview**, klik ikon **`</>`** (Web) → beri nama app → **Register app**.
2. Salin objek `firebaseConfig` yang muncul, contoh:
   ```js
   const firebaseConfig = {
     apiKey: "AIzaSyxxxxxxxx",
     authDomain: "quran-ceria.firebaseapp.com",
     projectId: "quran-ceria",
     storageBucket: "quran-ceria.appspot.com",
     messagingSenderId: "1234567890",
     appId: "1:1234567890:web:abcdef123456"
   };
   ```
3. Buka `index.html`, cari blok **`window.firebaseConfig = { ... }`** (di bagian atas), lalu **ganti nilainya** dengan config Anda. Simpan & commit ulang ke GitHub.

### 3. Atur Aturan (Rules) Firestore
Di **Firestore Database → tab Rules**, tempel aturan berikut lalu **Publish** (isi file `firestore.rules` yang disertakan):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /classes/{classId} {
      allow read, write: if true;
      match /students/{studentId} {
        allow read, write: if true;
      }
    }
  }
}
```

> ⚠️ **Catatan keamanan (jujur):** aturan di atas sengaja sederhana agar mudah dipakai di kelas kecil, dan **membuka akses baca/tulis** ke data kelas. Karena itu, **jangan menyimpan data pribadi/sensitif** — cukup nama panggilan/nama depan anak dan progres belajar. Untuk keamanan lebih, Anda bisa mengaktifkan **Firebase App Check** atau **Anonymous Auth**. Data yang disimpan aplikasi ini memang hanya: nama, jumlah bintang, dan ringkasan progres.

---

## 👩‍🏫👦 Cara Memakai Akun

**Guru:**
1. Buka situs → pilih **"Saya Guru"**.
2. Isi **Nama**, **Kode Kelas** (bebas, mis. `KELASCERIA`), dan **PIN Guru** (rahasia).
3. Kelas otomatis dibuat saat pertama masuk. **Bagikan Kode Kelas** ke murid.
4. Dashboard menampilkan progres semua murid secara langsung.

**Murid:**
1. Buka situs → pilih **"Saya Murid"**.
2. Isi **Nama** dan **Kode Kelas** dari guru → **Masuk & Belajar**.
3. Setiap bintang yang dikumpulkan otomatis tersimpan dan terlihat di dashboard guru.

> Satu Kode Kelas = satu kelas. Guru cukup satu PIN; murid tidak perlu PIN, hanya kode kelas.

---

## 🔊 Tentang Audio
- **Murottal ayat**: rekaman qari asli via CDN `islamic.network` (utama) & `everyayah.com` (cadangan). Butuh koneksi internet.
- **Suara huruf hijaiyah & doa**: memakai pelafalan otomatis perangkat (Web Speech) sebagai alat bantu latihan.

## 📄 Lisensi
Bebas dipakai untuk pendidikan. Teks Al-Qur'an mengikuti mushaf standar; audio milik masing-masing penyedia.

Dibuat dengan ❤️ untuk anak-anak calon penghafal Al-Qur'an.
