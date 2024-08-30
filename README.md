# Task-Lambda-Function-CI-CD

Pada tugas ini kita akan mencoba menggunakan Lambda function dengan CI/CD Pipeline. Disini saya menggunakan automation server Jenkins untuk tugas ini. Saya akan mencoba menggunakan 2 tipe job yang ada di Jenkins yakni **Freestyle Project** dan **Pipeline**.

Tools/Bahan yang digunakan pada tugas ini : 
1. Windows
2. Jenkins (Diinstall di Windows)
3. AWS Academy Sandbox Lab
4. Ngrok (Digunakan untuk Webhook Github)

## Jenkins Freestyle Project

* Pertama kita setting terlebih dahulu AWS Lambda nya. Buka Lambda pada AWS, kemudian kita create function baru, saya menggunakan python untuk bahasa pemrogramannya serta saya tambah trigger API Gateway dengan HTTP API untuk nanti mudah melihat hasilnya.

![image](https://github.com/user-attachments/assets/072f7621-2482-4cf2-9572-fb8ad725dd25)

* Untuk kode python yang ada pada Lambda, kita copy ataupun move ke repository github kita, dan diletakkan di main branch kita.


