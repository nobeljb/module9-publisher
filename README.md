# Module 9 subscriber

## a. How much data your publisher program will send to the message broker in one run?

Program publisher akan mengirim 5 buah pesan ke message broker dalam satu kali dijalankan.  
Setiap pesan adalah objek UserCreatedEventMessage yang memiliki dua field: user_id dan user_name.

## b.  The url of: “amqp://guest:guest@localhost:5672” is the same as in the subscriber program, what does it mean?

URL tersebut menjelaskan alamat koneksi ke message broker (RabbitMQ). Rinciannya:

- amqp: protokol yang digunakan, yaitu AMQP (Advanced Message Queuing Protocol).
- guest:guest: username dan password untuk autentikasi ke broker RabbitMQ (username = guest, password = guest).
- localhost: alamat server RabbitMQ, dalam hal ini berarti berjalan di komputer lokal.
- 5672: adalah port default RabbitMQ untuk koneksi AMQP.

Karena publisher dan subscriber memakai URL yang sama, itu berarti keduanya terhubung ke RabbitMQ yang sama, sehingga pesan yang dipublish akan bisa diterima oleh subscriber melalui queue yang sama (misalnya user_created).

## Screen of my running RabbitMQ
![img.png](img.png)

## Sending and Processing Event

Gambar di bawah menunjukkan ketika publisher mengirim 5 event ke message broker RabbitMQ, dan subscriber berhasil menerima serta memproses event tersebut.

![img_1.png](img_1.png)

Setiap event berisi informasi `user_id` dan `user_name`, dan diproses oleh subscriber dengan mencetak isi pesan tersebut ke terminal.

## Monitoring Chart Based on Publisher

Gambar berikut menunjukkan tampilan antarmuka RabbitMQ Management pada `localhost:15672`.

![img_2.png](img_2.png)

Spike (lonjakan) pada grafik `Message rates` muncul saat publisher dijalankan (`cargo run`). Setiap spike menandakan sejumlah event dikirim ke message broker. Dalam kasus ini, setiap kali publisher dijalankan, lima event dikirim sekaligus, sehingga terjadi peningkatan pada `Publish` dan `Deliver (manual ack)` pada grafik.

Hal ini mengindikasikan bahwa sistem berjalan dengan baik, dan RabbitMQ berhasil mengatur alur pengiriman dan penerimaan pesan antara publisher dan subscriber.
