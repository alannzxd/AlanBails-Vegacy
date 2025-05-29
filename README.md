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

Baileys WhatsApp API adalah library berbasis Node.js untuk berkomunikasi dengan WhatsApp Web tanpa perlu WebSocket tambahan. Ini adalah hasil modifikasi dari Whiskey Baileys agar lebih stabil dan mendukung lebih banyak tipe pesan.

Dikembangkan dengan performa tinggi untuk kebutuhan bot, otomatisasi pesan, dan integrasi aplikasi WhatsApp lainnya.

## Tentang Proyek Ini
Repositori ini dikembangkan dan dikelola oleh **AlannXD** bersama para kontributor open-source lainnya.  
Dukungan dan kontribusi dari komunitas sangat diapresiasi!   

---

## ✨ Fitur Utama

✅ **Autentikasi tanpa QR** menggunakan session authentication  
✅ **Dukungan Multi-Device (MD)** terbaru dari WhatsApp  
✅ **Kirim & terima pesan** dalam berbagai format  
✅ **Mengelola grup** (buat grup, tambahkan/kick anggota, atur deskripsi, dll.)  
✅ **Integrasi event** seperti masuk/keluar grup, pesan diterima, pesan terbaca  
---

## 🔐 Penggunaan Dasar Pairing Code

```js
import makeWASocket, { useMultiFileAuthState } from '@whiskeysockets/baileys';

const startSock = async () => {
  const { state, saveCreds } = await useMultiFileAuthState('./auth');
  const sock = makeWASocket({
    auth: state,
    printQRInTerminal: true,
  });

  sock.ev.on('creds.update', saveCreds);

  sock.ev.on('connection.update', async (update) => {
    const { connection, lastDisconnect, qr, pairingCode } = update;

    if (connection === 'open') {
      console.log('✅ Terhubung ke WhatsApp!');
    }

    if (pairingCode) {
      console.log('📲 Pairing code:', pairingCode);
    }
  });
};

startSock();


---

📚 Dokumentasi API

Fitur	Deskripsi

generatePairingCode()	Mengirim pairing code 6 digit
sendInteractive()	Mengirim semua jenis pesan interaktif
sendButton()	Mengirim pesan dengan tombol pilihan
sendStore()	Mengirim pesan toko (product message)
Lihat dokumentasi lengkap: Baileys Docs	



---

🔧 Contoh Kode Tambahan

📋 Mengirim Semua Interaktif Msg

await sock.sendMessage(id, {
  text: "Pilih salah satu opsi!",
  footer: "Interaktif msg",
  templateButtons: [
    { index: 1, urlButton: { displayText: "YouTube", url: "https://yt.alannzxd.my.id" } },
    { index: 2, callButton: { displayText: "Panggil Dev", phoneNumber: "+62xxx" } },
    { index: 3, quickReplyButton: { displayText: "Klik aku", id: "id_click" } },
  ],
});

🔘 Mengirim Pesan Button

await sock.sendMessage(id, {
  text: "Ini pesan dengan tombol",
  buttons: [
    { buttonId: "id1", buttonText: { displayText: "Tombol 1" }, type: 1 },
  ],
});

🛍️ Mengirim Pesan Toko

await sock.sendMessage(id, {
  product: {
    productImageCount: 1,
    title: "Top Up Game",
    description: "Aman dan terpercaya",
    currencyCode: "IDR",
    priceAmount1000: 10000,
  }
});

🗳️ Hasil Polling dari Newsletter

sock.ev.on('messages.upsert', ({ messages }) => {
  const msg = messages[0];
  if (msg.pollUpdates) {
    console.log("Polling Results:", msg.pollUpdates);
  }
});

👥 Mention di Status

await sock.sendMessage('status@broadcast', {
  text: "Halo semuanya 👋",
  mentions: ['628xxx@s.whatsapp.net']
});

🖼️ Pesan dengan Kartu

await sock.sendMessage(id, {
  text: "Berita Terbaru",
  externalAdReply: {
    title: "Lihat selengkapnya",
    body: "News Channel",
    thumbnailUrl: "https://example.com/image.jpg",
    mediaType: 1,
    sourceUrl: "https://example.com"
  }
});


---

📌 Fitur Tambahan Lain

💬 Kirim pesan album / galeri

📥 Menyimpan & menyematkan pesan

📨 Undangan grup via chat

🎨 Format teks kaya (bold, italic, dll)



---

📫 Kontak & Komunitas

Author: AlannXD

Telegram: @AlannXD

---

## Kontak

📩 **Email**: fuckingmoney@gmail.com  
🌍 **Website**: [Baileys API](https://github.com/alannzxd/AlanBails-Vegacy)  

---

🚀 **Semoga kamu suka & semangat ngoding!** �
