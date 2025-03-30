# Travel Fraud Analyst at the New York City Taxi and Limousine Commission (NYC TLC)
---
## 1. Project Overview 📌
NYC Taxi and Limousine Commission (NYC TLC) mengawasi layanan transportasi berlisensi di New York City untuk memastikan keselamatan, keadilan, dan kepatuhan. Salah satu tantangan yang dihadapi adalah potensi kecurangan dalam perjalanan taksi yang dapat merugikan penyedia layanan maupun pelanggan. Proyek ini bertujuan untuk mendeteksi potensi kecurangan dalam data perjalanan taksi NYC TLC dengan mengidentifikasi anomali pada jarak, durasi, dan tarif perjalanan, serta pola pickup dan drop-off. 

Analisis ini bertujuan mendeteksi anomali pada data perjalanan taksi yang berpotensi mencerminkan aktivitas mencurigakan atau kecurangan, dengan fokus pada:
1. Deteksi Anomali Perjalanan:
    * Jarak perjalanan yang tidak masuk akal.
    * Durasi perjalanan yang terlalu lama untuk jarak pendek atau terlalu cepat untuk jarak jauh.
    * Tarif perjalanan yang tidak sesuai dengan jarak atau waktu tempuh.
1. Deteksi Anomali Pola Pickup dan Dropoff:
    * Identifikasi lokasi yang sering terjadi anomali.
    * Analisis waktu tertentu yang memiliki pola perjalanan mencurigakan.

## 2. Data Sources 🛢
* [New York City Taxi and Limousine Commission (NYC TLC) Trip Record](data/NYC%20TLC%20Trip%20Record.csv) -
Dataset ini memuat berbagai informasi penting seperti waktu dan lokasi penjemputan serta pengantaran, jumlah penumpang, jarak perjalanan, tarif, metode pembayaran, serta status perjalanan dari tahun 2009 sampai dengan 2023, yang dapat diunduh [disini](https://drive.google.com/drive/folders/1NYHIL-RgVPW-HONz4pdzlcbIChF-c37N).

* [Taxi Zones](data/taxi-zone-lookup.csv) - Dataset ini merupakan data pelengkap untuk mengubah dan menambahkan Borough dan Zone yang sesuai dengan dataset utama berdasarkan LocationID, yang dapat diunduh [disini](https://www.nyc.gov/site/tlc/about/tlc-trip-record-data.page)

## 3. Technologies Used 💻
* Programming Language: Python
* Visualization: Matplotlib, Seaborn, Plotly
* Interactive Dashboard: Tableau
* Version Control: Git
* Others: Jupyter Notebook

## 4. Project Structure 🧬
```
├── README.md         
|
├── data
│   ├── NYC TLC Trip Record.csv      <- Dataset mentah yang akan diolah.
|   |── taxi-zone-lookup.csv         <- Dataset untuk mencari zona taxi dengan locationID
|   |── taxi_zones_tableau           <- Folder yang berisi data zone untuk map tableau
│   └── Clean NYC TLC.csv            <- Dataset yang sudah bersih.
│
├── notebook          
│   └── New York City TLC Trip.ipynb <- File utama untuk menjalankan kode.
│
├── reports            
|   ├── NYC TLC.pptx                 <- PowerPoint untuk presentasi
│   └── NYC TLC Dashboard.twbx       <- Dashboard Tableau untuk visualiasi interaktif
│
└── requirements.txt                 <- Library yang dibutuhkan untuk menjalankan kode

```

## 5. Summary of Finding 📝

### 5.1 Business Insight
**A. Permintaan Taksi**
* Manhattan menjadi pusat aktivitas taksi tertinggi dengan 37.474 perjalanan, jauh melampaui borough lainnya. Hal ini wajar karena Manhattan adalah pusat bisnis, pariwisata, dan hiburan di NYC. Aktivitas tinggi ini juga didorong oleh keberadaan destinasi populer seperti Times Square, Wall Street, dan berbagai pusat perkantoran.
* Queens menempati posisi kedua dengan 17.261 perjalanan, yang kemungkinan besar dipengaruhi oleh kedekatannya dengan dua bandara utama, yakni JFK dan LaGuardia. Ini menandakan Queens sebagai wilayah transit utama bagi pendatang dan pelancong.
* Brooklyn memiliki 8.014 perjalanan, mencerminkan aktivitas yang cukup stabil, meski tidak setinggi Manhattan atau Queens.
* Bronx, Staten Island, dan wilayah dengan label "Unknown" memiliki jumlah perjalanan yang jauh lebih sedikit. Aktivitas terbatas ini mencerminkan karakteristik wilayah yang lebih bersifat residensial atau kurang padat.
* EWR (Newark Airport) mencatat hanya 1 perjalanan, menunjukkan minimnya aktivitas taksi yang berhubungan dengan bandara tersebut, kemungkinan karena penumpang lebih memilih moda transportasi lain seperti kereta atau layanan rideshare.

**B. Zona dengan Anomali Tinggi**
* Borough Queens mencatat jumlah perjalanan mencurigakan tertinggi senilai 1317, meskipun total perjalanan lebih rendah dari Manhattan.
* East Harlem North (Manhattan) mencatat jumlah anomali tertinggi dalam kategori zone dengan 234 kasus (0,37% dari seluruh perjalanan). Sebagai wilayah dengan aktivitas sosial yang beragam, East Harlem North berpotensi memiliki risiko lebih tinggi terkait aktivitas mencurigakan.
* Astoria (Queens) berada di posisi kedua dengan 187 kasus (0,29%). Astoria merupakan wilayah yang ramai dengan restoran, kafe, dan area komersial, yang mungkin berkontribusi pada lonjakan anomali.

**C. Polanya Berdasarkan Waktu**
* Hari dengan Anomali Tertinggi:
    * Anomali cenderung lebih banyak terjadi pada Selasa (575 kasus), diikuti oleh Rabu (520 kasus) dan Senin (511 kasus). Hal ini kemungkinan besar disebabkan oleh aktivitas yang lebih tinggi pada hari kerja, terutama di awal minggu.
    * Aktivitas anomali menurun secara bertahap dari Kamis hingga Minggu, dengan jumlah terendah pada Sabtu (421 kasus).
    * Pola ini menyoroti bahwa potensi aktivitas mencurigakan lebih berhubungan dengan hari kerja daripada akhir pekan.

* Waktu dengan Anomali Tertinggi:
    * Anomali mencapai puncaknya pada pukul 14:00 - 15:00 dan tetap tinggi sepanjang pukul 11:00 - 16:00. Periode ini bertepatan dengan jam makan siang dan transisi shift kerja, yang mungkin meningkatkan potensi perilaku mencurigakan di tengah lonjakan aktivitas.
    * Anomali cenderung menurun secara signifikan setelah pukul 20:00, mencerminkan berkurangnya mobilitas warga pada malam hari.
    * Dini hari (pukul 00:00 - 06:00) mencatat jumlah anomali terendah, menandakan minimnya aktivitas taksi pada periode ini.

### 5.2 Actionable Recommendation
**A. Optimalisasi Penempatan Taksi**
* **Penyesuaian Armada di Manhattan:** <br>
Dengan jumlah perjalanan tertinggi, Manhattan memerlukan distribusi armada yang optimal, terutama di kawasan padat seperti Times Square, Wall Street, dan pusat bisnis lainnya. Ini merupakan sebuah peluang untuk dapat mempertimbangkan penempatan kendaraan tambahan selama jam sibuk (11:00 - 16:00).
* **Optimalisasi Layanan di Queens** <br>
Karena tingginya jumlah perjalanan terkait bandara di Queens, kerja sama dengan pihak bandara untuk menyediakan jalur taksi khusus atau pos taksi di lokasi strategis dapat meningkatkan layanan.
* **Strategi Promosi di Brooklyn dan Area Sepi** <br>
Untuk meningkatkan permintaan di Brooklyn dan area dengan aktivitas lebih rendah, mungkin dapat mengadakan penawaran diskon, layanan antar-jemput berbasis reservasi, atau kerja sama dengan layanan pariwisata.
* **Peninjauan Layanan ke EWR (Newark Airport)** <br>
Dengan minimnya aktivitas taksi ke EWR, disarankan untuk mengevaluasi tarif, rute, dan promosi khusus untuk menarik penumpang.

**B. Mitigasi Aktivitas Anomali**
* **Deteksi dan Pencegahan Manipulasi Perjalanan** <br>
Mengingat potensi pencatatan perjalanan palsu dan manipulasi data GPS , solusinya:
    - Memperbarui dan maintenance berkala pada perangkat pencatat perjalanan seperti taximeter agar dapat mengurangi kesalahan pencatatan perjalanan dan kesalahan pengiriman data.
    - Memperbarui Perangkat Lunak GPS untuk meningkatkan akurasi dan mendeteksi lokasi yang tidak realistis atau perjalanan yang tidak sesuai pola wajar.
* **Penambahan Pengawasan di Zona Rawan** <br>
Karena East Harlem North (Manhattan) dan Astoria (Queens) mencatat banyak anomali, disarankan untuk:
    - Memasang CCTV dan Sensor Pemantauan di area dengan lonjakan anomali.
    - Membentuk Tim Inspeksi Lapangan untuk mengecek potensi manipulasi data oleh pengemudi.

**C. Edukasi**
* **Sosialisasi kepada Pengemudi tentang Kebijakan dan Etika** <br>
Program ini bertujuan untuk meningkatkan kesadaran pengemudi akan konsekuensi hukum manipulasi data serta pentingnya kejujuran dalam pencatatan perjalanan.
* **Edukasi Penumpang** <br>
Kampanye informasi untuk penumpang agar mereka memahami cara melaporkan jika menemukan perjalanan yang mencurigakan atau tidak sesuai.

## 6. How to use 🚀
### A. Requiments:
* Python version 3.13 or later
* Tableau Desktop or Public
### B. Installation:
```
git clone https://github.com/Meowstronot/New-York-City-TLC-Trip-Analyst
cd New-York-City-TLC-Trip-Analyst
pip install -r requirements.txt 
```
### C. Open Notebook
* Buka file `New York City TLC Trip.ipynb` yang pada folder notebok
* Eksekusi setiap sel kode untuk menjalankan analisis.
* Buka file `NYC TLC Dashboard.twbx` pada folder report untuk membuka Dasboard Tableau

## 7. Contact 📩
* **Nama**: Muhammad Khisanul Fakhrudin Akbar
* **Email** : shinaruikhisan@gmail.com
* **Linkedin** : https://www.linkedin.com/in/muhammad-khisanul-fakhrudin-akbar/