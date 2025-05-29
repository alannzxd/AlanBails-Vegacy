# Baileys WhatsApp API - By AlannXD

<div align="center"><img src="https://files.catbox.moe/urxlw4.jpg"></div>

<div align='center'>

![GitHub Downloads (all assets, all releases)](https://img.shields.io/github/downloads/whiskeysockets/baileys/total)
![NPM Downloads](https://img.shields.io/npm/dw/%40whiskeysockets%2Fbaileys?label=npm&color=%23CB3837)
![GitHub code size in bytes](https://img.shields.io/github/languages/code-size/whiskeysockets/baileys)
![GitHub License](https://img.shields.io/github/license/whiskeysockets/baileys)
![Discord](https://img.shields.io/discord/725839806084546610?label=discord&color=%235865F2)
![GitHub Repo stars](https://img.shields.io/github/stars/whiskeysockets/baileys)
![GitHub forks](https://img.shields.io/github/forks/whiskeysockets/baileys)

</div>

AlanBails-Vegacy adalah library berbasis Node.js yang memanfaatkan protokol WhatsApp Web melalui Baileys. Proyek ini merupakan hasil modifikasi dari Whiskey Baileys dengan fokus pada stabilitas, performa tinggi, dan dukungan penuh terhadap fitur-fitur WhatsApp Multi-Device (MD).


---

🧩 Tentang Proyek

Proyek ini dikembangkan dan dikelola oleh AlannXD bersama komunitas open-source. Kontribusi dan kolaborasi sangat dihargai. Jika Anda tertarik untuk berkontribusi, silakan buat pull request atau laporkan masalah melalui tab Issues.


---

✨ Fitur Unggulan

✅ Autentikasi Tanpa QR Code
Gunakan autentikasi berbasis sesi tanpa perlu memindai QR berulang kali.

✅ Dukungan WhatsApp Multi-Device (MD)
Kompatibel dengan sistem multi-device terbaru dari WhatsApp.

✅ Pengiriman & Penerimaan Pesan Lengkap
Dukungan untuk teks, gambar, video, dokumen, stiker, audio, dan lainnya.

✅ Manajemen Grup
Buat grup, tambah/hapus anggota, ubah deskripsi, dan kelola lainnya melalui API.

✅ Integrasi Event Real-Time
Tangkap event seperti anggota masuk/keluar grup, pesan dibaca, pesan diterima, dll.



---

🛠️ Instalasi

git clone https://github.com/alannzxd/AlanBails-Vegacy.git
cd AlanBails-Vegacy
npm install


---

🚀 Penggunaan Dasar
```ts

const makeWASocket = require('./index');

async function startBot() {
  const sock = makeWASocket();

  sock.ev.on('messages.upsert', async ({ messages }) => {
    const msg = messages[0];
    if (!msg.message) return;
    await sock.sendMessage(msg.key.remoteJid, { text: 'Halo dari bot!' });
  });
}

startBot();


---

🧪 Fitur Lanjutan

🔐 Pairing Kode (Kode 6 Digit)
Autentikasi perangkat baru dengan kode pairing tanpa QR.

🧾 Pesan Interaktif
Kirim pesan dengan tombol, daftar, dan quick reply.

🛍️ Pesan Toko (Product Messages)
Kirim katalog produk dengan gambar, harga, dan deskripsi.

📊 Polling & Voting
Buat polling interaktif dalam grup atau chat pribadi.

🧷 Mention & Status
Mention pengguna dalam pesan dan kelola status.

🖼️ Pesan Album & Kartu (Card Messages)
Kirim galeri gambar atau pesan dengan tampilan kartu.

📌 Simpan & Sematkan Pesan
Simpan dan sematkan pesan penting dalam chat.

📩 Undangan Grup
Kirim undangan grup melalui tautan atau pesan khusus.



---

📂 Struktur Folder

AlanBails-Vegacy/
├── auth/           # Modul autentikasi sesi
├── lib/            # Logika utama protokol WhatsApp
├── messages/       # Handler pesan dan media
├── plugins/        # Plugin tambahan (opsional)
└── index.js        # Entry point utama


---

🤝 Kontribusi

Kami membuka pintu untuk semua bentuk kontribusi, baik berupa:

Pelaporan bug

Penambahan fitur baru

Dokumentasi

Refactoring kode


> Pastikan Anda membaca CONTRIBUTING.md sebelum membuat pull request.




---

📄 Lisensi

Proyek ini dirilis di bawah lisensi MIT. Silakan gunakan, modifikasi, dan distribusikan dengan bebas, selama tetap mencantumkan kredit kepada pengembang asli.


---

📫 Kontak & Komunitas

Author: AlannXD

GitHub: github.com/alannzxd

Telegram: @AlannXD

---

## Kontak

📩 **Email**: fuckingmoney@gmail.com  
🌍 **Website**: [Baileys API](https://github.com/alannzxd/AlanBails-Vegacy)  

---

🚀 **Semoga kamu suka & semangat ngoding!** �
