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

Untuk command shell yang saya digunakan yakni : 
>```
>powershell Compress-Archive -Update lambda_function.py hello-world-didan.zip
>```
>Command ini berfungsi untuk mengubah file lambda_function.py yang ada di github repository menjadi file zip yang nanti digunakan untuk upload ke Lambda function

>```
>aws --version
>
>aws configure set aws_access_key_id $AWS_ACCESS_KEY_ID
>aws configure set aws_secret_access_key $AWS_SECRET_ACCESS_KEY
>aws configure set aws_session_token $AWS_SESSION_TOKEN
>aws configure set region us-west-2
>
>aws lambda update-function-code --function-name hello-world-didan --zip-file fileb://hello-world-didan.zip
>```
>Command ini digunakan untuk agar Jenkins bisa terkoneksi dengan AWS, kemudian meng-update code Lambda dengan file zip dari command sebelumnya.

* Selesai untuk konfigurasinya, kita coba untuk mengubah kode yang ada di github kemudian klik Build Now pada Jenkins dan lihat hasil perubahan kode di Lambda nya

https://github.com/user-attachments/assets/996f4fa9-8de0-4e7e-9ab7-e433fda2a503




