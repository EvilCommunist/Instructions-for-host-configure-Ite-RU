# Instructions-for-host-configure-Ite-RU

# Шаг 1: Проверка установленных агентов Zabbix
```
# Polish agents
ls -la /opt | grep zab

# Russian agents
ls -la /etc | grep zab
```
_Вариант 2_<br>
`systemctl status zabb` + `tab`

<strong>Также необходимо убедиться, что на системе ещё не стоит нужный агент, путём проверки наличия разных инстанций SAP</strong><br>
`ls -la /usr/sap | grep -o '[A-Z]\{3\}$'`

# Шаг 2: Установка и настройка заббикс агента версии 2
```
# Repo installation
rpm -Uvh --nosignature https://repo.zabbix.com/zabbix/7.4/release/sles/15/noarch/zabbix-release-latest-7.4.sles15.noarch.rpm
zypper --gpg-auto-import-keys refresh 'Zabbix Official Repository'
# Check if agent is there 
zypper se zabbix-agent2
# Zabbix agent 2 installation
zypper in zabbix-agent2
```
Проверка, установился ли агент `ls -la /etc/zabbix`

_Настройка агента_
```
# Move to zabbix dir
cd /etc/zabbix/
# Configure agent
vim ./zabbix_agent2.conf
```
- Заменить после `Server=127.0.0.1` на IP Zabbix proxy
- Заменить поле `# ListenPort=10050` на `ListenPort=10055`
- Закомментировать `ServerActive=127.0.0.1`
- Заменить `Hostname=Zabbix server` на значение из таблицы
