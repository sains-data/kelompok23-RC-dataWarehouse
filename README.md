# Laporan Tugas Data Warehouse

## Misi 1 - Dokumentasi Spesifikasi

### A. Profil Industri & Masalah Bisnis

<p align="justify"> Di tengah transformasi digital dunia sepak bola, data kini menjadi aset penting untuk merumuskan strategi kemenangan. Namun, kompleksitas data mulai dari statistik pemain, jalannya pertandingan, hingga formasi dan taktik membuat klub dan pelatih kesulitan mengakses wawasan yang benar-benar relevan.

<p align="justify"> Taktika hadir sebagai penyedia layanan data analytics untuk sepak bola modern. Kami mengubah data mentah dari lebih dari 25.000 pertandingan dan 10.000 pemain Eropa menjadi insight taktis dan strategis untuk berbagai pihak: klub, pelatih, analis, media, bahkan fans. Tantangan utamanya adalah integrasi data dari berbagai sumber yang tidak terstruktur, sehingga dibutuhkan solusi Data Warehouse (DW) sebagai pondasi sistem analitik yang solid, akurat, dan mudah digunakan.

### B. Daftar Stakeholder & Tujuan Bisnis

#### Stakeholder & Peran dalam Industri Sepak Bola

| Stakeholder          | Peran dalam Industri Sepak Bola                             | Tujuan Penggunaan Data Warehouse                           |
|----------------------|------------------------------------------------------------|-----------------------------------------------------------|
| Pelatih Tim          | Menentukan strategi dan susunan pemain                      | Mengoptimalkan formasi dan taktik berdasarkan data lawan   |
| Analis Klub          | Menganalisis performa tim dan pemain                        | Mengukur performa per pertandingan, musim, dan lawan       |
| Departemen Rekrutmen | Menyeleksi dan mengevaluasi pemain baru                     | Menilai potensi pemain berdasarkan statistik historis       |
| Media & Penyiar      | Menyampaikan berita dan analisis pertandingan               | Menyediakan statistik menarik dan prediktif untuk penonton |
| Fans & Komunitas     | Konsumen informasi sepak bola                               | Mengakses insight mendalam, tidak hanya highlight atau skor|

#### Tujuan Bisnis

- Mengoptimalkan strategi pertandingan berdasarkan data historis lawan
- Meningkatkan efektivitas scouting pemain melalui data performa objektif
- Menyediakan laporan dan insight cepat untuk pelatih dan analis teknis
- Memberikan informasi taktis yang mudah diakses untuk media dan fans
- Menyatukan sumber data pertandingan dalam satu sistem terpusat (DW)

#### Interview Simulasi (Pelatih Kepala):

1. Saat menyusun strategi melawan lawan tertentu, data apa yang paling Anda butuhkan?
2. Apakah Anda ingin melihat performa pemain lawan berdasarkan formasi yang digunakan?
3. Seberapa sering Anda ingin mendapatkan laporan data (harian, mingguan, sebelum match)?
4. Apakah Anda lebih suka data visual (grafik, heatmap) atau tabel?
5. Pernahkah Anda kehilangan peluang taktik karena keterlambatan data?

#### Studi Kasus

<p align="justify"> Banyak klub sepak bola di Eropa mengalami kesulitan dalam melakukan analisis taktik lawan karena data tersebar di banyak file, tidak real-time, dan tidak disesuaikan dengan kebutuhan pelatih. Dengan DW, semua data ini dapat diakses dalam satu sistem dan bisa ditampilkan sesuai kebutuhan pelatih — misal: "Rekap 5 pertandingan terakhir melawan tim dengan formasi 4-3-3."

### C. Daftar Fakta & Dimensi

#### Fakta (Measures)

- Jumlah Gol
- Jumlah Assist
- Jumlah Tembakan & Akurasi
- Jumlah Intersep / Tackle
- Rata-rata Rating Pemain
- Penguasaan Bola (%)

#### Dimensi

- **Waktu**: Tanggal, musim, pekan ke-
- **Pemain**: Nama, posisi, usia, tinggi, kemampuan individu
- **Klub**: Nama klub, formasi, pelatih, liga
- **Kompetisi**: Nama liga, negara, tahun kompetisi
- **Lokasi**: Stadion, status (home/away), kota pertandingan
- **Formasi**: Formasi yang digunakan klub (misal: 4-3-3, 3-5-2)

#### Diagram Skema

##### Penjelasan Skema Bintang

<p align="justify"> Skema bintang (Star Schema) adalah model data dimensional yang umum digunakan dalam data warehouse untuk memfasilitasi analisis cepat dan efisien. Dalam skema ini:

- **Tabel Fakta** berada di tengah dan berisi data kuantitatif seperti gol, assist, dan statistik performa.
- **Tabel Dimensi** mengelilingi tabel fakta dan menyediakan konteks analisis, seperti siapa pemainnya, kapan pertandingan berlangsung, di mana lokasinya, dan dalam kompetisi apa.
  
<p align="justify"> Setiap tabel dimensi terhubung langsung ke tabel fakta melalui kunci primer/asing (primary/foreign key). Bentuk "bintang" muncul dari struktur ini: fakta di tengah, dan dimensi menyebar keluar.

**Keunggulan dari skema ini:**

- Query analisis menjadi lebih cepat
- Struktur mudah dipahami oleh analis bisnis dan pelatih
- Mendukung visualisasi dan pelaporan yang fleksibel

### D. Sumber Data & Metadata

| Nama File    | Kaggle Konten Utama                             | Format | Frekuensi Update |
|--------------|-------------------------------------------------|--------|------------------|
| Match.csv    | Data pertandingan, skor, tim, event pertandingan | CSV    | Mingguan         |
| Player.csv   | Atribut & statistik pemain                      | CSV    | Triwulanan       |
| Team.csv     | Info klub: nama, formasi, pelatih               | CSV    | Triwulanan       |
| League.csv   | Daftar liga, negara                             | CSV    | Tahunan          |

#### Contoh Metadata:

| Nama Kolom        | Tipe Data   | Deskripsi                                                   |
|-------------------|-------------|-------------------------------------------------------------|
| home_team_goal    | INTEGER     | Jumlah gol oleh tim tuan rumah                              |
| away_team_goal    | INTEGER     | Jumlah gol oleh tim tamu                                    |
| buildUpPlaySpeed  | STRING      | Strategi serangan: cepat/lambat                             |
| player_api_id     | INTEGER     | ID unik pemain yang digunakan lintas sistem                 |
| date              | DATE        | Tanggal pertandingan berlangsung                            |
| possession_home   | FLOAT       | Persentase penguasaan bola oleh tim tuan rumah              |

### E. Referensi

1. Hugomathien, “European Soccer Database,” Kaggle Dataset:  
   [Kaggle Link](https://www.kaggle.com/datasets/hugomathien/soccer)
   
2. Kimball, Ralph. *The Data Warehouse Toolkit*

---

## Misi 2 - Dokumentasi Desain
### 1. Ringkasan Kebutuhan dari Misi

#### 1.1 Ringkasan Tabel Dimensi, Hirarki, dan Ukuran

| Jenis   | Nama Tabel         | Hirarki/Detail     | Atribut                                                                 |
|---------|--------------------|--------------------|-------------------------------------------------------------------------|
| **Fakta** | Fakta Pertandingan  | Jumlah Gol, Assist, Tembakan, Akurasi, Intersep, Tackle, Rating, Penguasaan Bola (%)  |
| **Dimensi** | Dim_Waktu           | Tanggal → Pekan → Musim                                       |
| **Dimensi** | Dim_Pemain          | Nama → Posisi → Usia → Tinggi → Kemampuan Individu              |
| **Dimensi** | Dim_Klub            | Nama Klub → Formasi → Pelatih → Liga                            |
| **Dimensi** | Dim_Kompetisi       | Nama Liga → Negara → Tahun Kompetisi                            |
| **Dimensi** | Dim_Lokasi          | Stadion → Kota → Status Home/Away                              |
| **Dimensi** | Dim_Formasi         | Formasi → Strategi Taktikal                                     |

#### 1.2 Deskripsi Naratif Kebutuhan Bisnis

<p align="justify"> **Masalah bisnis:** Banyak klub kesulitan mengakses data taktis karena data tersebar, tidak real-time, dan tidak sesuai kebutuhan pelatih. DW diperlukan agar semua data terintegrasi dalam satu sistem yang cepat dan analitis.

#### 1.3 Metadata Bisnis

| Atribut           | Definisi                                       | Pengguna Utama       | Sumber Data (CSV) | Catatan                        |
|-------------------|------------------------------------------------|----------------------|-------------------|--------------------------------|
| home_team_goal    | Jumlah gol oleh tim tuan rumah                | Pelatih, Analis Klub | Match.csv         | —                              |
| away_team_goal    | Jumlah gol oleh tim tandang                    | Pelatih, Media       | Match.csv         | —                              |
| buildUpPlaySpeed  | Kecepatan serangan (lambat/cepat)              | Analis Klub, Pelatih | Team.csv          | Diganti jadi: strategi_serangan|
| player_api_id     | ID unik pemain                                 | Semua stakeholder teknis | Player.csv       | —                              |
| date              | Tanggal pertandingan                           | Semua stakeholder     | Match.csv         | —                              |
| possession_home   | Penguasaan bola tim tuan rumah (%)            | Analis Klub, Pelatih | Match.csv         | —                              |
| league_name       | Nama kompetisi                                 | Analis Klub, Media   | League.csv        | Nama jelas                    |
| player_attributes | Gabungan kemampuan individu pemain            | Rekruter, Analis Klub | Player.csv        | Jika tidak digunakan → dicatat|
| formation_used    | Formasi yang digunakan tim                     | Pelatih, Analis Klub | Team.csv/Match.csv| Nama diganti dari formation_classic |

#### 1.4 Inti Pendekatan Business-Driven

Pendekatan yang digunakan berfokus pada kebutuhan pelatih, analis, media, dan fans.

#### 1.5 Dokumentasi Skema Sumber dan Penyesuaian

Sumber Data & File: Data diperoleh dari file seperti Match.csv, Player.csv, Team.csv, dan League.csv, bersumber dari dataset Kaggle yang di-update secara mingguan hingga triwulanan.

Penyesuaian Atribut: Atribut teknis diubah namanya menjadi istilah bisnis agar mudah dipahami (misalnya buildUpPlaySpeed → strategi_serangan).

Pendekatan yang digunakan adalah business-driven, yaitu fokus awal pada kebutuhan pengguna bisnis. Atribut yang tidak digunakan tetap dicatat.

### 2. Skema

#### Penjelasan Skema Bintang

<p align="justify"> Skema bintang (Star Schema) adalah model data dimensional yang umum digunakan dalam data warehouse untuk memfasilitasi analisis cepat dan efisien. Dalam skema ini:

- **Tabel Fakta** berada di tengah dan berisi data kuantitatif seperti gol, assist, akurasi, dan lain-lain.
- **Tabel Dimensi** mengelilingi tabel fakta dan menyediakan konteks analisis, seperti siapa pemainnya, kapan pertandingan berlangsung, di mana lokasinya, dan dalam kompetisi apa.
  
<p align="justify"> Setiap tabel dimensi terhubung langsung ke tabel fakta melalui kunci primer/asing (primary/foreign key). Bentuk "bintang" muncul dari struktur ini: fakta di tengah, dan dimensi menyebar keluar.

**Keunggulan dari skema ini:**

- Query analisis menjadi lebih cepat
- Struktur mudah dipahami oleh analis bisnis dan pelatih
- Mendukung visualisasi dan pelaporan yang fleksibel

## 3. Penjelasan Tiap Komponen

<p align="justify"> Pendekatan multidimensional untuk membangun conceptual schema data warehouse mengorganisasi data menjadi dua jenis utama yakni fakta (facts) dan dimensi (dimensions) serta hierarki yang ada tiap dimensi. Berikut ini penjelasan tiap komponennya:

### A. Fakta Pertandingan

<p align="justify"> Fakta disini adalah tabel yang berisi data numerik atau metrik yang merepresentasikan kejadian nyata yakni pertandingan sepakbola yang terdiri dari: jumlah gol, penguasaan bola (Persentase kendali atas bola), jumlah operan, tembakan (ke arah gawang maupun tidak), assist (ada gol yang tidak ada assistnya) dan clean_sheet (Indikator tim dalam menjaga gawangnya tidak kebobolan). Dengan ini fakta memberikan fungsi sebagai inti dari data warehouse, menyimpan informasi kuantitatif yang dapat digunakan untuk analisis. Setiap baris dalam tabel fakta mewakili satu pertandingan. Foreign Keys yang menghubungkan tabel fakta ke masing-masing dimensi yakni: tanggal (Dim_Waktu), nama klub (Dim_Klub), stadion (Dim_Lokasi), nama (Dim_Lokasi) dan nama liga (Dim_Kompetisi).

### B. Dimensi

<p align="justify"> Dimensi disini adalah tabel yang menyediakan konteks kepada fakta. Mereka terdiri dari atribut deskriptif non-numerik pada data yang terdiri dari:

#### a. Dim_Waktu

<p align="justify"> Dimensi ini menyediakan konteks waktu mulainya setiap pertandingan untuk analisis tren seiring waktu, seperti perubahan performa tim atau pemain selama musim berjalan dengan hierarki berikut ini: tanggal (Data format datetime), musim (misal: "2023-2024"), pekan ke- (misal: jika ada 20 tim maka pertandingan sebanyak 38 pekan), hari pertandingan (biasanya akhir pekan Sabtu-Minggu).

#### b. Dim_Klub

<p align="justify"> Dimensi ini menyediakan informasi tentang klub sepak bola yang terlibat dalam membantu melacak performa klub secara keseluruhan, termasuk faktor-faktor seperti pengaruh pelatih terhadap tim dengan hierarki berikut ini: nama klub (resmi), pelatih (utama), ranking (taip kompetisi yang dijalani).

#### c. Dim_Lokasi

<p align="justify"> Dimensi ini menyediakan informasi lokasi pertandingan yang dapat membantu menganalisis faktor-faktor seperti keuntungan kandang, kondisi lapangan, atau preferensi penonton dengan hierarki berikut ini: stadion, kota (Kota tempat stadion/klub) dan status (pertandingan tandang atau kandang).

#### d. Dim_Pemain

<p align="justify"> Dimensi ini menyediakan informasi tentang pemain yang terlibat untuk menganalisis kontribusi individu pemain terhadap performa tim, serta faktor-faktor seperti usia atau tinggi badan yang mungkin mempengaruhi performa dengan hierarki berikut ini: nama, posisi (misal: gelandang tengah (CM), penyerang (ST)), usia, tinggi, dan kemampuan (misal: rating pertandingan (skala 0-10)).

#### e. Dim_Kompetisi

<p align="justify"> Dimensi ini menyediakan konteks kompetitif di mana pertandingan dilangsungkan untuk membantu memahami dinamika kompetisi, seperti tingkat kesulitan lawan atau dampak kompetisi internasional terhadap performa klub dengan hierarki berikut ini: nama liga (misal: Liga Premier Inggris, La Liga Spanyol), negara dan tingkat (misal: level nasional, internasional atau divisi).

#### f. Dim_Formasi

<p align="justify"> Dimensi ini menyediakan konteks formasi yang dipakai dan tipe strategi dari formasi supaya sesuai antar hierarki yang terdiri dari: formasi (misal: taktik 4-3-3, 5-4-1) dan strategi (misal: menyerang, bertahan).

### 4. Justifikasi Desain Konseptual

#### 4.1 Alasan Pemilihan Skema Bintang (Star Schema)

<p align="justify"> Desain konseptual menggunakan skema bintang dipilih karena memiliki keunggulan utama dalam kemudahan eksplorasi data oleh pengguna non-teknis, kinerja query yang cepat berkat struktur sederhana yang mendukung indeksasi efisien, serta kompatibilitas tinggi dengan OLAP dan visualisasi analitik. Dalam konteks industri sepak bola, skema ini sangat cocok untuk analisis performa, karena memudahkan penyajian informasi berdasarkan waktu, pemain, tim, maupun liga secara fleksibel.

#### 4.2 Relevansi Setiap Komponen

<p align="justify"> Setiap komponen dalam skema dirancang berdasarkan pertanyaan analitik kunci dan kebutuhan stakeholder dari Misi 1:

| Komponen                  | Justifikasi                                                                 |
|---------------------------|-----------------------------------------------------------------------------|
| **Fakta_Performa_Pertandingan** | Memuat metrik utama performa pemain yang diperlukan untuk evaluasi taktis dan manajerial. |
| **Dim_Pemain**             | Menyediakan detail identitas dan posisi pemain untuk analisis individu atau peran dalam tim. |
| **Dim_Tim**                | Menggambarkan konteks klub yang memungkinkan analisis performa berdasarkan asal tim. |
| **Dim_Waktu**              | Diperlukan untuk analisis tren historis, performa musiman, dan evaluasi tahunan. |
| **Dim_Liga**               | Berguna untuk segmentasi berdasarkan kompetisi yang diikuti, serta membandingkan performa antar liga. |

#### 4.3 Kesesuaian dengan Tujuan Analitik

Skema ini dapat menjawab kebutuhan seperti:

- Menampilkan top scorer dalam satu liga selama musim tertentu.
- Melihat distribusi kartu merah di setiap kuartal kompetisi.
- Membandingkan durasi bermain rata-rata berdasarkan posisi pemain.
- Menganalisis pengaruh pelatih baru terhadap performa tim.

#### 4.4 Integrasi Sumber Data

<p align="justify"> Desain ini juga mempertimbangkan struktur data mentah dari file seperti match.csv, player.csv, team.csv, dan league.csv yang telah diuraikan pada Misi 1. Ketersediaan atribut-atribut utama dalam sumber data menjamin kepraktisan implementasi skema ini secara teknis.

### 5. Kesesuaian dengan sumber data

#### 5.1 Asal Data

<p align="justify"> Data yang digunakan dalam skema konseptual dengan pendekatan multidimensional berasal dari European Soccer Database dengan platform Kaggle. Dataset tersebut merupakan sebuah dataset historis yang mengumpulkan data lebih dari 25.000 pertandingan sepak bola, 10.000 pemain dan 11 negara yang berada di Eropa. Dataset tersebut berisikan data statistik pertandingan, informasi para pemain, kompetisi yang diikuti dan detail dari klub yang dibentuk dalam format tabel. Hal tersebut menjadi dasar sistem analitik pada performa sepak bola modern.

#### 5.2 Hubungan Skema dengan Data Asal

<p align="justify"> Desain konseptual multidimensi yang telah dirancang memiliki tingkat kesesuaian yang tinggi dengan struktur data yang tersedia dalam dataset European Soccer Database. Setiap komponen yang terdapat dalam skema, baik fakta maupun dimensi dapat dipetakan secara langsung ke dalam tabel dan atribut dalam sumber dataset. Hal tersebut memastikan bahwa proses pengisian data ke dalam skema data warehouse efisien dan realistis.

**Berikut hubungan antara skema konseptual dengan data asal:**

| Komponen Skema              | Sumber Data   | Atribut Utama                | Keterangan                                                                  |
|-----------------------------|---------------|------------------------------|----------------------------------------------------------------------------|
| **Fakta_Performa_Pertandingan** | Match.csv     | home_team_goal, away_team_goal, possession, shots_on_target | Statistik performa pertandingan yang digunakan untuk mengevaluasi secara taktis dan manajerial. |
| **Dim_Pemain**               | Player.csv    | player_name, birthday, height, weight, potential | Identitas dan karakteristik pemain yang relevan untuk analisis tiap individu. |
| **Dim_Tim**                  | Team.csv      | team_long_name, formation, coach_name | Informasi mengenai klub dan formasi tim yang mendukung analisis berbasis tim. |
| **Dim_Waktu**                | Match.csv     | date, season                  | Informasi mengenai tanggal dan musim untuk analisis tren historis. |
| **Dim_Liga**                 | League.csv    | league_name, country_id       | Nama liga dan negara untuk segmentasi kompetisi. |

---

## Misi 4 - Implementasi, Reporting, dan Produksi

### 1. Pendahuluan

#### 1.1 Latar Belakang

<p align="justify"> Di era digitalisasi olahraga modern, data menjadi aset penting bagi klub sepak bola dalam pengambilan keputusan taktis dan strategis. Namun, data tersebar dalam berbagai format dan sumber seperti database SQLite, file CSV, dan Excel. Ketidakterpaduan tersebut dapat menyulitkan analisis yang menyeluruh terhadap performa pemain, baik pola permainan lawan hingga manajemen operasional tim. Untuk mengatasi hal tersebut, diperlukannya mengintegrasikan data secara efisien dan dibutuhkan sistem Data Warehouse (DW) yang mampu menyimpan, memproses, dan menyajikan data secara terstruktur. Proyek ini bertujuan membangun gudang data bertema sepak bola “Taktika: Where Data Meets Strategy” sebagai platform utama untuk analitik sepak bola.

#### 1.2 Tujuan

1. Membangun gudang data berbasis SQL Server.
2. Menerapkan proses ETL untuk memindahkan data mentah ke dalam Data Warehouse.
3. Menyediakan query analitik OLAP berbasis SQL.
4. Menyusun dokumentasi proyek dan struktur repositori Github.

#### 1.2 Ruang Lingkup

1. Tabel fakta berisi performa pertandingan.
2. Tabel dimensi mencakup waktu, pemain, tim, lokasi, formasi dan kompetisi.
3. Proses transformasi data dari SQLite atau CSV ke bentuk yang lebih terstruktur.
4. Penerapan indexing, partisi, dan views untuk optimasi performa query.

### 2. Metodologi Pengembangan

#### 2.1 Pendekatan Waterfall

Tahapan pengembangan dengan pendekatan waterfall dilakukan secara berurutan:
1. **Misi 1**: Identifikasi kebutuhan dan stakeholder.
2. **Misi 2**: Desain konseptual dan logika.
3. **Misi 3**: Desain fisikal, indexing dan partisi.
4. **Misi 4**: Implementasi, ETL, OLAP dan pelaporan.

#### 2.2 Tools yang Digunakan

1. **SQL Server** untuk melakukan manajemen Data Warehouse.
2. **Python** dan **SQLite3** untuk proses ETL.
3. **Power BI** atau **Tableau** untuk pelaporan visual.
4. **Github** sebagai repositori dokumentasi dan script SQL.

### 3. Analisis Kebutuhan ( Misi 1 )

#### 3.1 Stakeholder Utama

1. **Pelatih**: Sebagai pemilih strategi, menyusun formasi dan taktik dalam pertandingan berdasarkan data lawan dan tim pemain.
2. **Analisis Klub**: Bertugas untuk menganalisis dan mengevaluasi performa pemain baik secara individu maupun tim secara keseluruhan.
3. **Media dan Fans**: Menginginkan akses statistik yang informatif dan menarik.

#### 3.2 Fakta dan Dimensi

**Tabel Fakta:**
- fakta_performa_pertandingan: Menyimpan data statistik seperti gol, assist dan waktu bermain.

**Tabel Dimensi:**
- dim_pemain:  Menyimpan data deskriptif pemain yang berisikan nama, posisi, dan usia.
- dim_tim: Menyimpan informasi mengenai tim yang berisikan nama, tim dan pelatih.
- dim_formasi: Menyimpan informasi taktis mengenai formasi tim dalam pertandingan tertentu.
- dim_kompetisi: Menyimpan informasi mengenai liga dan negara.
- dim_lokasi: Menyimpan data lokasi berlangsungnya pertandingan seperti stadion dan kota.
- dim_waktu: Menyediakan dimensi waktu untuk analisis temporal dalam bentuk tanggal, bulan dan tahun.

### 4. Desain Data Warehouse ( Misi 2 dan 3 )

#### 4.1 Desain Konseptual
<p align="justify"> Desain konseptual data warehouse menggunakan pendekatan skema bintang (star schema), dimana tabel fakta berada di pusat dengan foreign key yang dihubungkan  ke tabel dimensi. Struktur tersebut mendukung eksplorasi data dengan menggunakan OLAP (Online Analytical Processing) dan visualisasi interaktif.

#### 4.2 Script Pembuatan Tabel Dimensi
```
CREATE TABLE dim_waktu (
  id_dim_waktu INT PRIMARY KEY,
  tanggal DATE,
  bulan VARCHAR(20),
  tahun INT
);
CREATE TABLE dim_tim (
  id_dim_tim INT PRIMARY KEY,
  nama_tim VARCHAR(100),
  pelatih VARCHAR(100)
);
```
<p align="justify"> Pembuatan tabel dim_waktu berfungsi untuk mencatat referensi waktu pada setiap peristiwa pertandingan dalam tabel fakta. Tabel dim_waktu memungkinkan untuk melakukan analisis performa tim atau pemain seperti tren bulanan dan tahunan berdasarkan periode waktu tertentu. Sedangkan tabel dim_tim berfungsi untuk menyimpan informasi deskriptif mengenai tim yang bertanding. Tabel dim_tim dapat memungkinkan pengguna melakukan analisis untuk melihat performa tim berdasarkan klub dan pelatih.

#### 4.3 Script Pembuatan Tabel Fakta
```
CREATE TABLE fakta_performa_pertandingan (
  id_fakta INT PRIMARY KEY,
  id_dim_tim INT,
  id_dim_pemain INT,
  id_dim_waktu INT,
  jumlah_gol INT,
  jumlah_assist INT,
  FOREIGN KEY (id_dim_tim) REFERENCES dim_tim(id_dim_tim),
  FOREIGN KEY (id_dim_pemain) REFERENCES dim_pemain(id_dim_pemain),
  FOREIGN KEY (id_dim_waktu) REFERENCES dim_waktu(id_dim_waktu)
);

```
<p align="justify"> Tabel fakta_performa_pertandingan menyimpan data kuantitatif yang dapat digunakan untuk mempresentasikan para performa pemain individu dalam suatu pertandingan. Dengan direlasikan ke tabel dimensi, dapat dilakukannya analisis multidimensi dengan OLAP seperti tren performa pemain berdasarkan formasi tertentu atau perbandingan antar liga.

#### 4.4 Indexing dan Partisi

Script index waktu pertandingan: 
```
CREATE CLUSTERED INDEX idx_match_date
ON fakta_performa_pertandingan (id_dim_waktu);
```

<p align="justify"> Indeks  waktu pertandingan dibuat dikarenakan pada rentang waktu tertentu, analisis dan pelaporan dibuat seperti tren performa setiap per bulan ataupun per tahun. Untuk memastikan data disusun berdasarkan urutan waktu, digunakannya clustered index supaya pencarian dan agregasi data per waktu menjadi lebih cepat dan efisien.

<p align="justify"> Partisi dilakukan secara horizontal berdasarkan tahun pertandingan dengan membagi data berdasarkan segmen nilai tahun dan waktu untuk efisiensi manajemen data. Tujuan partisi ini adalah untuk:
1. Meningkatkan efisiensi pemrosesan data.
2. Mempermudah pemeliharaan manajemen data historis.
3. Menghindari data besar dengan beban yang berlebih saat menganalisis data dari beberapa musim pertandingan.

### 5. IMPLEMENTASI GUDANG DATA ( MISI 4 )

#### 5.1 Pembuatan Struktur dan Relasi

1. Semua tabel dibuat menggunakan script create_tables.sql.
2. Data dummy dari data_dw.sql dimuat melalui insert_data.sql.
3. Semua foreign key telah dikonfigurasi antar dimensi dan fakta.


#### 5.2 Commit ke GitHub
Struktur file:
- sql/create_tables.sql
- sql/insert_data.sql
- sql/analysis_queries.sql
- docs/laporan_misi4.pdf

### 6. Proses ETL / ELT

#### 6.1 Ekstraksi
<p align="justify"> Proses ekstraksi dilakukan dengan menggunakan Python yang terhubung dengan SQLite. Data hasil ekstraksi tersebut disimpan dalam format staging area atau sementara yang kemudian akan diproses pada tahap transformasi. Data pertandingan tersebut diambil dari tabel match dengan secara keseluruhan dengan menggunakan query SQL:

```
import sqlite3
conn = sqlite3.connect('database.sqlite')
cursor = conn.cursor()
cursor.execute("SELECT * FROM match")
data = cursor.fetchall()
```
  
#### 6.2 Transformasi

<p align="justify"> Pada tahap transformasi, data mentah diolah supaya sesuai dengan struktur Data Warehouse, yaitu: 

1. Mengubah format tanggal yang sebelumnya bertipe YYYY-MM-DD menjadi integer ID yang merepresentasikan waktu.
2. Normalisasi data ke tabel dimensi berdasarkan atribut, dengan memastikan data tersebut konsisten dan tidak ada duplikasi.
3. Validasi data untuk menjaga kualitas data supaya tidak ada nilai null ketika melakukan mapping formasi para pemain.

#### 6.3 Load ke Warehouse
<p align="justify"> Setelah melakukan transformasi data, dilakukannya proses loading dengan insert data ke dalam tabel fakta dan tabel dimensi Data Warehouse untuk memastikan data tersebut sudah siap untuk dilakukannya analisis OLAP. Berikut contoh query untuk load data ke Warehouse:

```
INSERT INTO fakta_performa_pertandingan
SELECT ... FROM staging_match;
```

### 7. Query OLAP Dan Analitik

#### 7.1 Total Gol per Tim
<p align="justify"> Berikut query untuk menampilkan akumulasi gol oleh setiap tim. Hasil query tersebut dapat dilakukannya analisis untuk memahami tim mana yang memiliki kekuatan serangan terbaik.
  
```
SELECT dt.nama_tim, SUM(fp.jumlah_gol) AS total_gol
FROM fakta_performa_pertandingan fp
JOIN dim_tim dt ON fp.id_dim_tim = dt.id_dim_tim
GROUP BY dt.nama_tim;
```

#### 7.2 Rata-rata Assist Pemain
<p align="justify"> Untuk menghitung rata-rata kontribusi assist setiap pemain, query ini dapat memberikan insight mengenai kontribusi para pemain dalam proses menciptakan gol.

```  
SELECT dp.nama_pemain, AVG(fp.jumlah_assist) AS rata_assist
FROM fakta_performa_pertandingan fp
JOIN dim_pemain dp ON fp.id_dim_pemain = dp.id_dim_pemain
GROUP BY dp.nama_pemain;
```

#### 7.3 Total Gol per Tahun
<p align="justify"> Analisis tren jumlah gol dari tahun ke tahun dilakukan untuk melihat performa secara temporal dari tim dan pemain. Untuk membantu mengidentifikasi periode peningkatan performa atau musim terbaik, dapat digunakan query berikut:

```
SELECT dw.tahun, SUM(fp.jumlah_gol) AS total_gol
FROM fakta_performa_pertandingan fp
JOIN dim_waktu dw ON fp.id_dim_waktu = dw.id_dim_waktu
GROUP BY dw.tahun;
```

### 8. Hasil Implementasi Dan Evaluasi

### 8.1 Hasil Implementasi

1. Semua komponen termasuk tabel fakta, tabel dimensi, indeks dan partisi berhasil dibuat dan diuji sesuai rancangan.
2. Data dummy mempermudah pengujian performa query dan validasi struktur data secara efektif.
3. Struktur skema bintang (star schema) dan integritas relasi antar tabel sudah terimplementasi dengan baik sesuai standar Data Warehouse dan mendukung proses analitik OLAP.


### 8.2 Evaluasi

**Keberhasilan**:
1. Struktur skema bintang (star schema) berjalan baik, terbukti mendukung dalam melakukan analisis multidimensi secara efisien.
2. Penerapan indexing dan partisi memberikan peningkatan yang signifikan pada kecepatan dalam eksekusi query OLAP, khususnya pada analisis berbasis waktu 


**Kendala dan tantangan**:
1. Data dummy yang digunakan belum sepenuhnya mewakili skenario riil kompetisi, sehingga analisis bersifat terbatas.
2. Transformasi awal dari SQLite memerlukan pembersihan dan normalisasi secara manual, sehingga memakan waktu yang cukup banyak.

### 9. Penutup Dan Pengembangan Lanjutan

#### 9.1 Pengembangan Ke Depan

1. Mengembangkan visualisasi interaktif di Power BI berdasarkan query OLAP, untuk mendukung eksplorasi data.
2. Integrasi data live dari API sepak bola resmi, supaya Data Warehouse selalu terupdate dan selalu relevan pada kondisi pertandingan yang terkini.
3. Otomatisasi pipeline ETL dengan tools seperti Microsoft SSIS atau Apache Airflow untuk peningkatan efisiensi dan mengurangi kesalah manual.


#### 9.2 Kesimpulan
<p align="justify"> Proyek ini berhasil menunjukkan bahwa sistem Data Warehouse bertema sepak bola dengan skema bintang, yang didukung dengan proses ETL dan indexing yang tepat mampu meningkatkan performa query OLAP. Sistem yang dibuat mampu menyediakan insight penting dalam domain sepak bola, seperti pengambilan keputusan dan strategi dalam dunia sepak bola.

### LAMPIRAN TIM PROYEK

- **Nama Tim**: DWFC (Data Warehouse Football Club)
- **Anggota**:
  - Muhammad Kaisar Firdaus
  - Haikal Dwi Syaputra
  - Aditya Rahman
  - Khaalishah Zuhrah A. V.
  - Rafa Aqilla Jungjunan
- **Ketua Proyek**: Muhammad Kaisar Firdaus
