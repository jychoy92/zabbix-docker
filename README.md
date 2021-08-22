docker-compose -f docker-compose-ubuntu-zabbix-psql-nginx.yml up -d

Change the zabbix-agent interface for zabbix-server to use Docker DNS "zabbix-agent"

## Zabbix
http://<host_ip>

Admin/zabbix

## Grafana
http://<host_ip>:3000

admin/admin
