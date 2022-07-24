1. создайте виртуальную машину c Ubuntu 20.04 LTS (bionic) в GCE типа e2-medium в default VPC в любом регионе и зоне, например us-central1-a
-- создал 
![image](https://user-images.githubusercontent.com/45406197/180643629-ec4c47c6-d27f-4b57-906d-3c80a3397e09.png)
2. поставьте на нее PostgreSQL 14 
--команда sudo apt update && sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y -q && sudo sh 
-c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && wget 
--quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo 
apt-key add - && sudo apt-get update && sudo DEBIAN_FRONTEND=noninteractive apt -y install postgresql-14
3. проверьте что кластер запущен
-- ![image](https://user-images.githubusercontent.com/45406197/180643687-d595c2d2-840e-4572-b731-a4747347cba6.png)
4.зайдите из под пользователя postgres в psql и сделайте произвольную таблицу с произвольным содержимым
-- ![image](https://user-images.githubusercontent.com/45406197/180643707-87cd35f8-4cdb-4333-99aa-7a9ff24b91d4.png)
5.остановите postgres
--![image](https://user-images.githubusercontent.com/45406197/180643719-33c3fbce-60ff-458a-bcc2-6c14b4b1d378.png)
6. создайте новый standard persistent диск GKE через Compute Engine -> Disks в том же регионе и зоне что GCE инстанс размером например 10GB
-- ![image](https://user-images.githubusercontent.com/45406197/180643732-75fb7c5d-eca1-4cda-b218-8d7918f21a13.png)
7. проинициализируйте диск согласно инструкции и подмонтировать файловую систему
--![image](https://user-images.githubusercontent.com/45406197/180643755-b7c190ff-e9d5-423f-b677-7dede52eb6d6.png)
--![image](https://user-images.githubusercontent.com/45406197/180643768-8b6ccd63-f34c-496d-92ee-ccf941b4b509.png)
--![image](https://user-images.githubusercontent.com/45406197/180643786-e8e5f372-e17f-480e-9770-466471ceab05.png)
8.сделайте пользователя postgres владельцем
--![image](https://user-images.githubusercontent.com/45406197/180644454-c2df01b0-2ee4-47d8-b03c-b230e97f259d.png)
9.перенесите содержимое /var/lib/postgres/14 в /mnt/data
--![image](https://user-images.githubusercontent.com/45406197/180644482-95bf9c48-93b7-45b4-93ba-3cd54525fe70.png)
10.попытайтесь запустить кластер
--не запускается
![image](https://user-images.githubusercontent.com/45406197/180644537-bbd6a46d-3de7-4b98-ac60-1d2fec48f9a3.png)
11.задание: найти конфигурационный параметр в файлах раположенных в /etc/postgresql/10/main
--параметр который поменял в конфиге
![image](https://user-images.githubusercontent.com/45406197/180644591-d2e79937-9305-41df-934f-1c424f6194cb.png)
путь
![image](https://user-images.githubusercontent.com/45406197/180644609-26a3145f-dd77-4e42-a1d5-f6c2f54d6138.png)
12. попытайтесь запустить кластер
--![image](https://user-images.githubusercontent.com/45406197/180644660-d0064adb-fae7-4678-b593-013b20965fdd.png)
13. зайдите через через psql и проверьте содержимое ранее созданной таблицы
--![image](https://user-images.githubusercontent.com/45406197/180644678-003b4ef0-dd89-413f-83fd-1dd4314e86d5.png)

