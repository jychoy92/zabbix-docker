docker-compose -f docker-compose-ubuntu-zabbix-psql-nginx.yml up -d

## Zabbix
http://<host_ip>

Admin/zabbix

## Grafana
http://<host_ip>:3000

admin/admin

## Zabbix-Server's Zabbix Agent
Change the zabbix-agent interface for zabbix-server to use Docker DNS "zabbix-agent"
![image](https://user-images.githubusercontent.com/83763465/130350449-f5f08b5e-d383-4d40-8d99-87383d55ea36.png)

## Install Zabbix Plugin in Grafana
```
docker container exec -it <container_name> bash
grafana-cli plugins install alexanderzobnin-zabbix-app
exit
docker-compose -f docker-compose-ubuntu-zabbix-psql-nginx.yml restart
```
![image](https://user-images.githubusercontent.com/83763465/130351264-1b8f07c8-90f6-40b7-9c37-9f47126351e6.png)
