# Домашнее задание к занятию "`Система мониторинга Zabbix`" - `Осаковская Анна`

---

### Задание 1

`1. Cкриншот авторизации в интерфейсе админке Zabbix`

<img width="1581" height="857" alt="Снимок экрана zabbix admin" src="https://github.com/user-attachments/assets/8f4b0e0f-c697-4d8d-963f-c4033e8ed205" />


`2. Текст использованных команд`

```
sudo apt install -y postgresql postgresql-contrib
sudo systemctl enable postgresql
sudo -u postgres psql -c "CREATE USER zabbix WITH PASSWORD 'zabbix' SUPERUSER; CREATE DATABASE zabbix OWNER zabbix;"

wget https://repo.zabbix.com/zabbix/6.4/ubuntu/pool/main/z/zabbix-release/zabbix-release_6.4-1+ubuntu22.04_all.deb
sudo dpkg -i zabbix-release_6.4-1+ubuntu22.04_all.deb
sudo apt update

sudo apt install -y zabbix-server-pgsql zabbix-frontend-php php8.1-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent

zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix

sudo systemctl restart apache2
sudo systemctl start zabbix-server
sudo systemctl enable zabbix-server
sudo systemctl start zabbix-agent
sudo systemctl enable zabbix-agent

```
---

### Задание 2

1. `Скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу`
<img width="1618" height="867" alt="Zabbix aggents" src="https://github.com/user-attachments/assets/c3d04d36-7008-420c-a46e-0c6feffa4826" />

2. `Скриншот лога zabbix agent, где видно, что он работает с сервером`
<img width="847" height="449" alt="agent_log" src="https://github.com/user-attachments/assets/03378ab2-733f-4386-8db5-0582002a8db5" />

3. `Скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные`
<img width="1618" height="838" alt="agents_data" src="https://github.com/user-attachments/assets/bb4a39a7-af30-4358-aa93-9d8b136818fb" />

`4. Текст использованных команд для установки zabbix-agent`

```
#Установка на сервере VM1

sudo apt install -y zabbix-agent

sudo sed -i 's/^Server=.*/Server=127.0.0.1,192.168.1.221/; s/^ServerActive=.*/ServerActive=127.0.0.1,192.168.1.221/; s/^Hostname=.*/Hostname=Zabbix server/' /etc/zabbix/zabbix_agentd.conf

sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent

#Установка на клиенте VM2

wget https://repo.zabbix.com/zabbix/6.4/debian/pool/main/z/zabbix-release/zabbix-release_6.4-1+debian11_all.deb
sudo dpkg -i zabbix-release_6.4-1+debian11_all.deb
sudo apt update

sudo apt install -y zabbix-agent

sudo sed -i '/^Server=/d; /^ServerActive=/d; /^Hostname=/d; $a\Server=192.168.1.221\nServerActive=192.168.1.221\nHostname=Debian_host' /etc/zabbix/zabbix_agentd.conf

sudo systemctl restart zabbix-agent
sudo systemctl enable zabbix-agent

```
---

### Задание 3 *

`Задание 3 не выполнялось`

