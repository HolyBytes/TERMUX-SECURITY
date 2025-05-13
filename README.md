# **Termux Security Toolkit**

**🔒 Bantuan Keamanan Termux untuk Pemula & Pengguna Mahir**  
*"Keamanan itu perjalanan, bukan tujuan akhir."*

---

## **📱 Kenalan dengan Termux Security Toolkit**

Halo teman-teman! Termux Security Toolkit ini adalah **kumpulan script otomatis** yang bisa membantu kamu melakukan pengecekan keamanan, analisis jaringan, dan pembelajaran dasar keamanan siber langsung dari aplikasi Termux di HP kamu. 

Toolkit ini dibuat supaya kamu nggak perlu repot-repot install banyak tools satu per satu. Tinggal jalankan scriptnya, pilih fitur yang kamu mau, dan langsung bisa dipakai!

### **✨ Cocok untuk:**
- Kamu yang baru mulai belajar keamanan siber
- Pengguna yang sudah paham dan butuh tools praktis di Termux
- Teman-teman yang suka mencari bug (bug hunter)
- Peserta CTF (Capture The Flag) seperti HackTheBox, TryHackMe, dll

---

## **🌟 Fitur & Kegunaannya**

### **🔍 OSINT & Pengumpulan Informasi**

| Tools | Apa Fungsinya | Kelebihannya | Kekurangannya |
|-------|---------------|--------------|---------------|
| **Have I Been Pwned** | Mengecek apakah email/password kamu pernah bocor | Hasilnya cepat dan akurat | Tidak bisa scan banyak email sekaligus |
| **SpiderFoot** | Mengumpulkan informasi target secara otomatis (IP, domain, dll) | Mendukung banyak sumber data | Beberapa fitur butuh API key |
| **Shodan** | Mencari perangkat IoT, server, kamera yang terhubung internet | Database sangat besar | Perlu API key untuk hasil maksimal |

### **🛡️ Pengujian Kerentanan**

| Tools | Apa Fungsinya | Kelebihannya | Kekurangannya |
|-------|---------------|--------------|---------------|
| **XSS Tools** | Mencari celah XSS & membuat payload | Sangat berguna untuk latihan CTF | Tidak selalu akurat di semua situasi |
| **Path Traversal** | Menguji kerentanan LFI (Local File Inclusion) | Bisa mengakses file sistem jika target rentan | Target harus memiliki kerentanan ini |
| **VirusTotal** | Scan file dengan 70+ antivirus | Deteksi malware sangat akurat | File besar membutuhkan waktu lama |

### **⚔️ Pengujian Penetrasi & Eksploitasi**

| Tools | Apa Fungsinya | Kelebihannya | Kekurangannya |
|-------|---------------|--------------|---------------|
| **HackTheBox Helper** | Membantu menyelesaikan tantangan HTB | Praktis untuk latihan | Butuh koneksi internet stabil |
| **PayloadsAllTheThings** | Kumpulan payload (SQLi, RCE, dll) | Sangat lengkap | Perlu pemahaman cara penggunaan |
| **DDoS Tools** (Slowloris, GoldenEye) | Menguji ketahanan server | Efektif untuk pembelajaran | **Gunakan hanya untuk tujuan edukasi ya!** |

### **🛠️ Alat Bantu Lainnya**

| Tools | Apa Fungsinya | Kelebihannya | Kekurangannya |
|-------|---------------|--------------|---------------|
| **Wireshark (TShark)** | Menganalisis lalu lintas jaringan | Bisa membaca semua traffic | Butuh akses root untuk fitur lengkap |
| **Auto-Update** | Update toolkit secara otomatis | Tidak perlu install ulang | Kadang error jika koneksi lambat |

---

## **🚀 Cara Install & Persiapan**

**⏳ Waktu install:** Sekitar 1-5 menit (tergantung kecepatan internet kamu)

1. **Buka aplikasi Termux**, lalu ketik perintah ini:
   ```bash
   pkg update -y && pkg upgrade -y
   pkg install git python curl -y
   git clone https://github.com/HolyBytes/TERMUX-SECURITY.git
   cd TERMUX-SECURITY
   chmod +x termux-toolkit.sh
   ./termux-toolkit.sh
   ```
2. **Pilih tools** yang ingin kamu gunakan
3. **Ikuti petunjuk** yang muncul di layar

💡 **Tips:** Simpan API key (Shodan, VirusTotal) di lokasi berikut:
`/data/data/com.termux/files/home/.config/termux-toolkit/api_keys.conf`

---

## **⚠️ Bagian yang Boleh dan Tidak Boleh Diubah**

### **🔧 Bagian yang Boleh Diedit**

Kamu bisa mengubah bagian-bagian script berikut dengan aman:

1. **Tampilan & Warna (UI)**
   ```bash
   # Warna teks - bisa diganti kode warnanya sesuai selera
   RED='\033[1;31m'
   GREEN='\033[1;32m'
   YELLOW='\033[1;33m'
   BLUE='\033[1;34m'
   MAGENTA='\033[1;35m'
   CYAN='\033[1;36m'
   WHITE='\033[1;37m'
   NC='\033[0m'  # No Color
   ```

2. **Menu & Deskripsi Fitur**
   ```bash
   # Contoh: Modifikasi menu utama
   printf "| ${CYAN}%-4s${GREEN} | ${YELLOW}%-25s${GREEN} | ${MAGENTA}%-35s${GREEN} |\n" "1" "Have I Been Pwned" "Check account breaches"
   ```

3. **Lokasi Penyimpanan**
   ```bash
   # Lokasi penyimpanan log dan config - bisa diubah sesuai kebutuhan
   CONFIG_DIR="$HOME/.config/termux-toolkit"  # Ganti path ini jika perlu
   LOG_FILE="$CONFIG_DIR/toolkit.log"
   ```

4. **Menambahkan Tools Baru**
   ```bash
   # Contoh menambahkan fitur baru
   my_new_tool() {
       echo -e "${GREEN}[*] Sedang memasang Tool Baru...${NC}"
       pkg install some-package -y
       echo -e "${GREEN}[+] Selesai dipasang! Cara pakai: mytool <target>${NC}"
   }
   ```

### **🚫 Bagian yang Jangan Diedit**

1. **Struktur Utama Script**
   ```bash
   #!/bin/bash
   # Jangan hapus shebang (#!) di awal file

   init_toolkit() {
       # Fungsi init harus tetap ada
       check_requirements
   }
   ```

2. **Sistem Auto-Update**
   ```bash
   update_toolkit() {
       # Jangan diubah ya, agar update tetap lancar
       latest_version=$(curl -s "$REPO_URL/raw/main/termux-toolkit.sh" | grep "TOOL_VERSION=")
       # ...
   }
   ```

3. **Nama File Konfigurasi**
   ```bash
   API_KEYS_FILE="$CONFIG_DIR/api_keys.conf"  # Jangan ganti nama file ini
   ```

### **⚠️ Dampak Jika Asal Mengubah**

| Yang Diedit | Dampak Positif | Dampak Negatif |
|-------------|----------------|----------------|
| Warna UI | Tampilan jadi lebih personal | Error jika kode warna salah |
| Path Config | Bisa simpan di lokasi yang kamu inginkan | Tools lain mungkin tidak menemukan config |
| Menambah Fitur | Fungsi toolkit bertambah | Bisa menyebabkan konflik jika coding kurang tepat |
| Struktur Utama | - | Script bisa error total |
| Sistem Update | - | Tidak bisa update otomatis lagi |

### **💡 Tips Mengubah dengan Aman**

- **Backup dulu** sebelum mengubah:
  ```bash
  cp termux-toolkit.sh termux-toolkit.backup
  ```
- Uji perubahan sedikit demi sedikit
- Jangan hapus fungsi-fungsi penting (init_toolkit, check_requirements)
- Kalau ingin menambah tools, buat fungsi baru tanpa mengubah yang sudah ada

### **🔍 Contoh Perubahan yang Disarankan**

**Menambahkan Fitur Baru:**
```bash
# Tambahkan di bagian fungsi
scan_jaringan_saya() {
    echo -e "${CYAN}[*] Menjalankan Scanner Jaringan${NC}"
    read -p "Masukkan IP target: " ip
    ping -c 4 $ip
}

# Tambahkan pilihan menu (di display_features)
printf "| ${CYAN}%-4s${GREEN} | ${YELLOW}%-25s${GREEN} | ${MAGENTA}%-35s${GREEN} |\n" "13" "Scanner Jaringan" "Pemindai Jaringan Sederhana"
```

**Mengubah Warna:**
```bash
# Ganti warna merah jadi pink
RED='\033[1;38;5;206m'  # Warna pink
```

Dengan panduan ini, kamu bisa menyesuaikan script sesuai kebutuhanmu tanpa merusak fungsi utamanya! 🛠️

---

## **💡 Kelebihan & Keterbatasan**

### **✨ Kelebihan:**
- Hemat waktu karena tidak perlu memasang banyak tools secara manual
- Sangat cocok untuk belajar keamanan siber dari dasar
- Bisa diperbarui otomatis (tinggal pilih menu update)
- Mudah digunakan bahkan untuk pemula

### **📝 Keterbatasan:**
- Beberapa tools membutuhkan API key (seperti Shodan, VirusTotal)
- Tidak bisa menggantikan tools khusus seperti Metasploit sepenuhnya
- Performa bisa lambat jika koneksi internet tidak stabil
- Beberapa fitur mungkin memerlukan akses root

---

## **📌 Pesan Penting!**

### **❌ Mohon jangan digunakan untuk:**
- Hacking yang melanggar hukum
- Menyerang website tanpa izin resmi
- Menyebarkan malware atau program berbahaya
- Mengakses sistem orang lain tanpa persetujuan

### **✅ Gunakan dengan bijak untuk:**
- Memeriksa keamanan website milik sendiri
- Belajar dan mengembangkan pengetahuan keamanan siber
- Bug hunting (dengan izin tertulis dari pemilik)
- Latihan CTF dan pengembangan skill keamanan

---

## **💌 Dukungan & Kontribusi**

Jika toolkit ini bermanfaat untuk kamu, kamu bisa mendukung pengembangannya melalui:

🔗 **Saweria:** [https://saweria.co/HolyBytes](https://saweria.co/HolyBytes)

Kamu juga bisa berkontribusi dengan cara:
1. **Melaporkan bug** (buat Issue di GitHub)
2. **Mengusulkan fitur** baru yang kamu butuhkan
3. **Membagikan** toolkit ini ke teman-teman yang mungkin membutuhkan

📱 **Temukan kami di GitHub:** [HolyBytes/TERMUX-SECURITY](https://github.com/HolyBytes/TERMUX-SECURITY)

---

**🔥 Selamat Belajar Keamanan Siber!**
*"Belajar dengan etika, praktik dengan tanggung jawab."* 🚀
