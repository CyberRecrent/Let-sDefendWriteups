# SOC257 - VPN Connection Detected from Unauthorized Country  
Event ID: 225  
Event Time: Feb 13, 2024, 02:04 AM  
Rule: SOC257 - VPN Connection Detected from Unauthorized Country  
Level: Security Analyst  
Source Address: 113.161.158.12  
Destination Address: 33.33.33.33  
Destination Hostname: Monica  
Username: monica@letsdefend.io  
Alert Trigger Reason: VPN connection detected from an unauthorized country  
URL: https://vpn-letsdefend.io  



## Проверяем IP-адрес на VirusTotal и AbuseIPDB  

Тут мы видим, что на IP-адрес было 4651 репорт, но все равно он зеленый  


<img width="640" height="516" alt="image" src="https://github.com/user-attachments/assets/ddaeeae7-e17c-40a1-ae6b-61d6280eb985" />  


Однако ниже мы можем заметить, что последний репорт был год назад. IP-адрес был замечен в ssh brute-force атаках.  


 <img width="1276" height="803" alt="image 1" src="https://github.com/user-attachments/assets/04eebaf0-8952-4603-8146-903d42045a06" />  
 

 В VirusTotal данный IP-адрес находится в категории подозрительных, вредоносных. 7 из 91 вендоров пометили этот адрес как вредоносный.  
 

 <img width="1901" height="735" alt="image 2" src="https://github.com/user-attachments/assets/e39c0b1b-20cf-4861-a62e-f4462537cbe9" />  
 

 В комментариях мы также можем заметить, что данный IP-адрес был замечен на ssh brute-force  
 
 
 <img width="1837" height="427" alt="image 3" src="https://github.com/user-attachments/assets/ff59c765-2dc2-4180-9aac-7398047b6833" />  


 

 ## Log management  


 Указал в фильтрах подозрительный IP-адрес. В логах мы можем заметить 21 событие с этого IP-адреса до момента алерта и все соединения идут с одного адреса за короткий промежуток времени. Destination порты разные, включая 443  


 <img width="515" height="76" alt="image 4" src="https://github.com/user-attachments/assets/9d530492-49cd-4b13-9081-8e8edbc14b7c" />  
 

 <img width="1572" height="706" alt="image 5" src="https://github.com/user-attachments/assets/62da0cac-62d4-49c9-8127-57f7b6871608" />  
 

 Предлагаю посмотреть последний лог перед алертом. Тут я вижу, что была попытка соединения, но не удалось пройти двухфакторную аутентификацию потому что ввели неправильный одноразовый код. Таких логов было еще 2 до этого. Предлагаю посмотреть почту, может Моника сама просила код.  


<img width="417" height="385" alt="image 6" src="https://github.com/user-attachments/assets/ddbfec6e-5c72-408d-b915-3cf61ad1d15a" />  


## Email security


Указываю почту Моники и можем заметить 3 письма от отдела безопасности с одноразовыми кодами, но не одного от самой Моники, что указывает, что атакующий пытался подключиться к VPN, но не смог пройти MFA. Успешного входа не было  


<img width="1632" height="352" alt="image 7" src="https://github.com/user-attachments/assets/e3dd3514-dc38-47d5-b4e6-4bf5ff88e49d" />  



## Endpoint security


Почти точно я уверен, что это была неудачная атака, но давайте проверим в Endpoint security. Отфильтровав процессы видно, что подозрительной активности не обнаружено - все процессы стандартные системные

<img width="1230" height="634" alt="image 8" src="https://github.com/user-attachments/assets/99b02d48-9b19-4163-af49-bb9744b45932" />  



## Закрытие алерта  


Алерт был true positive. Тип инцидента:  Несанкционированный доступ (Unauthorized Access).  IP-адрес принадлежит внешней сети. Репутация IP-адреса: вредоносный. Критически важные системы не пострадали. Риска утечки данных нет. Изоляция устройства не нужна.  


<img width="1264" height="392" alt="image 9" src="https://github.com/user-attachments/assets/8b57b113-cd34-4617-a7dd-e6d089fbc278" />  


## Заключение  


Атакующий с IP-адреса 113.161.158.12 (Вьетнам) был помечен как 7/91 вендорами на VirusTotal, пытался войти в VPN под учетной записью monica@letsdefend.io. Было зафиксировано 21 соединение в промежутке 1:54-2:03 13 февраля 2024 года. Система отправила 3 OTP кода, но атакующий не смог пройти двухфакторную аутентификацию. Успешного входа не зафиксировано. Verdict: True Positive  










 



