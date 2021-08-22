# Compose the container
docker-compose -f docker-compose-ubuntu-zabbix-psql-nginx.yml up -d

# Files-Keys References
| File  | References |
| ------------- | ------------- |
| .env_agent  | Zabbix Agent Environment Variables |
| .env_db_pgsql  | Postgres SQL Environment Variables  |
| .env_srv  | Zabbix Server Environment Variables  |
| .env_web  | Web Server Environment Variables  |
| .POSTGRES_USER  | Postgres SQL User  |
| .POSTGRES_PASSWORD  | Postgres SQL Password  |

** you can change all these environment variable accordingly. **

## Default Postgres SQL USERNAME/Password
|username|Password|
|-------------|-------------|
|zabbix|zabbix|

# Zabbix Grafana Portal Access
|Portal|URL|Default Username|Default Password|
|-------------|-------------|-------------|-------------|
|Zabbix|http://<host_ip>|Admin|zabbix|
|Grafana|http://<host_ip>:3000|admin|admin|

# Configure Zabbix Agent in Zabbix Server
Change the zabbix-agent interface for zabbix-server to use Docker DNS "zabbix-agent"
![image](https://user-images.githubusercontent.com/83763465/130350449-f5f08b5e-d383-4d40-8d99-87383d55ea36.png)

# Install Zabbix Plugin in Grafana
```
docker container exec -it <container_name> bash
grafana-cli plugins install alexanderzobnin-zabbix-app
exit
docker-compose -f docker-compose-ubuntu-zabbix-psql-nginx.yml restart
```
![image](https://user-images.githubusercontent.com/83763465/130351264-1b8f07c8-90f6-40b7-9c37-9f47126351e6.png)

# Grafana - Connect to Postgres SQL
![image](https://user-images.githubusercontent.com/83763465/130351548-d9263593-3d44-4ea0-8c02-2eaebc4fa72d.png)

