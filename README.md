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
