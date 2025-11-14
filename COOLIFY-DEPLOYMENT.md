# 🚀 Deploy WhatsApp Bot ke Coolify

Panduan lengkap deploy WhatsApp Bot dengan QR Code download ke Coolify.

## 📋 Persiapan

### 1. File yang Diperlukan

Pastikan file-file ini ada di repository:
- ✅ `bot.js` - Bot utama dengan HTTP server
- ✅ `package.json` - Dependencies
- ✅ `Dockerfile` - Container configuration
- ✅ `.dockerignore` - Exclude files
- ✅ `check-book.js` - Helper functions

### 2. Push ke Git Repository

```bash
git init
git add .
git commit -m "Initial commit - WhatsApp Bot"
git remote add origin <your-git-url>
git push -u origin main
```

## 🔧 Setup di Coolify

### Step 1: Create New Resource

1. Login ke Coolify dashboard
2. Klik **"+ New Resource"**
3. Pilih **"Docker Compose"** atau **"Dockerfile"**
4. Connect ke Git repository kamu

### Step 2: Configure Application

**General Settings:**
- **Name:** whatsapp-bot
- **Port:** 3000
- **Build Pack:** Dockerfile

**Environment Variables:**
```env
PORT=3000
NODE_ENV=production
```

**Health Check:**
- **Path:** `/health`
- **Port:** 3000
- **Interval:** 30s

### Step 3: Deploy

1. Klik **"Deploy"**
2. Tunggu build process selesai
3. Coolify akan assign public URL

## 📱 Cara Menggunakan

### 1. Akses QR Code

Setelah deploy berhasil, buka URL yang diberikan Coolify:

```
https://your-app.coolify.io
```

Kamu akan melihat halaman dengan:
- ✅ QR Code yang auto-refresh
- ✅ Tombol download QR Code
- ✅ Instruksi cara scan

### 2. Download QR Code

**Cara 1: Via Browser**
- Buka `https://your-app.coolify.io`
- Klik tombol **"💾 Download QR Code"**
- File `qr_code_bot-wa-saya.png` akan terdownload

**Cara 2: Direct Download**
- Akses: `https://your-app.coolify.io/download-qr`
- QR Code langsung terdownload

**Cara 3: Via API**
```bash
curl -O https://your-app.coolify.io/download-qr
```

### 3. Scan QR Code

1. Buka WhatsApp di HP
2. Tap menu (⋮) → **Linked Devices**
3. Tap **"Link a Device"**
4. Scan QR code dari browser atau file yang didownload
5. Bot akan terkoneksi!

## 🔍 Monitoring

### Health Check

Cek status bot:
```bash
curl https://your-app.coolify.io/health
```

Response:
```json
{
  "status": "ok",
  "qrReady": true,
  "timestamp": "2025-11-14T14:30:00.000Z"
}
```

### Logs

Di Coolify dashboard:
1. Pilih aplikasi **whatsapp-bot**
2. Klik tab **"Logs"**
3. Lihat real-time logs

## 🎯 Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Halaman QR Code dengan UI |
| `/qr-image` | GET | QR Code image (PNG) |
| `/download-qr` | GET | Download QR Code |
| `/health` | GET | Health check status |

## 🔧 Troubleshooting

### QR Code tidak muncul?

**Cek logs:**
```bash
# Di Coolify dashboard, lihat logs
```

**Kemungkinan masalah:**
1. Chromium belum terinstall → Dockerfile sudah include dependencies
2. Port tidak expose → Pastikan PORT=3000 di env vars
3. Health check gagal → Cek endpoint `/health`

### Bot tidak connect?

1. **QR Code expired** → Refresh halaman untuk QR baru
2. **WhatsApp sudah login** → Logout dari device lain dulu
3. **Session conflict** → Hapus folder `_IGNORE_bot-wa-saya`

### Download QR gagal?

1. **QR belum ready** → Tunggu beberapa detik
2. **Browser block download** → Allow download di browser settings
3. **CORS error** → Sudah dihandle di server

## 📦 Persistent Storage (Optional)

Untuk menyimpan session WhatsApp agar tidak perlu scan ulang:

**Di Coolify:**
1. Go to **Storage** tab
2. Add volume:
   - **Source:** `/app/_IGNORE_bot-wa-saya`
   - **Destination:** Persistent volume
3. Redeploy

Dengan ini, session WhatsApp akan tersimpan dan tidak perlu scan QR lagi setelah restart.

## 🔐 Security Tips

1. **Jangan share QR Code** ke orang lain
2. **Set environment variables** untuk sensitive data
3. **Enable HTTPS** di Coolify (default enabled)
4. **Limit access** dengan Coolify authentication jika perlu

## 🚀 Auto-Deploy

Setup auto-deploy dari Git:

1. Di Coolify, enable **"Auto Deploy"**
2. Setiap push ke branch `main` akan auto-deploy
3. Webhook akan trigger build otomatis

## 📊 Resource Requirements

**Minimum:**
- CPU: 0.5 core
- RAM: 512 MB
- Storage: 1 GB

**Recommended:**
- CPU: 1 core
- RAM: 1 GB
- Storage: 2 GB

## 💡 Tips

1. **QR Code auto-refresh** setiap 2 detik di browser
2. **Download QR** untuk backup atau share ke tim
3. **Health check** untuk monitoring uptime
4. **Logs** untuk debugging issues
5. **Persistent storage** untuk session WhatsApp

## 📞 Support

Jika ada masalah:
1. Cek logs di Coolify dashboard
2. Test health endpoint: `/health`
3. Restart container jika perlu
4. Redeploy jika masih error

---

**Happy Deploying! 🎉**

Bot akan running 24/7 di Coolify dan QR Code bisa didownload kapan saja!
