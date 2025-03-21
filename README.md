# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Заярченко Ивана`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

Установите Zabbix Server с веб-интерфейсом.

### Процесс выполнения
Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
1. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
2. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
3. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server.
Требования к результаты
1. Прикрепите в файл README.md скриншот авторизации в админке.
2. Приложите в файл README.md текст использованных команд в GitHub.

### Ответ.
Команды использованные при установке  Zabbix Server:

`wget https://repo.zabbix.com/zabbix/7.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.0+ubuntu24.04_all.deb
 dpkg -i zabbix-release_latest_7.0+ubuntu24.04_all.deb
 apt update`

`apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts`

`sudo -u postgres createuser --pwprompt zabbix
 sudo -u postgres createdb -O zabbix zabbix`

`zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix`

`sudo nano /etc/zabbix/zabbix_server.conf`

`systemctl restart zabbix-server zabbix-agent apache2
 systemctl enable zabbix-server zabbix-agent apache2`

 
![Zabbix Dashboards](https://github.com/vonoid/HW_Zabbix_1/blob/18f8bdce94e4cd0fda1ddac94beec39d1ac3a1ec/img/Zabbix_login.jpg)


---

### Задание 2

Установите Zabbix Agent на два хоста.

### Процесс выполнения
1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результаты

1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером
3. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
4. Приложите в файл README.md текст использованных команд в GitHub

### Ответ.

Cкриншот раздела Configuration > Hosts
![Hosts](https://github.com/vonoid/HW_Zabbix_1/blob/cb88030b32a04de5bd908f11de5f4452ace1c0eb/img/Hosts.jpg)

Cкриншот лога zabbix agent виртуальной машины №1
![LogTest1](https://github.com/vonoid/HW_Zabbix_1/blob/cb88030b32a04de5bd908f11de5f4452ace1c0eb/img/logAgent1.jpg)

Cкриншот лога zabbix agent виртуальной машины №2
![LogTest2](https://github.com/vonoid/HW_Zabbix_1/blob/cb88030b32a04de5bd908f11de5f4452ace1c0eb/img/logAgent2.jpg)

Скриншот раздела Monitoring > Latest data для виртуальной машины №1
![MonitoringTest1](https://github.com/vonoid/HW_Zabbix_1/blob/cb88030b32a04de5bd908f11de5f4452ace1c0eb/img/MonitoringTest1.jpg)

Скриншот раздела Monitoring > Latest data для виртуальной машины №2
![MonitoringTest2](https://github.com/vonoid/HW_Zabbix_1/blob/cb88030b32a04de5bd908f11de5f4452ace1c0eb/img/MonitoringTest2.jpg)
