# Fraud Detection in NYC Taxi Services: A Data Science Approach Using TLC Trip Data (January 2023)
---
## 1. Project Overview 📌
NYC Taxi and Limousine Commission (NYC TLC) mengawasi layanan transportasi berlisensi di New York City untuk memastikan keselamatan, keadilan, dan kepatuhan. Salah satu tantangan yang dihadapi adalah potensi kecurangan dalam perjalanan taksi yang dapat merugikan penyedia layanan maupun pelanggan. Proyek ini bertujuan untuk mendeteksi potensi kecurangan dalam data perjalanan taksi NYC TLC dengan mengidentifikasi abnormalitas pada jarak, durasi, dan tarif perjalanan, serta pola pickup dan drop-off. 

Analisis ini bertujuan mendeteksi abnormalitas pada data perjalanan taksi yang berpotensi mencerminkan aktivitas mencurigakan atau kecurangan, dengan fokus pada:
1. Mendeteksi perjalanan mencurigakan
    * Abnormalitas pada jarak perjalanan, apakah ada perjalanan dengan jarak yang tidak masuk akal?
    * Abnormalitas pada durasi perjalanan, apakah ada perjalanan yang berlangsung terlalu lama untuk jarak pendek atau terlalu cepat untuk jarak jauh?
    * Abnormalitas pada tarif perjanalan, apakah ada perjalanan yang kategori tarifnya tidak sesuai?
1. Pola Abnormalitas
    * Mengetahui daerah mana saja yang sering terjadinya abnormalitas perjalanan
    * Mengetahui pada waktu-waktu tertentu yang sering terjadinya abnormalitas perjalanan

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
* Manhattan menjadi pusat aktivitas taksi tertinggi dengan 37.352 perjalanan, jauh melampaui borough lainnya. Hal ini wajar karena Manhattan adalah pusat bisnis, pariwisata, dan hiburan di NYC. Aktivitas tinggi ini juga didorong oleh keberadaan destinasi populer seperti Times Square, Wall Street, dan berbagai pusat perkantoran.
* Queens menempati posisi kedua dengan 17.018 perjalanan, yang kemungkinan besar dipengaruhi oleh kedekatannya dengan dua bandara utama, yakni JFK dan LaGuardia. Ini menandakan Queens sebagai wilayah transit utama bagi pendatang dan pelancong.
* Brooklyn memiliki 7.915 perjalanan, mencerminkan aktivitas yang cukup stabil, meski tidak setinggi Manhattan atau Queens.
* Bronx dan Staten Island memiliki volume perjalanan yang sangat rendah (885 dan hanya 12 perjalanan), mengindikasikan bahwa kedua borough ini memiliki tingkat penggunaan taksi yang sangat minim selama Januari 2023. Hal ini bisa disebabkan oleh preferensi moda transportasi lain, keterbatasan akses layanan, atau karakteristik wilayah yang berbeda.

**B. Lokasi dengan jumlah perjalanan mencurigakan Tinggi**
* Berdasarkan analisis per borough, Bronx dan Staten Island menunjukkan tingkat perjalanan mencurigakan tertinggi secara proporsional (masing-masing 36.27% dan 33.33%), meskipun jumlah perjalanan mencurigakannya rendah, sehingga perlu perhatian khusus. Brooklyn juga memiliki rasio yang cukup tinggi (9.70%) dibanding borough lain. Sebaliknya, Manhattan memiliki rasio terendah (1.90%) meskipun jumlah perjalanan mencurigakannya terbesar, menandakan potensi efektivitas sistem pengawasan. Sementara itu, Queens mencatat jumlah kasus terbanyak, namun dengan rasio yang relatif rendah (7.16%).
* Beberapa zona di Queens seperti Long Island City/Hunters Point (63.83%) dan Queensbridge/Ravenswood (56.49%) memiliki proporsi perjalanan mencurigakan yang sangat tinggi. Meski total perjalanan rendah, angka ini menjadi sinyal peringatan kuat akan potensi kecurangan yang terlokalisasi.

**C. Polanya Berdasarkan Waktu**
* **Awal Pekan dan Tengah Hari Jadi Periode Paling Rawan**
    * Perjalanan mencurigakan paling banyak terjadi pada hari kerja, khususnya Selasa, Rabu, dan Senin, dengan jumlah tertinggi tercatat pada rentang waktu 11:00–15:00. Ini menunjukkan bahwa awal minggu dan tengah hari adalah periode dengan risiko kecurangan tertinggi, kemungkinan karena tingginya aktivitas operasional dan volume perjalanan.

* **Akhir Pekan Lebih Stabil tapi Bukan Bebas Risiko**
    * Sabtu dan Minggu mencatat frekuensi perjalanan mencurigakan paling rendah, namun tetap signifikan. Hal ini menandakan bahwa meskipun volume perjalanan lebih rendah, potensi penyimpangan masih ada dan tidak boleh diabaikan.

* **Waktu-waktu Kritis di Pagi dan Sore Hari**
    * Selain puncak di tengah hari, terdapat lonjakan mencurigakan pada jam sibuk pagi (06:00–09:00), serta stabilisasi kembali pada sore hari (16:00–18:00), mencerminkan dinamika lalu lintas perkotaan dan perubahan intensitas pengawasan.


### 5.2 Actionable Recommendation
**A. Optimasi Layanan Berdasarkan Permintaan Taksi**
* **Penambahan Armada di Manhattan Selama Jam Sibuk:** <br>
Dengan dominasi perjalanan di Manhattan (37.352 perjalanan), disarankan untuk menambah armada taksi di zona sibuk seperti Times Square dan Wall Street, terutama pada rentang waktu 11:00–15:00, guna memenuhi lonjakan permintaan secara efisien.
* **Perkuat Infrastruktur Layanan di Queens** <br>
Queens sebagai hub bandara memerlukan kerja sama strategis dengan JFK dan LaGuardia. Penyediaan jalur prioritas dan pos taksi di titik kedatangan penting akan meningkatkan kenyamanan serta mengurangi waktu tunggu penumpang.
* **Dorongan Permintaan di Brooklyn & Area Rendah Aktivitas** <br>
Untuk meningkatkan permintaan di Brooklyn dan area dengan aktivitas lebih rendah, mungkin dapat mengadakan penawaran diskon, layanan untuk meningkatkan utilisasi taksi di Brooklyn dan borough seperti Bronx/Staten Island, perlu program promosi dinamis (misalnya: diskon, rute flat fare, atau layanan antar-jemput terjadwal). Fokuskan pada lokasi wisata lokal dan area pemukiman padat.

**B. Mitigasi Aktivitas Mencurigakan**
* **Penguatan Peran sebagai Regulator Data** <br>
Sebagai regulator, NYC TLC perlu memperkuat perannya dalam memastikan kualitas data dengan membentuk unit pengawasan data internal, menerapkan kebijakan data governance yang ketat, dan membangun sistem deteksi fraud untuk mengidentifikasi perjalanan mencurigakan secara akurat dan memastikan data yang dikumpulkan lebih valid.
* **Peningkatan Akurasi Data & Deteksi Dini Manipulasi** <br>
Bronx dan Staten Island meski volumenya rendah, memiliki rasio mencurigakan tinggi. Untuk itu:
    - Pembaruan sistem taximeter dan perangkat GPS wajib dilakukan secara berkala.
    - Memperbarui Perangkat Lunak GPS untuk meningkatkan akurasi dan mendeteksi lokasi yang tidak realistis atau perjalanan yang tidak sesuai pola wajar.
* **Fokus Pengawasan pada Zona dengan Proporsi Tinggi** <br>
Zona seperti Long Island City/Hunters Point dan Queensbridge/Ravenswood menunjukkan proporsi kecurigaan ekstrem (>50%). Disarankan:
    - Memasang CCTV dan Sensor Pemantauan di area dengan lonjakan perjalanan mencurigakan.
    - Membentuk Tim Inspeksi Lapangan untuk mengecek potensi manipulasi data oleh pengemudi.

**C. Edukasi**
* **Sosialisasi kepada Pengemudi tentang Kebijakan dan Etika** <br>
Program ini bertujuan untuk meningkatkan kesadaran pengemudi akan konsekuensi hukum manipulasi data serta pentingnya kejujuran dalam pencatatan perjalanan.
* **Pemberdayaan Penumpang dalam Pelaporan** <br>
Kampanyekan sistem pelaporan kecurangan berbasis aplikasi atau hotline agar penumpang merasa diberdayakan dan dilibatkan dalam menjaga integritas layanan.


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
* Buka file `NYC TLC Dashboard.twbx` pada folder report untuk membuka Dasboard Tableau <br>
atau membuka [Link Tableau Public](https://public.tableau.com/app/profile/khisanul.fakhrudin/viz/NYCTLCDashboard_17436066078670/Page1?publish=yes) dengan browser.

## 7. Contact 📩
* **Nama**: Muhammad Khisanul Fakhrudin Akbar
* **Email** : shinaruikhisan@gmail.com
* **Linkedin** : https://www.linkedin.com/in/muhammad-khisanul-fakhrudin-akbar/