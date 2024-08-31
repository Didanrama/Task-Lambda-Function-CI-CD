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

Untuk command shell yang digunakan yakni : 
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

## Jenkins Pipeline

* Kita akan mencoba tipe Pipeline. Buat item baru di Jenkins dengan tipe Pipeline, dan berikut adalah konfigurasi yang digunakan

![image](https://github.com/user-attachments/assets/5f90109a-184a-4eec-933b-c29e8453660e)
![image](https://github.com/user-attachments/assets/67eeb883-51a1-4bb3-9128-b0b488ee5eb1)
![image](https://github.com/user-attachments/assets/7d367f31-f56a-4f18-9597-ee7901f1ae6e)
Berikut script lebih jelas :
```
pipeline {
    agent any

    environment {
        AWS_REGION = 'us-west-2'
        LAMBDA_FUNCTION_NAME = 'hello-world-didan'
        AWS_ACCESS_KEY_ID = credentials('AWS_ACCESS_KEY_ID')
        AWS_SECRET_ACCESS_KEY = credentials('AWS_SECRET_ACCESS_KEY') 
        AWS_SESSION_TOKEN = credentials('AWS_SESSION_TOKEN')
    }

    stages {
        stage('Checkout Source Code') {
            steps {
                git branch: 'main', url: 'https://github.com/Didanrama/Task-Lambda-Function-CI-CD.git'
            }
        }

        stage('Build and Package') {
            steps {
                script {
                    bat 'powershell -Command "Compress-Archive -Path lambda_function.py -DestinationPath hello-world-didan.zip -Update"'
                }
            }
        }

        stage('Update Lambda Function') {
            steps {
                script {
                    bat """
                        aws lambda update-function-code \
                        --function-name ${LAMBDA_FUNCTION_NAME} \
                        --zip-file fileb://hello-world-didan.zip \
                        --region ${AWS_REGION}
                    """
                }
            }
        }
    }

    post {
        success {
            echo 'Lambda function updated successfully!'
        }
        failure {
            echo 'Failed to update the Lambda function.'
        }
    }
}
```
Untuk script kurang lebih fungsinya sama seperti di tipe Freestyle Project yakni mengubah file lambda_function.py menjadi file zip yang kemudian akan di upload ke Lambda Function.

* Selanjutnya kita coba untuk agar saat kita ubah kode di github otomatis langsung mengubah kode pada Lambda tanpa harus kita klik Build Now di Jenkinsnya dengan menggunakan Webhook Github. Kita memerlukan nama domain public untuk dipasang nanti di Webhook Github, jadi saya menggunakan Ngrok untuk mengubah localhost menjadi bisa public. Hasilnya seperti ini

![image](https://github.com/user-attachments/assets/5a321cb1-abaa-4fbe-adfa-6142f866f1c3)

* Kemudian kita setting Webhook Githubnya, berikut adalah settingan yang digunakan

![image](https://github.com/user-attachments/assets/2c02ea64-baaa-406f-8ffa-fd40cf9b10e4)

* Kita setting juga pada Jenkins yakni centang GitHub hook trigger for GITScm polling, yang berfungsi untuk agar Jenkins dapat menerima push hook dari Github

![image](https://github.com/user-attachments/assets/ef8a95a9-061b-40ed-a9e9-b9a89fba84b5)

* Terakhir kita lakukan percobaan

https://github.com/user-attachments/assets/43ba1e95-d255-4368-90fd-00709abc0741

### Terima Kasih

*Made By Didan Ramadhan*


