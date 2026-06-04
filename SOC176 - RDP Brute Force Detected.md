# SOC176 - RDP Brute Force Detected

EventID : 234  
Event Time : Mar, 07, 2024, 11:44 AM  
Rule : SOC176 - RDP Brute Force Detected  
Level : Security Analyst  
Source IP Address : 218.92.0.56  
Destination IP Address : 172.16.17.148  
Destination Hostname : Matthew  
Protocol : RDP  
Firewall Action : Allowed  
Alert Trigger Reason : Login failure from a single source with different non existing accounts  

## Проверка IP-адреса на VirusTotal и AbuseIPDB  
  
На скриншоте мы видим, что на VirusTotal этот адрес помесен как подозрительный, вредоносный. В комментариях сообщества были замечены брутфорс атаки с этого адреса 

<img width="1753" height="935" alt="image" src="https://github.com/user-attachments/assets/96fa868f-4364-4384-ac29-a4e3882fdf85" />  
  
На abuseIPDB на этот адрес было 453.031 репортов и находится в категории ssh brute-force. В нашем случае как раз был алерт на брут-форс  

<img width="1304" height="722" alt="image" src="https://github.com/user-attachments/assets/c629d05b-4ab1-4810-9096-f4574cf16cf2" />  


## Log managment

Давайте посмотрим были ли соединения с этого адреса. Тут мы можем заметить 30 соединений и все в одно время в Mar, 07, 2024, 11:44 AM, что указывает на брут-форс.  

  <img width="1595" height="590" alt="image" src="https://github.com/user-attachments/assets/cba3e1c2-3c4d-402f-9ca9-dd564e9d9497" />  

На скриншоте снизу видно, что перебирали аккаунты и все таки получилось подключиться через аккаунт Мэтью. Аккаунт Мэтью нужно срочно изолировать  

<img width="1592" height="440" alt="image" src="https://github.com/user-attachments/assets/918b5a54-c294-4ad1-ac30-e2a38c3aa673" />  

## Endpoint security  

Проверим, что успел сделать атакующий за аккаунт Мэтью. В разделе истории терминала я вижу, что атакующий зашел в командную строку, проверил текущего пользователя, изучил учетные записи и посмотрел активные покдлючения.   

  <img width="975" height="459" alt="image" src="https://github.com/user-attachments/assets/9bc766f9-1ca8-4fe9-8262-86a3064b8597" />  

В истории процессов можно увидеть, что атакующий проверил списки администраторов, все что он делал в терминале  

  <img width="1218" height="428" alt="image" src="https://github.com/user-attachments/assets/4de06fa8-6ed4-45d6-a456-56221579161d" />  

## Playbook  

ip атакующего был внешний, не внутренний. Ip - адрес был вредоносным и был в категории брут форса ( 8/91 вендоров пометили его как вредоносный на VirusTotal, но на abuseIPDB на этот адрес было 453,051 репортов).
В log management было 30 соединений от атакующего IP за короткий промежуток времени, что указывает на брут-форс. Хост Мэтью нужно изолировать.  

<img width="1018" height="341" alt="image" src="https://github.com/user-attachments/assets/5b02851b-be5b-4ef8-a252-76ea577e4a6f" />  




## Заключение  

Вердикт: True Positive. Нужно изолировать хост Мэтью. Эскалация на 2 уровень - активный взлом  












