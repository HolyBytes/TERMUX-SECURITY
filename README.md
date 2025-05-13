# **Termux Security Toolkit**  

**🔒 Toolkit Keamanan Termux untuk Pemula & Advanced**  
*"Security is a journey, not a destination."*  

---

## **📌 Apa Itu Termux Security Toolkit?**  
Tools ini adalah **kumpulan script otomatis** buat ngecek keamanan, analisis jaringan, dan eksploitasi dasar langsung dari Termux. Dibuat biar kamu gak perlu install banyak tools manual—tinggal jalanin script, pilih fitur, dan langsung bisa dipake!  

🔥 **Cocok buat:**  
✔ **Pemula** yang baru belajar cybersecurity  
✔ **Advanced users** yang butuh tools cepat di Termux  
✔ **Bug hunters** buat tes kerentanan sederhana  
✔ **CTF players** (HackTheBox, TryHackMe, dll)  

---

## **🌟 Fitur & Kegunaan**  

### **🔍 OSINT & Reconnaissance**  
| Tools | Fungsi | Kelebihan | Kekurangan |
|-------|--------|-----------|------------|
| **Have I Been Pwned** | Cek kebocoran email/password | Cepat & akurat | Gak bisa scan massal |
| **SpiderFoot** | Otomatis ngumpulin info target (IP, domain, dll) | Support banyak sumber | Butuh API key buat fitur premium |
| **Shodan** | Cari device IoT, server, kamera | Database besar | Harus punya API key |

### **🛡️ Vulnerability Testing**  
| Tools | Fungsi | Kelebihan | Kekurangan |
|-------|--------|-----------|------------|
| **XSS Tools** | Cari celah XSS & generate payload | Bisa pake buat CTF | Gak selalu akurat |
| **Path Traversal** | Tes LFI (Local File Inclusion) | Bisa akses file sistem | Target harus vulnerable |
| **VirusTotal** | Scan file pake 70+ antivirus | Deteksi malware akurat | File besar lama diproses |

### **⚔️ Pentesting & Exploitation**  
| Tools | Fungsi | Kelebihan | Kekurangan |
|-------|--------|-----------|------------|
| **HackTheBox Helper** | Bantu solve challenge HTB | Praktis buat latihan | Butuh koneksi stabil |
| **PayloadsAllTheThings** | Kumpulan payload (SQLi, RCE, dll) | Lengkap! | Harus paham cara pake |
| **DDoS Tools** (Slowloris, GoldenEye) | Tes ketahanan server | Efektif buat edukasi | **Jangan disalahgunakan!** |

### **🛠️ Utilities**  
| Tools | Fungsi | Kelebihan | Kekurangan |
|-------|--------|-----------|------------|
| **Wireshark (TShark)** | Analisis jaringan | Bisa baca traffic | Butuh root buat fitur lengkap |
| **Auto-Update** | Update toolkit langsung dari script | Gak perlu install ulang | Kadang error kalo koneksi jelek |

---

## **🚀 Install & Setup**  
**⏳ Waktu install:** ~1-5 menit (tergantung koneksi)  

1. **Buka Termux**, lalu ketik:  
   ```bash
   pkg update -y && pkg upgrade -y
   pkg install git python curl -y
   git clone https://github.com/HolyBytes/TERMUX-SECURITY.git
   cd TERMUX-SECURITY
   chmod +x termux-toolkit.sh
   ./termux-toolkit.sh
   ```  
2. **Pilih tools** yang mau dipake  
3. **Ikuti petunjuk** di layar  

🔹 **Tips:** Simpan API key (Shodan, VirusTotal) di:  
`/data/data/com.termux/files/home/.config/termux-toolkit/api_keys.conf`  

---

## **⚠️ Apa yang Bisa & Gak Bisa Diubah?**  
🔧 Bagian yang Bisa Diedit
Berikut bagian-bagian script yang aman untuk dimodifikasi:

1. Tampilan & Warna (UI)
bash
# Warna teks - bisa diganti kode warnanya
RED='\033[1;31m'
GREEN='\033[1;32m'
YELLOW='\033[1;33m'
BLUE='\033[1;34m'
MAGENTA='\033[1;35m'
CYAN='\033[1;36m'
WHITE='\033[1;37m'
NC='\033[0m'  # No Color
2. Menu & Deskripsi Fitur
bash
# Contoh: Modifikasi menu utama
printf "| ${CYAN}%-4s${GREEN} | ${YELLOW}%-25s${GREEN} | ${MAGENTA}%-35s${GREEN} |\n" "1" "Have I Been Pwned" "Check account breaches"
3. Konfigurasi Path
bash
# Lokasi penyimpanan log dan config - bisa diubah
CONFIG_DIR="$HOME/.config/termux-toolkit"  # Ganti path ini jika perlu
LOG_FILE="$CONFIG_DIR/toolkit.log"
4. Menambahkan Tools Baru
bash
# Contoh menambahkan fungsi baru
my_new_tool() {
    echo -e "${GREEN}[*] Installing My New Tool...${NC}"
    pkg install some-package -y
    echo -e "${GREEN}[+] Installed! Usage: mytool <target>${NC}"
}
🚫 Bagian yang Tidak Boleh Diedit
1. Struktur Utama Script
bash
#!/bin/bash
# Jangan hapus shebang (#!) di awal file

init_toolkit() {
    # Fungsi init harus tetap ada
    check_requirements
}
2. Sistem Auto-Update
bash
update_toolkit() {
    # Jangan modifikasi logika update
    latest_version=$(curl -s "$REPO_URL/raw/main/termux-toolkit.sh" | grep "TOOL_VERSION=")
    # ...
}
3. Nama File Konfigurasi
bash
API_KEYS_FILE="$CONFIG_DIR/api_keys.conf"  # Jangan ganti nama file ini
⚠️ Dampak Jika Asal Edit
Yang Diedit	Dampak Positif	Dampak Negatif
Warna UI	Tampilan lebih personal	Error jika kode warna salah
Path Config	Bisa simpan di lokasi lain	Tools lain gak nemu config
Menambah Fitur	Fungsi bertambah	Bikin conflict jika salah coding
Struktur Utama	-	Script bisa error total
Sistem Update	-	Gak bisa update otomatis
💡 Tips Modifikasi Aman
Backup script sebelum edit:

bash
cp termux-toolkit.sh termux-toolkit.backup
Test perubahan sedikit demi sedikit

Jangan hapus fungsi-fungsi kritis (init_toolkit, check_requirements)

Kalau mau nambah tools, buat fungsi baru jangan edit yang sudah ada

🔍 Contoh Edit yang Disarankan
Menambahkan Fitur Baru:
bash
# Tambahkan di bagian fungsi
my_custom_scanner() {
    echo -e "${CYAN}[*] Running Custom Scanner${NC}"
    read -p "Enter target IP: " ip
    ping -c 4 $ip
}

# Tambahkan pilihan menu (di display_features)
printf "| ${CYAN}%-4s${GREEN} | ${YELLOW}%-25s${GREEN} | ${MAGENTA}%-35s${GREEN} |\n" "13" "Custom Scanner" "My Ping Scanner"
Mengubah Warna:
bash
# Ganti warna merah jadi pink
RED='\033[1;38;5;206m'  # Warna pink
Dengan panduan ini, kamu bisa kostumisasi script tanpa takut merusak fungsi utamanya! 🛠️

---

## **💡 Manfaat & Batasan**  
✔ **Kelebihan:**  
- Gak perlu install banyak tools manual  
- Bisa dipake buat belajar cybersecurity  
- Update otomatis (tinggal pilih menu)  

✖ **Kekurangan:**  
- Beberapa tools butuh API key (Shodan, VirusTotal)  
- Gak bisa replace tools khusus kayak Metasploit  
- Koneksi lemot bikin proses lama  

---

## **📌 Penting!**  
❌ **Jangan dipake buat:**  
- Hacking ilegal  
- DDoS website tanpa izin  
- Nyebarin malware  

✅ **Pake yang bener:**  
- Tes keamanan website sendiri  
- Belajar cybersecurity  
- Bug hunting (dengan izin)  

---

## **💌 Support & Donasi**  
Kalo tools ini berguna, bantu **dukungan** biar terus dikembangkan:  
🔗 **Saweria:** [https://saweria.co/HolyBytes](https://saweria.co/HolyBytes)  

Bisa juga **kontribusi** dengan:  
1. **Lapor bug** (buat Issue di GitHub)  
2. **Request fitur** baru  
3. **Share** ke temen-temen  

🔎 **Link GitHub:** [HolyBytes/TERMUX-SECURITY](https://github.com/HolyBytes/TERMUX-SECURITY)  

---

**🔥 Happy Ethical Hacking!**  
*"Don't be a skid, be a pro."* 🚀
