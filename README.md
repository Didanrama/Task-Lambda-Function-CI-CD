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

* Kemudian kode python yang ada pada Lambda, kita copy ataupun move ke repository github kita, dan diletakkan di main branch kita.

![image](https://github.com/user-attachments/assets/1a0564e2-3cef-42ec-8e4a-85edaaec53cf)

* Selanjutnya install Jenkins nya, lalu buka Jenkins dibrowser. Kita buat item baru dan pilih tipe Freestyle Project. Berikut adalah konfigurasi yang saya gunakan

![image](https://github.com/user-attachments/assets/481daa96-b259-493f-8ce8-a33bb0414e08)
![image](https://github.com/user-attachments/assets/bd4bac29-a8af-4899-bb50-e3092fcffa3f)
![image](https://github.com/user-attachments/assets/e47e6e1f-febb-490c-bb9b-ebc64c92b7bb)
![image](https://github.com/user-attachments/assets/31604872-fbd0-4a84-8355-405392989e4c)
![image](https://github.com/user-attachments/assets/cc12b515-f4c0-44dc-b9ca-6ff637289ffc)
![image](https://github.com/user-attachments/assets/6768172b-a434-49b7-8e5b-e88295a7d0bb)
![image](https://github.com/user-attachments/assets/455bec90-aad9-4cde-a237-31b4fc6ebe2a)
![image](https://github.com/user-attachments/assets/62438420-a719-45c7-9eed-69e9206ace08)






