# SOC282 - Phishing Alert - Deceptive Mail Detected

EventID : 257  
Event Time : May, 13, 2024, 09:22 AM  
Rule : SOC282 - Phishing Alert - Deceptive Mail Detected  
Level : Security Analyst  
SMTP Address : 103.80.134.63  
Source Address : free@coffeeshooop.com  
Destination Address : Felix@letsdefend.io  
E-mail Subject : Free Coffee Voucher  
Device Action : Allowed  


## Проверка на virustotal  

Проверяем IP-адрес сервера SMTP и видим что 9/91 вендоров пометили этот адрес как вредоносный. Так же можно заметить, что адрес связан с фишингом как в нашем случае

<img width="1888" height="690" alt="image" src="https://github.com/user-attachments/assets/1707c4c3-429b-4db1-8bd2-dd472fd9140e" />


## Проверка почты

В письме в первую очередь обращаем внимание на домен @coffeeshooop.com, подозрительно, что тут одна лишняя буква o. Во вторых, в письме можем заметить архивированный файл, что очень подозрительно, почему купон на бесплатный кофе в зип файле еще и с паролем infected. Так же в обычном фишинге злоумышленники пытаются надавить на жертву разными способами, например, торопить как в нашем случае.

<img width="1178" height="726" alt="image" src="https://github.com/user-attachments/assets/7e6c7306-37e8-4548-891d-b63b615ef533" />

## Endpoint security

В этом разделе в истории браузера мы можем увидеть, что пользователь все таки открыл этот файл и злоумышленник получил доступ. Дальше в истории терминала видно, что он начал изучать окружение

<img width="911" height="267" alt="image" src="https://github.com/user-attachments/assets/3376971e-3382-4262-b941-42916f6ac2e4" />
<img width="836" height="461" alt="image" src="https://github.com/user-attachments/assets/315728c2-86b1-40e3-8c55-0a32b82abe28" />

##  Log management

По логам мы можем увидеть, что злоумышленник подключился к адресу 37.120.233.226. Злоумышленник собрал данные и передал их на сервер через подозрительный порт, что очень похоже на С2

<img width="1645" height="364" alt="image" src="https://github.com/user-attachments/assets/9122b627-ac0e-42a9-a745-e7498c1db7f3" />
<img width="484" height="329" alt="image" src="https://github.com/user-attachments/assets/3e1db28b-59ff-4015-acb7-4d9df209fbcf" />


Проверим этот IP-адрес на VirusTotal и по комментариям мы модем понять, что это точно С2. Нам нужно изолировать хост и эскалировать этот инцидент на L2

<img width="1823" height="736" alt="image" src="https://github.com/user-attachments/assets/60d895df-e070-4be0-87c7-74c59f05feee" />
<img width="836" height="549" alt="image" src="https://github.com/user-attachments/assets/b0039bfa-4b91-477b-8c9d-3bda9b756d97" />

## Playbook




