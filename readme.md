# 📱 Phone Screen Mirroring

Aplikasi web untuk melakukan screen mirroring dari handphone ke PC/Laptop menggunakan teknologi WebRTC dan QR Code.


## ✨ Fitur

- 🖥️ **Mode Penerima (PC/Laptop)** - Menerima dan menampilkan layar dari handphone
- 📱 **Mode Pengirim (Handphone)** - Membagikan layar handphone ke PC/Laptop
- 🔗 **QR Code Auto-Connect** - Koneksi mudah dengan scan QR code
- 🎯 **Manual ID Connection** - Opsi koneksi manual dengan ID
- 🔄 **Real-time Streaming** - Menggunakan WebRTC untuk streaming real-time
- 🎨 **Responsive Design** - Tampilan yang menyesuaikan dengan ukuran layar
- 🔊 **Audio Support** - Mendukung streaming audio (jika tersedia)

## 🚀 Cara Menggunakan

### Persiapan

1. **Download/Clone file `phone-mirror.html`**
2. **Host file di web server** (bisa menggunakan):
   - Local server (Python SimpleHTTPServer, Live Server VSCode, dll)
   - Online hosting (GitHub Pages, Netlify, Vercel, dll)
   - Atau buka langsung di browser (dengan keterbatasan tertentu)

### Langkah-langkah Mirroring

#### Di PC/Laptop (Penerima):

1. Buka `phone-mirror.html` di browser
2. Pilih **"Mode Penerima (PC/Laptop)"**
3. Klik tombol **"Buat Koneksi Baru"**
4. QR Code dan ID Koneksi akan muncul
5. Tunggu koneksi dari handphone

#### Di Handphone (Pengirim):

**Opsi 1: Menggunakan QR Code (Recommended)**
1. Buka `phone-mirror.html` di browser handphone
2. Pilih **"Mode Pengirim (Handphone)"**
3. Scan QR Code yang muncul di PC/Laptop
4. Klik **"Mulai Screen Sharing"**
5. Pilih layar/tab yang ingin dibagikan
6. Klik **"Share"**

**Opsi 2: Menggunakan ID Manual**
1. Buka `phone-mirror.html` di browser handphone
2. Pilih **"Mode Pengirim (Handphone)"**
3. Masukkan ID Koneksi yang tertera di PC/Laptop
4. Klik **"Mulai Screen Sharing"**
5. Pilih layar/tab yang ingin dibagikan
6. Klik **"Share"**

## 📋 Requirements

### Browser Support
- ✅ Chrome/Edge (Recommended) - versi 74+
- ✅ Firefox - versi 66+
- ✅ Safari - versi 12.1+
- ✅ Opera - versi 62+

### Koneksi
- Kedua device harus terhubung ke internet
- Untuk hasil terbaik, gunakan koneksi WiFi yang sama
- HTTPS diperlukan untuk screen sharing (kecuali localhost)

### Permissions
- Screen capture/sharing permission di handphone
- Microphone permission (opsional, untuk audio)

## 🛠️ Teknologi yang Digunakan

- **WebRTC** - Untuk peer-to-peer video streaming
- **QRCode.js** - Generate QR code
- **LocalStorage** - Signaling mechanism (demo)
- **HTML5 Canvas** - Rendering
- **CSS3** - Styling & animations

## ⚙️ Setup Development

### Quick Start dengan Python

```bash
# Python 3
python -m http.server 8000

# Python 2
python -m SimpleHTTPServer 8000
```

Kemudian buka `http://localhost:8000/phone-mirror.html`

### Dengan Node.js (http-server)

```bash
# Install http-server
npm install -g http-server

# Run server
http-server -p 8000
```

### Dengan PHP

```bash
php -S localhost:8000
```

### Dengan VS Code Live Server

1. Install extension "Live Server"
2. Klik kanan pada `phone-mirror.html`
3. Pilih "Open with Live Server"

## 🔧 Konfigurasi

### Mengubah STUN Servers

Edit bagian `configuration` di script:

```javascript
const configuration = {
    iceServers: [
        { urls: 'stun:stun.l.google.com:19302' },
        { urls: 'stun:stun1.l.google.com:19302' },
        // Tambahkan STUN/TURN server lainnya di sini
    ]
};
```

### Mengubah Kualitas Video

Edit bagian `getDisplayMedia`:

```javascript
localStream = await navigator.mediaDevices.getDisplayMedia({
    video: { 
        width: { ideal: 1920 },  // Ubah resolusi
        height: { ideal: 1080 },
        frameRate: { ideal: 30 } // Tambahkan frame rate
    },
    audio: true
});
```

## 🚨 Troubleshooting

### Koneksi Gagal

**Problem:** "Tidak bisa terhubung antara device"

**Solusi:**
- Pastikan kedua device menggunakan file yang sama
- Periksa koneksi internet
- Coba gunakan browser yang berbeda
- Clear localStorage: `localStorage.clear()` di console
- Pastikan tidak ada firewall yang memblokir WebRTC

### QR Code Tidak Muncul

**Problem:** "QR Code tidak ter-generate"

**Solusi:**
- Pastikan library QRCode.js ter-load dengan baik
- Periksa console untuk error
- Pastikan koneksi internet stabil (untuk CDN)

### Screen Sharing Tidak Berfungsi

**Problem:** "Tidak ada opsi untuk share screen di handphone"

**Solusi:**
- Gunakan HTTPS (bukan HTTP)
- Gunakan browser yang support screen sharing
- Update browser ke versi terbaru
- Di beberapa Android, gunakan Chrome atau Firefox

### Video Lag/Patah-patah

**Problem:** "Video tidak smooth"

**Solusi:**
- Gunakan WiFi yang lebih baik
- Kurangi resolusi video di konfigurasi
- Pastikan tidak ada aplikasi lain yang menggunakan bandwidth besar
- Kedua device sebaiknya di jaringan yang sama

## 📱 Platform Compatibility

| Platform | Browser | Screen Share | Status |
|----------|---------|--------------|--------|
| Android | Chrome | ✅ | Supported |
| Android | Firefox | ✅ | Supported |
| iOS/iPadOS | Safari | ⚠️ | Limited* |
| Windows | Chrome/Edge | ✅ | Supported |
| macOS | Safari/Chrome | ✅ | Supported |
| Linux | Chrome/Firefox | ✅ | Supported |

*iOS Safari memiliki keterbatasan dalam screen sharing

## ⚠️ Limitasi

1. **Signaling dengan LocalStorage:**
   - Hanya bekerja jika kedua device membuka file dari domain yang sama
   - Tidak persistent setelah refresh
   - Untuk production, gunakan WebSocket server

2. **Browser Compatibility:**
   - Tidak semua browser mobile support screen capture API
   - iOS Safari memiliki keterbatasan

3. **Network:**
   - Memerlukan koneksi internet yang stabil
   - Kualitas video tergantung bandwidth

## 🔐 Security & Privacy

- Koneksi peer-to-peer menggunakan WebRTC (end-to-end)
- Tidak ada data yang disimpan di server (menggunakan localStorage lokal)
- ID koneksi bersifat random dan temporary
- **Catatan:** Untuk production, implementasikan enkripsi dan autentikasi yang proper

## 🚀 Production Deployment

Untuk deployment production, pertimbangkan:

1. **Signaling Server:**
   - Implementasikan WebSocket server untuk signaling
   - Gunakan Socket.io atau library sejenis
   - Contoh: Node.js + Express + Socket.io

2. **TURN Server:**
   - Tambahkan TURN server untuk NAT traversal
   - Gunakan layanan seperti Twilio, Xirsys, atau self-hosted

3. **HTTPS:**
   - Wajib menggunakan HTTPS untuk production
   - Dapatkan SSL certificate (Let's Encrypt gratis)

4. **Scalability:**
   - Implementasikan load balancing
   - Gunakan CDN untuk static assets
   - Database untuk session management

## 📄 License

MIT License - Bebas digunakan untuk personal maupun komersial.

## 🤝 Contributing

Contributions welcome! Silakan:
1. Fork repository
2. Buat branch fitur (`git checkout -b feature/AmazingFeature`)
3. Commit changes (`git commit -m 'Add some AmazingFeature'`)
4. Push ke branch (`git push origin feature/AmazingFeature`)
5. Buat Pull Request

## 📞 Support

Jika mengalami masalah atau memiliki pertanyaan:
- Buka Issue di repository
- Periksa dokumentasi WebRTC
- Lihat browser console untuk error messages

## 🙏 Credits

- QRCode.js - https://github.com/davidshimjs/qrcodejs
- WebRTC - https://webrtc.org/
- STUN Servers - Google

## 📝 Changelog

### Version 1.0.0 (2026-01-31)
- ✅ Initial release
- ✅ Basic screen mirroring functionality
- ✅ QR code connection
- ✅ Manual ID connection
- ✅ Responsive UI design

---

**Dibuat dengan ❤️ untuk kemudahan screen mirroring**
