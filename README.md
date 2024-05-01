## Module 9 Reflection
### What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
Unary: Klient mengirim hanya 1 *request message*, Server menerima *request* dan mengirim *response* tunggal kembali ke klien, 
Cocok digunakan dalam keadaan dimana transfer data yang dilakukan terbatas  

Server-Streaming: Klient mengirim pesan permintaan tunggal, server menerima permintaan dan mengirimkan pesan respon kembali ke klien,
Cocok digunakan jika server perlu mengirim data dalam jumlah besar  

Bi-directional streaming: klien dan server bisa saling mengirim dan menerima pesan, adanya komunikasi dua arah secara *real-time* 
antara klien dan server, Cocok digunakan dalam aplikasi abrolan dan fitur kolaboratif dalam google docs/figma.

### What are the potential security considerations involved in implementing a gRPC service in Rust, particularly regarding authentication, authorization, and data encryption?
- Menghindari penggunaan plain text dalam mengirimkan pesan yang penting seperti username atau password
- Memastikan mekanisme yang digunakan untuk verifikasi data klien aman. Mekanisme ini bisa berupa token dan penggunaan username serta password dengan validasi yang baik dan hashing yang aman
- Membuat validasi yang ketat pada data yang diterima dari klien untuk mencegah terjadinya SQL dan command injection
- Menggunakan Transport Layer Security (TLS) untuk mengamankan komunikasi antar service

### What are the potential challenges or issues that may arise when handling bidirectional streaming in Rust gRPC, especially in scenarios like chat applications?
- Bidirectional streaming mengomsumsi banyak memori, apalagi ketika banyak pengguna yang aktif dalam mengirimkan dan menerima pesan. Penting bagi developer untuk melakukan optimisasi kode dengan penggunaan asynchronous programming.
- Ada kemungkinan pesan yang dikirimkan hilang atau tidak terkirim. Hal ini bisa diatasi dengan menyediakan fitur yang dapat melakukan pengiriman ulang pesan tanpa perlu menulis pesan itu kembali
- Manajemen state akan semakin rumit ketika banyak pengguna yang terhubung. Kode perlu untuk didesain dengan baik untuk menghindari kebocoran memori terkait state

### What are the advantages and disadvantages of using the tokio_stream::wrappers::ReceiverStream for streaming responses in Rust gRPC services?
Keuntungan: Memungkinkan streaming asynchronous yang akan meningkatkan responsivitas, mencegah klien kewalahan dengan data, streaming dapat dilakukan dengan berbagai tipe data
Kerugian: Menambahkan kompleksitas kode, Membutuhkan penanganan error yang baik, Terdapat potensi terjadinya kebocoran memori jika tidak dikelola dengan baik

### In what ways could the Rust gRPC code be structured to facilitate code reuse and modularity, promoting maintainability and extensibility over time?
- Menggunakan protobuf melalui file .proto untuk standarisasi pesan dan method antar service
- Pisahkan kode menjadi modul-modul kecil berdasarkan fungsionalitas tertentu
- Memiliki logging untuk melacak aktivitas service dan melakukan monitoring performa
- Buat unit test dan integration test untuk memastikan kualitas kode

### In the MyPaymentService implementation, what additional steps might be necessary to handle more complex payment processing logic?
- Memastikan data yang diterima valid sebelum dproses
- Memastikan sistem dapat memberikan respon yang baik ketika terjadi error tertentu
- Memanfaatkan *logging* dan *monitoring* untuk mencatat aktivitas dan performa sistem pembayaran

### What impact does the adoption of gRPC as a communication protocol have on the overall architecture and design of distributed systems, particularly in terms of interoperability with other technologies and platforms?
- Memungkinkan pembuatan service dan client di berbagai bahasa pemrograman yang mendukung gRPC
- Meningkatkan interoperabilitas yang lebih baik antara service yang dibangun dengan bahasa pemrograman yang berbeda jika menggunakan gRPC sebagai protokol komunikasi standar
- Meminimalkan overhead transfer data dan meningkatkan performa keseluruhan sistem
- Berjalan di berbagai platform dan sistem operasi

### What are the advantages and disadvantages of using HTTP/2, the underlying protocol for gRPC, compared to HTTP/1.1 or HTTP/1.1 with WebSocket for REST APIs?
Keuntungan HTTP/2:
- Memungkinkan pengiriman dan penerimaan beberapa permintaan/respon secara bersamaan melalui satu koneksi TCP
- Mengurangi kode boilerplate
- Menggunakan protobuf untuk representasi data yang ringkas, mengurangi overhead dibandingkan format berbais teks seperti JSON

Kekurangan HTTP/2:
- Memiliki kompleksitas yang lebih tinggi dibanding HTTP/1.1 pada REST API.
- Tidak didukung oleh semua server dan klien

Keuntungan HTTP/1.1:
- Didukung oleh semua server dan klien, kompabilitas lebih luas
- Kompleksitas lebih rendah dibanding HTTP/2, memudahkan penerapan dan penggunaan
- Memungkinkan berbagai metode permintaan (GET,POST,PUT,DELETE) untuk operasi yang berbeda

Kekurangan HTTP/1.1:
- Traffic jaringan yang tinggi karena banyak header yang dibutuhkan pada setiap permintaan
- Satu permintaan yang lambat dapat memblokir permintaan selanjutnya pada koneksi yang sama

## How does the request-response model of REST APIs contrast with the bidirectional streaming capabilities of gRPC in terms of real-time communication and responsiveness?
REST API:
- Model Komunikasi: Satu arah
- Kesesuaian real-time: Terbatas
- Latensi: Lebih tinggi
- Aliran data: Permintaan diskrit

gRPC:
- Model komunikas: Dua arah
- Kesesuaian real-time: Ideal
- Latens: Lebih rendah
- Aliran data: Berkelanjutan
