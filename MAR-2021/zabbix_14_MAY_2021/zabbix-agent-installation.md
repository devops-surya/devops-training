# ZABBIX-AGENT-INSTALLATION :
## Step 1 – Enable Apt Repository :

* For Ubuntu 18.04 (Bionic):

```
wget https://repo.zabbix.com/zabbix/4.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_4.0-3+bionic_all.deb
sudo dpkg -i zabbix-release_4.0-3+bionic_all.deb
```

* For Ubuntu 16.04 (Xenial):

```
wget https://repo.zabbix.com/zabbix/4.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_4.0-3+xenial_all.deb
sudo dpkg -i zabbix-release_4.0-3+xenial_all.deb
```

## Step 2 – Install Zabbix Agent :

```
sudo apt-get update
sudo apt-get install zabbix-agent
```

## Step 3 – Configure Zabbix Agent:

* sudo vi /etc/zabbix/zabbix_agentd.conf

```
#Server=[zabbix server ip]
#Hostname=[Hostname of client system ]

Server=192.168.1.10
Hostname=Server2
```

## Step 4 – Restart Zabbix Agent:

```
sudo systemctl enable zabbix-agent 
sudo systemctl start zabbix-agent 

sudo systemctl stop zabbix-agent 
sudo systemctl status zabbix-agent
```