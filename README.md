# Домашнее задание к занятию 9.2 «Система мониторинга Zabbix»

### Задание 1 

Установите Zabbix Server с веб-интерфейсом.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия что есть в системном репозитороии Debian 11
3. Пользуясь конфигуратором комманд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache
4. Выполните все необходимые команды для установки Zabbix Server и Zabbix Web Server

#### Требования к результаты 
1. Прикрепите в файл README.md скриншот авторизации в админке
![](https://github.com/VolkovMixail/9.2-Zabbix/blob/main/img/adminkaZabbix.jpg)
2. Приложите в файл README.md текст использованных команд в GitHub
На Сервере
* apt update upgrade
*  apt update && apt upgrade
*  wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
*  dpkg -i zabbix-release_6.4-1+debian11_all.deb
*  apt update
*  apt install postgresql
*  apt update
*  apt install zabbix-server-pgsql zabbix-frontend-php php7.4-pgsql zabbix-nginx-conf zabbix-sql-scripts zabbix-agent2
*  sudo -u postgres createuser --pwprompt zabbix
*  sudo -u postgres createdb -O zabbix zabbix
*  zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix
*  nano /etc/zabbix/zabbix_server.conf
*  systemctl restart zabbix-server.service
*  systemctl status zabbix-server.service
*  nano /etc/zabbix/nginx.conf
*  systemctl restart nginx.service
*  systemctl status nginx.service
---

### Задание 2 

Установите Zabbix Agent на два хоста.

#### Процесс выполнения
1. Выполняя ДЗ сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 виртмашины, одной из них может быть ваш Zabbix Server
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera
5. Проверьте что в разделе Latest Data начали появляться данные с добавленных агентов

#### Требования к результаты 
1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу
![](https://github.com/VolkovMixail/9.2-Zabbix/blob/main/img/hosts.jpg)
2. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.
![](https://github.com/VolkovMixail/9.2-Zabbix/blob/main/img/monitor.jpg)
3. Приложите в файл README.md текст использованных команд в GitHub
На Хостовых машинах
*  apt update
*  apt upgrade
*  wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
*  dpkg -i zabbix-release_6.4-1+debian11_all.deb
* apt update
*  apt install zabbix-agent2 zabbix-agent2-plugin-*
*  systemctl status zabbix-agent2.service
*  ip a
*   nano /etc/zabbix/zabbix_agent2.conf
*  systemctl restart zabbix-agent2.service
*   systemctl status zabbix-agent2.service
*   nano /etc/zabbix/zabbix_agent2.conf

