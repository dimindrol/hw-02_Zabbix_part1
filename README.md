# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Пергунов Д.В`

### Задание 1

1. Процесс установки описан в коде и дополнительно прикреплены скриншоты

```
# Добавление репозитория postgres
sudo sh -c 'echo "deb https://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list'

# Импорт ключа репозитория
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -

# Обновление пакетов
sudo apt-get update

#Настройка локализации
sudo locale-gen "en_US.UTF-8"
sudo dpkg-reconfigure locales

#Установка Postgres и Apache, добавление в автозапуск
apt -y install postgresql-client-13 postgresql-13
pg_createcluster 13 main --start
systemctl enable --now postgresql

sudo apt install apache2
systemctl enable --now apache2


nano /etc/postgresql/13/main/postgresql.conf
#Разкоментировал строку: listen_addresses = 'localhost'

nano /etc/postgresql/13/main/pg_hba.conf
#Добавил строку
host    zabbix          zabbix          127.0.0.1/32            trust
systemctl restart postgresql

# Установили Zabbix сервер, веб-интерфейс
wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.0-4+ubuntu22.04_all.deb
dpkg -i zabbix-release_6.0-4+ubuntu22.04_all.deb
apt update
apt install zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts

#Создали БД
sudo -u postgres createuser --pwprompt zabbix
sudo -u postgres createdb -O zabbix zabbix

#На хосте Zabbix сервера импортировали начальную схему и данные
zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

#Настроили базу данных для Zabbix сервера
nano /etc/zabbix/zabbix_server.conf
DBPassword=zabbix

#Перезагрузили и настроили автозапуск
systemctl restart zabbix-server apache2
systemctl enable zabbix-server apache2

```

Скриншоты 

![Название скриншота 1](https://github.com/dimindrol/hw-02_Zabbix_part1/blob/ff3cdf483706a8b8915dd35b507730b14adea9f7/img/zabbix1.png)`

![Название скриншота 1](https://github.com/dimindrol/hw-02_Zabbix_part1/blob/ff3cdf483706a8b8915dd35b507730b14adea9f7/img/zabbix2.png)`

![Название скриншота 1](https://github.com/dimindrol/hw-02_Zabbix_part1/blob/ff3cdf483706a8b8915dd35b507730b14adea9f7/img/zabbix3.png)`

---

### Задание 2

`Приведите ответ в свободной форме........`

1. Установили Zabbix агент на два хоста и настроили хосты
2. Настроили хосты подключили шаблоны


```
# Установили заббикс агент
sudo apt-get install zabbix-agent

#Отредактировали файл
sudo nano /etc/zabbix/zabbix_agentd.conf
#Прописали Source IP 127.0.0.1 для хоста с заббикс сервером IP 192.168.0.5 для стороннего хоста

# Добавляем в автозагрузку и перезапускаем
systemctl restart zabbix-agent
systemctl enable zabbix-agent
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`


---

### Задание 3

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`

### Задание 4

`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота](ссылка на скриншот)`
