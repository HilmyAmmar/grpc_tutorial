## Module 9 Reflection
### What are the key differences between unary, server streaming, and bi-directional streaming RPC (Remote Procedure Call) methods, and in what scenarios would each be most suitable?
Unary: Klient mengirim hanya 1 *request message*, Server menerima *request* dan mengirim *response* tunggal kembali ke klien, 
Cocok digunakan dalam keadaan dimana transfer data yang dilakukan terbatas  

Server-Streaming: Klient mengirim pesan permintaan tunggal, server menerima permintaan dan mengirimkan pesan respon kembali ke klien,
Cocok digunakan jika server perlu mengirim data dalam jumlah besar  

Bi-directional streaming: klien dan server bisa saling mengirim dan menerima pesan, adanya komunikasi dua arah secara *real-time* 
antara klien dan server, Cocok digunakan dalam aplikasi abrolan dan fitur kolaboratif dalam google docs/figma.


