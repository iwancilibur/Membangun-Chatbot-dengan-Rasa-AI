# Membangun-Chatbot-dengan-Rasa-AI
---
![Image](https://github.com/user-attachments/assets/a6489aed-9dd6-42a4-ac00-7362f8110d52)

**Rasa AI** adalah sebuah platform *open-source* untuk membangun asisten virtual dan chatbot canggih yang dapat memahami dan merespons percakapan manusia secara alami. Rasa memungkinkan pengembang untuk membuat sistem *conversational AI* yang dapat dijalankan secara *on-premise* (di server sendiri) tanpa bergantung pada layanan cloud eksternal.

### **Komponen Utama Rasa AI:**
1. **Rasa NLU (*Natural Language Understanding*)**  
   - Bertugas memahami maksud pengguna dari teks yang dikirim.  
   - Menggunakan *machine learning* untuk mengekstrak *intent* (tujuan) dan *entities* (informasi penting) dari pesan.  
   - Contoh: Jika pengguna menulis *"Booking tiket ke Jakarta besok"*, Rasa NLU dapat mengenali:  
     - **Intent**: `book_flight`  
     - **Entities**:  
       - `destination: Jakarta`  
       - `date: besok`  

2. **Rasa Core**  
   - Mengelola alur percakapan (*dialogue management*).  
   - Memutuskan tindakan selanjutnya berdasarkan percakapan yang terjadi.  
   - Menggunakan *machine learning* berbasis *stories* (contoh interaksi) untuk memprediksi respons terbaik.  

### **Keunggulan Rasa AI:**
✅ **Open-source** – Dapat digunakan dan dimodifikasi secara gratis.  
✅ **Privasi & Kontrol Data** – Data tetap di infrastruktur Anda sendiri.  
✅ **Fleksibel** – Dapat diintegrasikan dengan *backend* seperti Slack, WhatsApp, atau website.  
✅ **Mendukung Bahasa Alami** – Bisa dilatih untuk berbagai bahasa, termasuk Bahasa Indonesia.  

### **Contoh Penggunaan Rasa AI:**
- **Customer Support:** Chatbot otomatis untuk menjawab pertanyaan pelanggan.  
- **Asisten Pribadi:** Membantu jadwal meeting, reminder, atau rekomendasi.  
- **E-commerce:** Memandu proses pemesanan produk.  

### **Cara Kerja Rasa AI:**
1. Pengguna mengirim pesan (*user input*).  
2. **Rasa NLU** menganalisis maksud pesan.  
3. **Rasa Core** memilih respons terbaik berdasarkan konteks percakapan.  
4. Sistem mengirim balasan atau menjalankan aksi (misalnya, mencari data di database).  

Rasa cocok bagi perusahaan atau pengembang yang ingin membuat chatbot cerdas dengan kontrol penuh atas data dan logika percakapan.  

# **Mari kita buat chatbot sederhana bersama!** 🚀
![Image](https://github.com/user-attachments/assets/3721df27-6c17-40eb-ac1c-29a0aab0b1fb)

 Saya akan memandu Anda langkah demi langkah dengan contoh praktis dalam Bahasa Indonesia.  
---

### **Langkah 1: Persiapan**  
Pastikan Anda sudah:  
1. Menginstal Python (versi 3.7, 3.8, atau 3.9).  
2. Menjalankan perintah instalasi Rasa (jika belum):  
   ```bash
   pip install rasa
   ```

---

### **Langkah 2: Inisialisasi Proyek**  
1. Buka terminal/CMD, lalu buat folder proyek baru:  
   ```bash
   mkdir chatbot-indonesia
   cd chatbot-indonesia
   ```
2. Jalankan perintah inisialisasi:  
   ```bash
   rasa init --no-prompt
   ```  
   *(Flag `--no-prompt` akan melewati pertanyaan konfigurasi awal.)*  

   Ini akan membuat struktur file otomatis.  

---

### **Langkah 3: Edit File untuk Chatbot Bahasa Indonesia**  
#### **1. Tambahkan Contoh Intent**  
Buka file `data/nlu.yml`, ganti kontennya dengan:  
```yaml
version: "3.1"

nlu:
- intent: sapaan
  examples: |
    - hai
    - halo
    - selamat pagi
    - apa kabar?

- intent: tanya_produk
  examples: |
    - produk apa yang kamu jual?
    - saya mau lihat menu
    - ada promo hari ini?
    - bisa lihat daftar produk?

- intent: konfirmasi_pesanan
  examples: |
    - saya sudah transfer
    - pesanan saya sudah dibayar
    - konfirmasi pembayaran
```

#### **2. Definisikan Respons**  
Buka `domain.yml`, tambahkan:  
```yaml
responses:
  utter_sapaan:
    - text: "Halo! Senang bertemu dengan Anda. 😊 Ada yang bisa saya bantu?"

  utter_tanya_produk:
    - text: "Kami menjual: \n- Laptop \n- Smartphone \n- Aksesori Elektronik. \nLihat katalog kami di [sini](https://contoh.com)!"

  utter_konfirmasi:
    - text: "Terima kasih! Tim kami akan memverifikasi pembayaran Anda dalam 1x24 jam."
```

#### **3. Buat Alur Percakapan**  
Edit `data/stories.yml`:  
```yaml
version: "3.1"

stories:
- story: jalur sapaan
  steps:
    - intent: sapaan
    - action: utter_sapaan

- story: jalur tanya produk
  steps:
    - intent: tanya_produk
    - action: utter_tanya_produk

- story: jalur konfirmasi
  steps:
    - intent: konfirmasi_pesanan
    - action: utter_konfirmasi
```

---

### **Langkah 4: Latih Model**  
Jalankan pelatihan:  
```bash
rasa train
```  
Anda akan melihat output seperti:  
```
Your Rasa model is trained and saved at 'models/20240525-123456.tar.gz'.
```

---

### **Langkah 5: Uji Chatbot**  
#### **1. Mode Interaktif**  
```bash
rasa shell
```  
Coba ketik:  
- `"Halo"` → Bot merespons dengan sapaan.  
- `"Apa produk yang dijual?"` → Bot menampilkan daftar produk.  

#### **2. Simulasi di Browser**  
Jalankan server lokal:  
```bash
rasa run --enable-api --cors "*"
```  
Buka **http://localhost:5005** di browser atau gunakan Postman untuk menguji API.  

---

### **Contoh Percakapan**  
```
User: Hai  
Bot: Halo! Senang bertemu dengan Anda. 😊 Ada yang bisa saya bantu?  
User: Produk apa yang kamu jual?  
Bot: Kami menjual:  
     - Laptop  
     - Smartphone  
     - Aksesori Elektronik.  
     Lihat katalog kami di [sini](https://contoh.com)!  
User: Saya sudah transfer  
Bot: Terima kasih! Tim kami akan memverifikasi pembayaran Anda dalam 1x24 jam.
```

---

### **Tips Tambahan**  
🔹 **Tambahkan Lebih Banyak Data**: Semakin banyak contoh intent di `nlu.yml`, semakin pintar chatbot Anda.  
🔹 **Gunakan Entities**: Misalnya, ekstrak `"Saya mau pesan [nasi goreng](makanan)"`.  
🔹 **Kustomisasi Aksi**: Buat file `actions.py` untuk koneksi database/API.  

---

**Selanjutnya akan saya buatkan ke tahap berikutnya?**:  
- Menambahkan fitur [form](https://rasa.com/docs/rasa/forms) untuk isi data?  
- Integrasi dengan WhatsApp?  

