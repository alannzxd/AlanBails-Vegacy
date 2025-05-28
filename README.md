# Baileys WhatsApp API - By AlannXD

<div align="center"><img src="https://files.catbox.moe/2rpl7j.jpg"></div>

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

## Instalasi

Pastikan **Node.js ≥ 14.0++** sudah terpasang,
Kemudian jalankan perintah berikut di terminal:

```sh
npm install @alannzxd/AlanBails-Vegacy
```

Atau dengan **Yarn**:

```sh
yarn add @alannzxd/AlanBails-Vegacy
```

---

## Penggunaan Dasar pairing code

```javascript
const { useMultiFileAuthState, makeWASocket } = require('@alannzxd/AlanBails-Vegacy');
const readline = require('readline');

const rl = readline.createInterface({ input: process.stdin, output: process.stdout });
const question = (q) => new Promise(res => rl.question(q, res));

async function start() {
  const { state, saveCreds } = await useMultiFileAuthState('./session');
  const usePairingCode = true;

  const conn = makeWASocket({
    auth: state,
    printQRInTerminal: !usePairingCode,
    keepAliveIntervalMs: 50000,
  });

  conn.ev.on('creds.update', saveCreds);

  if (usePairingCode && !conn.authState.creds.registered) {
    const phone = (await question('Enter Your Number Phone:\n')).replace(/\D/g, '');
    rl.close();
    try {
      const code = await conn.requestPairingCode(phone);
      console.log('Code Whatsapp:', code.match(/.{1,4}/g).join('-'));
    } catch (e) {
      console.log('Failed to get pairing code:', e.message);
    }
  }

  conn.ev.on('connection.update', ({ connection, lastDisconnect }) => {
    if (connection === 'close') {
      const reason = lastDisconnect?.error?.output?.statusCode || 'Unknown';
      console.log('Connection closed:', reason);
      if ([401, 405].includes(reason)) {
        console.log('Logged out, delete session folder to relogin');
      } else if ([515, 428].includes(reason)) {
        console.log('Restarting...');
        start();
      }
    } else if (connection === 'open') {
      console.log('Whatsapp connected');
    }
  });

  conn.ev.on('messages.upsert', async (m) => {
    if (m.type === 'notify') {
      const msg = m.messages[0];
      if (!msg.key.fromMe && msg.message) {
        await conn.sendMessage(msg.key.remoteJid, { text: 'Hello there!' });
      }
    }
  });
}

start();
```

---

## Dokumentasi API

| Fitur               | Deskripsi |
|---------------------|----------|
| `sendMessage()`    | Mengirim pesan teks, gambar, video, dll. |
| `updateProfile()`  | Mengubah foto profil dan nama pengguna |
| `getChats()`       | Mendapatkan daftar chat pengguna |
| `groupParticipantsUpdate()` | Menambahkan/menghapus anggota grup |

📖 **Dokumentasi lengkap:** [Baileys API Docs](https://github.com/adiwajshing/Baileys/wiki)

---

## Contoh Kode Tambahan

### Mengirim Semua Interaktif Msg  
```ts
await sock.sendMessage(m.chat, {
  text: "halo",
  title: "tes",
  footer: "© ᴋᴀɢᴇɴᴏᴜ - 2025",
  interactiveButtons: [{
               "name": "single_select",
               "buttonParamsJson": "{\"title\":\"title\",\"sections\":[{\".menu\":\".play dj webito\",\"highlight_label\":\"label\",\"rows\":[{\"header\":\"header\",\"title\":\"title\",\"description\":\"description\",\"id\":\"id\"},{\"header\":\"header\",\"title\":\"title\",\"description\":\"description\",\"id\":\"id\"}]}]}"
             },
             {
               "name": "cta_reply",
               "buttonParamsJson": "{\"display_text\":\"quick_reply\",\"id\":\"message\"}"
             },
               {
                "name": "cta_url",
                "buttonParamsJson": "{\"display_text\":\"url\",\"url\":\"https://www.google.com\",\"merchant_url\":\"https://www.google.com\"}"
             },
             {
                "name": "cta_call",
                "buttonParamsJson": "{\"display_text\":\"call\",\"id\":\"message\"}"
             },
             {
                "name": "cta_copy",
                "buttonParamsJson": "{\"display_text\":\"copy\",\"id\":\"123456789\",\"copy_code\":\"message\"}"
             },
             {
                "name": "cta_reminder",
                "buttonParamsJson": "{\"display_text\":\"Recordatorio\",\"id\":\"message\"}"
             },
             {
                "name": "cta_cancel_reminder",
                "buttonParamsJson": "{\"display_text\":\"cta_cancel_reminder\",\"id\":\"message\"}"
             },
             {
                "name": "address_message",
                "buttonParamsJson": "{\"display_text\":\"address_message\",\"id\":\"message\"}"
             },
             {
                "name": "send_location",
                "buttonParamsJson": ""
             }]
}, { quoted: m });
```


### Mengirim Pesan Button  
```ts
sock.sendMessage(m.chat, {
     text: "Hello World !",
     footer: "JustKagenou",
     buttons: [ 
         { buttonId: `.play`,
          buttonText: {
              displayText: 'ini button'
          }, type: 1 }
     ],
     headerType: 1,
     viewOnce: true
 },{ quoted: null })
```

### Mengirim Pesan Toko  
```ts
sock.sendMessage(msg.key.remoteJid, {
    text: "Isi Pesan",
    title: "Judul",
    subtitle: "Subjudul",
    footer: "Footer",
    viewOnce: true,
    shop: 3,
    id: "199872865193",
}, { quoted: m })
```

### Hasil Polling dari Newsletter  
```ts
await sock.sendMessage(msg.key.remoteJid, {
    pollResult: {
        name: "Judul Polling",
        votes: [
            ["Opsi 1", 10], 
            ["Opsi 2", 10]
        ],
    }
}, { quoted: m })
```

### Mention di Status  
```ts
await sock.StatusMentions({ text: "Halo!" }, [
    "123456789123456789@g.us",
    "123456789@s.whatsapp.net",
])
```

### Pesan dengan Kartu  
```ts
await sock.sendMessage(msg.key.remoteJid, {
    text: "Halo!",
    footer: "Pesan Footer",
    cards: [
        {
            image: { url: 'https://example.jpg' }, 
            title: 'Judul Kartu',
            caption: 'Keterangan Kartu',
            footer: 'Footer Kartu',
            buttons: [
                { name: "quick_reply", buttonParamsJson: JSON.stringify({ display_text: "Tombol Cepat", id: "ID" }) },
                { name: "cta_url", buttonParamsJson: JSON.stringify({ display_text: "Buka Link", url: "https://www.example.com" }) }
            ]
        }
    ]
}, { quoted: m })
```

### Pesan Album  
```ts
await sock.sendAlbumMessage(msg.key.remoteJid, [
    { image: { url: "https://example.jpg" }, caption: "Halo Dunia" },
    { video: { url: "https://example.mp4" }, caption: "Halo Dunia" }
], { quoted: m, delay: 2000 })
```

### Menyimpan & Menyematkan Pesan  
```ts
await sock.sendMessage(msg.key.remoteJid, { keep: message.key, type: 1, time: 86400 })
await sock.sendMessage(msg.key.remoteJid, { pin: message.key, type: 1, time: 86400 })
```

### Pesan Undangan Grup  
```ts
await sock.sendMessage(msg.key.remoteJid, { 
    groupInvite: { 
        subject: "Nama Grup",
        jid: "1234@g.us",
        text: "Undangan Grup",
        inviteCode: "KODE",
        inviteExpiration: 86400 * 3,
    } 
}, { quoted: m })
```
**Dan Banyak Lagi Kode Pesan Baharu**
---

## Kontribusi

Kami menyambut kontribusi dari siapa saja! Jika ingin membantu:  
1. **Fork** repositori ini  
2. **Buat branch baru**  
3. **Buat Pull Request (PR)**  

---

## Kontak

📩 **Email**: fuckingmoney@gmail.com  
🌍 **Website**: [Baileys API](https://github.com/alannzxd/AlanBails-Vegacy)  

---

🚀 **Semoga kamu suka & semangat ngoding!** �
