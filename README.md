docker-compose -f docker-compose-ubuntu-zabbix-psql-nginx.yml up -d

Change the zabbix-agent interface for zabbix-server to use DNS "zabbix-agent" (docker interface)

## Zabbix
http://<host_ip>

Admin/zabbix

## Grafana
http://<host_ip>:3000

admin/admin
