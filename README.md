# Домашнее задание к занятию "`Система мониторинга Zabbix `" - `Болов Кантемир`



### Задание 1

Установите Zabbix Server с веб-интерфейсом.

**Процесс выполнения**

1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите PostgreSQL. Для установки достаточна та версия, что есть в системном репозитороии Debian 11.
3. Пользуясь конфигуратором команд с официального сайта, составьте набор команд для установки последней версии Zabbix с поддержкой PostgreSQL и Apache.
4. Выполните все необходимые команды для установки Zabbix 
Server и Zabbix Web Server.

**Требования к результатам**

1. Прикрепите в файл README.md скриншот авторизации в админке.

![alt text](<img/Скриншот 07-03-2026 182623.jpg>)
![alt text](<img/Скриншот 07-03-2026 182847.jpg>)

2. Приложите в файл README.md текст использованных команд в GitHub.`


```
sudo apt install postgresql
wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu22.04_all.deb
dpkg -i zabbix-release_latest_7.4+ubuntu22.04_all.deb
apt update
apt install zabbix-server-mysql zabbix-frontend-php zabbix-apache-conf zabbix-sql-scripts zabbix-agent
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix
sudo sed -i 's/# DBPassword=/DBPassword=zabbix_pass/' /etc/zabbix/zabbix_server.conf

```

### Задание 2

`Установите Zabbix Agent на два хоста.`


 Процесс выполнения

1. Выполняя ДЗ, сверяйтесь с процессом отражённым в записи лекции.
2. Установите Zabbix Agent на 2 вирт.машины, одной из них может быть ваш Zabbix Server.
3. Добавьте Zabbix Server в список разрешенных серверов ваших Zabbix Agentов.
4. Добавьте Zabbix Agentов в раздел Configuration > Hosts вашего Zabbix Servera.
5. Проверьте, что в разделе Latest Data начали появляться данные с добавленных агентов.

Требования к результатам

1. Приложите в файл README.md скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу

![alt text](<img/Скриншот 07-03-2026 223559.jpg>)

2. Приложите в файл README.md скриншот лога zabbix agent, где видно, что он работает с сервером

![alt text](<img/Скриншот 07-03-2026 235112.jpg>)
![alt text](<img/Скриншот 07-03-2026 235245.jpg>)
![alt text](<img/Скриншот 07-03-2026 235837.jpg>)

4. Приложите в файл README.md скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные.

![alt text](<img/Скриншот 07-03-2026 233236.jpg>)
![alt text](<img/Скриншот 08-03-2026 000021.jpg>)

5. Приложите в файл README.md текст использованных команд в GitHub

```
sudo apt update
wget https://repo.zabbix.com/zabbix/7.4/release/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_7.4+ubuntu22.04_all.deb
dpkg -i zabbix-release_latest_7.4+ubuntu22.04_all.deb
apt update
sudo apt install zabbix-agent -y
systemctl restart zabbix-agent
systemctl enable zabbix-agent

