# 🔒 SuanggiCrypt // ASCII Cyber Ops

<p align="center">
  <img src="https://img.shields.io/badge/Security-AES--256--GCM-00ff66?style=for-the-badge&logo=shield" alt="AES-256-GCM">
  <img src="https://img.shields.io/badge/KDF-PBKDF2--SHA256-00ff66?style=for-the-badge&logo=lock" alt="PBKDF2">
  <img src="https://img.shields.io/badge/Engine-Web_Crypto_API-00ff66?style=for-the-badge&logo=javascript" alt="WebCrypto">
  <img src="https://img.shields.io/badge/License-MIT-00ff66?style=for-the-badge" alt="License">
</p>

<p align="center">
  <b>Aplikasi enkripsi teks berbasis peramban (zero server-side footprint) dengan backend Web Crypto API standar industri dan visual interaktif real-time ASCII webcam canvas.</b>
</p>

---

## 📌 Ringkasan Proyek

**SuanggiCrypt** adalah modul enkripsi portabel sisi klien (*client-side*) yang mengombinasikan standar kriptografi militer modern dengan estetika visual retro-*cyberpunk*. 

Berbeda dari skrip enkripsi dasar yang mengandalkan algoritma simetris statis atau *hardcoded keys*, seluruh proses enkripsi dan dekripsi di SuanggiCrypt dieksekusi secara terisolasi di dalam memori browser menggunakan **Web Crypto API** bawaan tanpa sekali pun mengirim data mentah maupun ciphertext ke server backend (*Zero-Knowledge Architecture*).

---

## ⚡ Fitur Utama

- **Enkripsi Terotentikasi (Authenticated Encryption):** Menggunakan **AES-256-GCM**, cipher mode modern yang menjamin kerahasiaan (*confidentiality*) sekaligus integritas pesan (*authenticity*). Jika satu bit saja diubah oleh penyerang, proses dekripsi akan langsung gagal.
- **Key Stretching Tangguh (PBKDF2):** Menerapkan 250.000 putaran hash SHA-256 yang dipadukan dengan Salt dinamis untuk memperlambat dan menggagalkan serangan *offline brute-force* berbasis GPU.
- **Entropi Kriptografis Asli:** Tidak ada generator acak pseudo-matematis biasa (`Math.random()`). Semua Salt dan IV dibangkitkan lewat `crypto.getRandomValues()` (CSPRNG tingkat OS).
- **Latar ASCII Webcam Real-Time:** Menangkap feed kamera webcam pengguna secara lokal dan merendernya menjadi susunan karakter ASCII berbasis luminansi piksel kanvas HTML5.
- **Matrix Digital Fallback:** Mode animasi matriks otomatis langsung aktif jika perizinan kamera ditolak atau perangkat tidak memiliki sensor webcam.
- **Zero-Dependency & Self-Contained:** Berjalan 100% menggunakan HTML5, CSS3 Glassmorphism, dan Vanilla JavaScript murni tanpa ketergantungan CDN eksternal yang rentan manipulasi rantai pasok (*supply chain attacks*).

---

## 🔬 Spesifikasi Kriptografi

| Parameter | Spesifikasi Teknis | Keterangan |
| :--- | :--- | :--- |
| **Cipher Engine** | AES (Advanced Encryption Standard) | Galois/Counter Mode (GCM) |
| **Key Size** | 256-bit (32 bytes) | Rekomendasi ketahanan Post-Quantum level simetris |
| **Key Derivation Function** | PBKDF2 | Standar RFC 2898 / NIST SP 800-132 |
| **KDF Iterations** | 250.000 rounds | Mengimbangi kemampuan akselerasi komputasi modern |
| **Hash Digest** | SHA-256 | Output 32-byte digest |
| **Salt Size** | 128-bit (16 bytes) | Mencegah serangan *pre-computed rainbow tables* |
| **IV / Nonce** | 96-bit (12 bytes) | Ukuran optimal dan paling aman untuk mode GCM |
| **Encoding Format** | Base64 Encoded | Portabel untuk disalin ke teks atau aplikasi chat |

### Struktur Payload Ciphertext
Hasil enkripsi dienkapsulasi menjadi satu paket byte terpadu sebelum dikonversi ke Base64:
```text
+-----------------------+--------------------+------------------------------------------+
|  Salt (0..15 / 16B)   |  IV (16..27 / 12B) | Ciphertext + GCM Auth Tag (28..n bytes)  |
+-----------------------+--------------------+------------------------------------------+
