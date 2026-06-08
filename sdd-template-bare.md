# Software Design Description
## For SCS (SmartRoom Campus System)

Version 0.1  
Prepared by Kelompok 5 
Siti Aisyah, Syifa Salma, Silvi Rusmiati, Salma Ikhti  
Rabu, 3 Juni 2026

## Table of Contents
<!-- TOC -->
* [1. Introduction](#1-introduction)
  * [1.1 Document Purpose](#11-document-purpose)
  * [1.2 Subject Scope](#12-subject-scope)
  * [1.3 Definitions, Acronyms, and Abbreviations](#13-definitions-acronyms-and-abbreviations)
  * [1.4 References](#14-references)
  * [1.5 Document Overview](#15-document-overview)
* [2. Design Overview](#2-design-overview)
  * [2.1 Penjelasan Sistem SRCS](#21-stakeholder-concerns)
  * [2.2 Alasan Menggunakan Arsitektur Object Oriented (OO)](#22-alasan-menggunakan-arsitektur-object-oriented-(OO))
* [3. Design Views](#3-design-views)
   * [3.1 Identifikasi Objek Atau Class](#31-identifikasi-object)
   * [3.2 Class Diagram](#32-class-diagram)
   * [3.3 Activity Diagram Login ](#33-activity-diagram-login)
   * [3.4 Activity Diagram Booking Ruangan ](#34-activity-diagram-booking-ruangan)
   * [3.5 Swimlane Diagram](#35-swimlane-diagram)
   * [3.6 Fokus Perancangan Antar Muka](#36-fokus-perancangan-antar-muka)
<!-- TOC -->

## Revision History
<!-- tracks document updates and reasons for change -->

| Name | Date | Reason For Changes | Version |
|------|------|--------------------|---------|
|      |      |                    |         |
|      |      |                    |         |

# 1. Introduction

## 1.1 Document Purpose
Dokumen Software Design Description (SDD) ini dibuat untuk mendeskripsikan rancangan perangkat lunak Smart Room Campus System (SRCS) secara terstruktur dan terperinci. Dokumen ini berfungsi sebagai acuan bagi tim pengembang dalam proses implementasi sistem, serta memberikan gambaran mengenai arsitektur, desain antarmuka, struktur kelas, dan mekanisme kerja sistem kepada seluruh stakeholder yang terlibat.

Selain itu, dokumen ini menjadi dasar dalam memastikan bahwa desain yang dikembangkan telah sesuai dengan kebutuhan yang telah didefinisikan pada dokumen Software Requirements Specification (SRS).

## 1.2 Subject Scope
Smart Room Campus System (SRCS) merupakan aplikasi berbasis web yang dirancang untuk membantu pengelolaan dan peminjaman ruangan di lingkungan kampus secara digital. Sistem ini memungkinkan mahasiswa, dosen, dan admin untuk mengakses informasi ketersediaan ruangan secara real-time, melakukan pemesanan ruangan secara online, serta mengelola proses persetujuan peminjaman secara terintegrasi.

Fitur utama yang tersedia dalam sistem meliputi login dan autentikasi pengguna, pengecekan ketersediaan ruangan, pemesanan ruangan, verifikasi peminjaman oleh admin, pengelolaan fasilitas ruangan, serta notifikasi status peminjaman.

## 1.3 Definitions, Acronyms, and Abbreviations
| Istilah/Singkatan | Keterangan                                                                                           |
| ----------------- | ---------------------------------------------------------------------------------------------------- |
| SRCS              | Smart Room Campus System                                                                             |
| SDD               | Software Design Description                                                                          |
| SRS               | Software Requirements Specification                                                                  |
| GUI               | Graphical User Interface                                                                             |
| Admin Sapras      | Pengelola sarana dan prasarana kampus yang bertanggung jawab melakukan verifikasi peminjaman ruangan |
| Booking           | Proses pemesanan atau peminjaman ruangan                                                             |
| Real-Time         | Informasi yang ditampilkan secara langsung sesuai kondisi terkini                                    |
| Database          | Tempat penyimpanan data yang digunakan oleh sistem                                                   |
| Client-Server     | Arsitektur sistem yang memisahkan pengguna (client) dan pengelola data (server)                      |


## 1.4 References
Dokumen ini disusun berdasarkan referensi berikut:
1. Dokumen Software Requirements Specification (SRS) Smart Room Campus System (SRCS).
2. Materi Rekayasa Perangkat Lunak (RPL).
3. Hasil wawancara dengan bagian Sarana dan Prasarana (Sapras) kampus.
4. Kebutuhan pengguna yang diperoleh dari mahasiswa dan dosen sebagai calon pengguna sistem.

## 1.5 Document Overview
Dokumen DDP ini terdiri dari beberapa bagian penting. Bab Pendahuluan menguraikan tujuan, ruang lingkup, definisi istilah, referensi, dan gambaran umum dokumen. Bab Gambaran Desain memberikan penjelasan umum mengenai desain sistem serta pendekatan yang diambil dalam pengembangan software. Bab Pandangan Desain berisi rincian desain sistem, termasuk diagram kelas, diagram aktivitas, diagram swimlane, dan desain antarmuka pengguna. Bab Keputusan menjelaskan keputusan desain yang diambil selama proses pembuatan, sementara bagian Lampiran memuat materi dukung yang relevan dengan dokumentasi desain sistem.

# 2. Design Overview

## 2.1 Penjelasan Sistem SRCS
Sistem yang dikembangkan dalam penelitian ini adalah Smart Room Campus System (SRCS) yang dibangun berbasis web application. Aplikasi berbasis web ini memungkinkan pengguna untuk mengakses sistem melalui browser tanpa perlu melakukan instalasi tambahan pada perangkat. Sistem dirancang agar dapat berjalan pada berbagai platform seperti komputer, laptop, maupun smartphone selama terhubung dengan jaringan internet. 

Secara arsitektur, sistem menggunakan konsep client-server, dimana: 
• Client merupakan perangkat pengguna (mahasiswa, dosen, admin) yang mengakses sistem melalui browser 
• Server berfungsi sebagai pusat pengolahan data dan penyimpanan database 

Sistem ini juga dirancang untuk: 
• Mendukung akses multi-user secara bersamaan 
• Menyediakan informasi secara real-time terkait ketersediaan ruangan 
• Terintegrasi dengan database untuk penyimpanan data peminjaman Dengan pendekatan berbasis web ini, diharapkan sistem dapat memberikan kemudahan akses, fleksibilitas pengguna.


### 2.2 Alasan Menggunakan Arsitektur Object Oriented (OO)

Objek dalam Sistem
Smart Room Campus System memiliki entitas-entitas nyata yang secara alami dapat direpresentasikan sebagai objek, antara lain:
•	User (Mahasiswa, Dosen, Admin Sapras): setiap pengguna memiliki data dan perilaku tersendiri
•	Ruangan: memiliki atribut seperti nama, kapasitas, dan fasilitas
•	Booking: merepresentasikan proses peminjaman ruangan
•	Notifikasi: objek yang dikirim ke pengguna berdasarkan status booking
•	Fasilitas: tambahan yang dapat diminta saat booking (proyektor, AC, dll)

Hubungan Antar Objek
Objek-objek dalam SRCS saling berinteraksi membentuk alur bisnis yang jelas:
•	User melakukan Booking terhadap Ruangan
•	Booking memiliki relasi ke Fasilitas yang diminta
•	Admin memverifikasi Booking dan mengubah statusnya
•	Notifikasi dikirim ke User berdasarkan perubahan status Booking

Hubungan ini wajar dalam OO karena Mahasiswa dan Dosen pada dasarnya sama-sama User, hanya berbeda hak akses , cukup dibuat satu class User yang diwarisi keduanya.
Keuntungan OO pada Sistem SRCS:

Modular:  setiap fitur berdiri sendiri, jadi kalau ada yang error atau perlu diubah, tidak mengganggu bagian lain.
Tidak perlu mengulang kode: Mahasiswa dan Dosen berbagi data dasar seperti nama dan password dari class User yang sama.
Mudah dikembangkan: kalau ke depannya mau tambah fitur baru seperti IoT atau integrasi sistem akademik, tinggal tambah class baru tanpa mengubah yang sudah ada.
Dekat dengan dunia nyata:  objek dalam sistem seperti Ruangan, Booking, dan Notifikasi mencerminkan hal-hal nyata di kampus, sehingga alur sistem lebih mudah dipahami semua pihak.


# 3. Design View

### 3.1	Identifikasi Object / Class

Berikut class-class yang terdapat dalam sistem SRCS beserta fungsinya:

1.	User: Class induk yang mewakili semua pengguna sistem. Menyimpan data dasar seperti nama, email, password, dan role. Class ini diwarisi oleh Mahasiswa, Dosen, dan Admin.
2.	Mahasiswa: Turunan dari User. Mewakili mahasiswa yang dapat mengajukan peminjaman ruangan untuk kegiatan akademik maupun organisasi.
3.	Dosen: Turunan dari User. Mewakili dosen yang dapat memesan ruangan untuk perkuliahan tambahan, seminar, atau bimbingan.
4.	Admin (Sapras): Turunan dari User. Bertanggung jawab memverifikasi permintaan booking, mengelola data ruangan, dan mengatur fasilitas.
5.	Ruangan: Mewakili ruang fisik di kampus. Menyimpan informasi seperti nama ruangan, kapasitas, lokasi, dan status ketersediaan.
6.	Booking: Mewakili proses peminjaman ruangan. Menyimpan data seperti siapa yang memesan, ruangan mana, tanggal dan waktu, serta status persetujuan.
7.	Fasilitas: Mewakili fasilitas tambahan yang bisa diminta saat booking, seperti proyektor, sound system, atau penataan kursi.
8.	Notifikasi: Mewakili pesan yang dikirim ke pengguna ketika status booking berubah (disetujui, ditolak, atau menunggu).
9.	Dashboard: Menampilkan ringkasan informasi utama sesuai role pengguna — booking aktif, riwayat, dan statistik penggunaan ruangan.



### 3.2  Class Diagram
(![alt text](1.PNG))

Class Diagram pada sistem SRCS menggambarkan struktur kelas-kelas yang ada di dalam sistem beserta atribut, method, dan hubungan antar kelasnya. Diagram ini menjadi fondasi utama dalam perancangan sistem berbasis Object Oriented karena menunjukkan bagaimana setiap objek saling terhubung dan berinteraksi satu sama lain.

Hubungan antar class dalam sistem SRCS adalah sebagai berikut:
•	Inheritance : Mahasiswa, Dosen, dan Admin mewarisi class User — artinya ketiga class tersebut mewarisi atribut dasar seperti nama, email, dan password dari class User, namun masing-masing memiliki atribut dan method tambahan sesuai perannya.
•	Asosiasi : Mahasiswa/Dosen membuat Booking, Admin memverifikasi Booking, dan Booking terhubung ke Ruangan menggambarkan hubungan antar objek yang saling berinteraksi dalam alur peminjaman ruangan.
•	Agregasi : Booking mengandung Fasilitas, artinya Fasilitas dapat berdiri sendiri tanpa harus ada Booking, namun Booking bisa memiliki satu atau lebih Fasilitas tambahan.

Selain itu, Booking menghasilkan Notifikasi yang dikirim ke pengguna, dan data Booking ditampilkan di Dashboard sesuai role masing-masing pengguna.


### 3.3 Activity Diagram Login
Activity Diagram Login menggambarkan alur aktivitas yang terjadi ketika pengguna (Mahasiswa, Dosen, atau Admin) masuk ke dalam sistem SRCS. Diagram ini menunjukkan bagaimana sistem merespons setiap aksi pengguna, termasuk kondisi normal maupun kondisi alternatif seperti data salah atau kosong

(![alt text](diagram_login.PNG))

•	Pink muda		: aksi yang dilakukan pengguna 
•	Pink sedang		: respons dari sistem 
•	Pink tua		: notifikasi berhasil 
•	Pink gelap		: pesan error / peringatan 
•	Pink pastel : diamond	: titik keputusan / decision

Activity Diagram Login ini menggambarkan dua jalur utama:

•	Jalur normal
Pengguna membuka website, memilih menu login, mengisi username dan password, lalu menekan tombol login. Jika data valid, sistem menampilkan notifikasi berhasil dan langsung mengarahkan ke dashboard sesuai role masing-masing (mahasiswa, dosen, atau admin).
•	Jalur alternatif
Jika data tidak valid, sistem membedakan dua jenis kesalahan. Pertama, jika kolom kosong, muncul pesan "Data harus diisi". Kedua, jika username atau password salah, muncul pesan "Username/password salah". Keduanya mengarahkan pengguna kembali ke form untuk mencoba lagi.
	

### 3.4	Activity Diagram Booking Ruangan

(![alt text](bookingRuangan.PNG))

Activity Diagram Booking Ruangan menggambarkan proses pengajuan peminjaman ruangan oleh Mahasiswa atau Dosen setelah berhasil login.

•	Jalur normal
Pengguna memilih menu booking, sistem menampilkan form, pengguna mengisi data pemesanan seperti tanggal, waktu, dan keperluan kegiatan, lalu mengupload surat persyaratan dalam format PDF. Setelah klik submit dan semua data lengkap, sistem menyimpan data ke database dan mengirim notifikasi "Booking berhasil dikirim". Status booking kemudian berubah menjadi menunggu verifikasi admin.
•	Jalur alternatif 
Sistem mengecek dua kemungkinan error. Pertama, jika data pemesanan belum lengkap, muncul pesan "Data belum lengkap" dan pengguna diarahkan kembali ke form isian. Kedua, jika surat persyaratan belum diupload, muncul pesan "Upload surat wajib" dan pengguna diarahkan kembali ke bagian upload.


## 3.5  Swimlane Diagram
Login & Booking Ruangan

(![alt text](swimline.PNG))


Swimlane Diagram ini membagi alur sistem ke dalam tiga jalur (lane)
Berdasarkan aktor yang terlibat, yaitu User/Mahasiswa, Sistem, dan Admin. Tujuannya adalah untuk menunjukkan dengan jelas siapa yang bertanggung jawab atas setiap aktivitas dalam proses login dan booking ruangan.

•	Proses Login: dimulai dari User yang membuka website dan memilih menu login. Sistem merespons dengan menampilkan form, lalu User mengisi dan mengirim data. Sistem kemudian memvalidasi,  jika valid, dashboard ditampilkan; jika tidak, pesan error muncul dan User diminta mengulang.
•	Proses Booking: setelah login, User memilih menu booking. Sistem menampilkan form, User mengisi data dan mengupload surat persyaratan, lalu klik submit. Sistem mengecek kelengkapan data, jika lengkap, data disimpan ke database dan notifikasi dikirim ke Admin. Admin menerima notifikasi, melakukan verifikasi, lalu menyetujui atau menolak. Sistem memperbarui status booking dan mengirimkan notifikasi hasil ke User.


### 3.6	Fokus Perancangan Antarmuka
a.	Desain Antarmuka Inter-Modular
Menggambarkan hubungan dan aliran data antar modul yang ada di dalam sistem SRCS. Setiap modul saling terhubung dan dikendalikan oleh aliran data yang mengalir dari satu modul ke modul lainnya 

Diagram ini menunjukkan bagaimana setiap modul dalam SRCS saling terhubung dan berbagi data satu sama lain.

Login menjadi pintu masuk utama: setelah autentikasi berhasil, pengguna diarahkan ke Dashboard yang berfungsi sebagai pusat navigasi sistem.

Dari Dashboard, pengguna dapat mengakses empat modul utama. Cek Ruangan memungkinkan pengguna melihat ketersediaan ruangan secara real-time, dan hasilnya dapat langsung diteruskan ke modul Booking untuk memilih slot waktu. Modul Notifikasi menerima data dari Booking dan mengirimkan status peminjaman ke pengguna. Modul Approval Admin menerima data booking, lalu admin memverifikasi dan hasilnya dikirim kembali ke Dashboard untuk memperbarui data secara keseluruhan.

(![alt text](uiInterModular.PNG))

b.	Desain Antarmuka Eksternal
Desain Antarmuka Eksternal menggambarkan hubungan sistem SRCS dengan pihak atau perangkat di luar sistem itu sendiri, yaitu pengguna (Mahasiswa, Dosen, Admin), browser sebagai media akses, serta database dan server sebagai penyimpanan data. Sesuai materi, antarmuka eksternal mencakup antarmuka antar aplikasi dan antarmuka antara perangkat lunak dengan produsen/konsumen informasi non-manusia.

(![alt text](uiEksternal.PNG))

Diagram ini menunjukkan bagaimana sistem SRCS berinteraksi dengan pihak dan perangkat di luar sistem.

Dari sisi pengguna, Mahasiswa dan Dosen berinteraksi dengan sistem untuk melakukan booking dan mengecek ketersediaan ruangan. Admin Sapras berinteraksi untuk memverifikasi dan mengelola data ruangan. Ketiga pengguna ini mengakses sistem melalui Browser (Chrome, Edge, atau Firefox), browser mengirimkan input pengguna ke sistem dan sistem mengembalikan tampilan antarmuka.

Dari sisi teknis, sistem terhubung dua arah dengan Database/Server, sistem menyimpan data booking ke database dan mengambil data kembali saat dibutuhkan. Setelah proses selesai, sistem mengirimkan Notifikasi status peminjaman kembali ke pengguna.

c.	Desain Antarmuka Manusia-Komputer

1.	Halaman Dashboard
Dashboard adalah halaman pertama yang muncul setelah pengguna berhasil login. Tampilannya disesuaikan dengan role pengguna, pada contoh ini adalah mahasiswa. Halaman ini menampilkan ringkasan booking aktif, jumlah booking yang sedang menunggu persetujuan, dan total booking bulan ini. Di bawahnya terdapat daftar peminjaman aktif beserta statusnya (Disetujui / Menunggu) dan riwayat booking terbaru. Tombol + Booking Ruangan ditempatkan di pojok kanan atas agar mudah diakses kapan saja.
 
(![alt text](halamDashboard.PNG))

2.	Halaman Cek Ketersediaan Ruangan
Halaman ini menampilkan kalender mingguan yang menunjukkan ketersediaan ruangan secara real-time. Pengguna dapat memilih ruangan melalui dropdown di pojok kanan atas dan berpindah minggu menggunakan tombol navigasi kiri-kanan. Setiap slot waktu diberi kode warna yang jelas, hijau untuk tersedia, merah untuk sudah terbooking, dan kuning untuk menunggu persetujuan admin. Dengan tampilan ini pengguna langsung bisa melihat slot mana yang bisa dipesan tanpa perlu bertanya ke admin.

(![alt text](cekKetersediaan.PNG))

3.	Halaman Admin	
Halaman ini khusus untuk Admin Sapras. Menampilkan daftar semua permintaan booking yang masuk dalam bentuk tabel, dilengkapi filter berdasarkan tanggal dan ruangan. Setiap baris menampilkan nama pemohon, ruangan yang diminta, tanggal dan jam, serta status saat ini. Admin dapat langsung mengklik tombol Setujui atau Tolak pada setiap permintaan yang masih berstatus Menunggu, sedangkan yang sudah disetujui hanya menampilkan tombol Detail.

(![alt text](HalamanAdmin.PNG))


4. Form Pemesanan Ruangan
Form ini muncul ketika pengguna menekan tombol booking. Pengguna mengisi ruangan yang diinginkan melalui dropdown, menentukan tanggal, waktu mulai dan selesai, serta keperluan kegiatan. Terdapat area upload surat permohonan dalam format PDF maksimal 2 MB. Di bagian bawah tersedia checklist fasilitas tambahan yang bisa diminta seperti proyektor, sound system, mic wireless, AC tambahan, dan penataan kursi. Setelah semua terisi, pengguna menekan tombol Kirim Permintaan.


(![alt text](PemesananRuangan.PNG))



### 2.2 Selected Viewpoints
<!-- lists viewpoints used to describe the system, their purpose, and addressed concerns -->

#### 2.2.1 Context
<!-- system boundaries, external actors, and interactions -->

#### 2.2.2 Composition
<!-- major components/subsystems and how they are organized -->

#### 2.2.3 Logical
<!-- main abstractions (classes, interfaces) and relationships -->

#### 2.2.4 Physical
<!-- hardware topology and infrastructure constraints -->

#### 2.2.5 Structure
<!-- internal organization of components and connectors -->

#### 2.2.6 Dependency
<!-- relationships and dependencies among design elements -->

#### 2.2.7 Information
<!-- data structures, persistence, and data management -->

#### 2.2.8 Interface
<!-- contracts between components or with external systems -->

#### 2.2.9 Interaction
<!-- runtime message flow and collaboration among components -->

#### 2.2.10 Algorithm
<!-- processing logic, steps, and key computations -->

#### 2.2.11 State Dynamics
<!-- states, transitions, and events affecting system behavior -->

#### 2.2.12 Concurrency
<!-- handling of parallelism, synchronization, and ordering -->

#### 2.2.13 Patterns
<!-- design or architectural patterns applied and their roles -->

#### 2.2.14 Deployment
<!-- mapping of software components to physical nodes or environments -->

#### 2.2.15 Resources
<!-- resource use, allocation, and management (e.g., memory, threads) -->

## 3. Design Views
<!-- detailed architectural and design elements, diagrams, and rationale -->

## 4. Decisions
<!-- major design or architectural choices and their justifications -->

## 5. Appendixes
<!-- supporting material such as models, datasets, or references -->
