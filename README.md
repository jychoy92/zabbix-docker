# Compose the containers :smiling_face_with_three_hearts:
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

# Grafana - Add Datasource (Zabbix Postgres SQL)
![image](https://user-images.githubusercontent.com/83763465/130351548-d9263593-3d44-4ea0-8c02-2eaebc4fa72d.png)
|Item|Default Value|Remark|
|-------------|-------------|-------------|
|Host|postgres-server:5432|Use Docker Network DNS|
|Database|zabbix|refer to .env_db_pgsql|
|User|zabbix|refer to .POSTGRES_USER|
|Password|zabbix|refer to .POSTGRES_PASSWORD|

# (Optional) Grafana - Install Zabbix Plugin
Zabbix Plugin is not necessary but is good to have as it will help to get better query perfomance rather than just the SQL DB datasource. 
```
docker container exec -it <container_name> bash
grafana-cli plugins install alexanderzobnin-zabbix-app
exit
docker-compose -f docker-compose-ubuntu-zabbix-psql-nginx.yml restart
```
![image](https://user-images.githubusercontent.com/83763465/130351264-1b8f07c8-90f6-40b7-9c37-9f47126351e6.png)

Enable the Zabbix Plugin
![image](https://user-images.githubusercontent.com/83763465/130352088-80764336-ac22-47cd-a2d7-016e600f76d8.png)


## (Optional) Grafana - Add Datasource (Zabbix Plugin) 
### Create a dedicated API user in Zabbix 
|Item|Value|
|----|----|
|Username|grafana-api|
|Group|No access to the frontend|
|Permission Role|User Role|

<img src="https://user-images.githubusercontent.com/83763465/130352607-0a6393d0-4aea-4ca7-acc4-1875122cb16b.png" width="40%"> <img src="https://user-images.githubusercontent.com/83763465/130352683-36d6bbda-2bc1-4767-bc28-1dcbd206374b.png" width="40%" >
![image](https://user-images.githubusercontent.com/83763465/130353457-9999fc19-4273-4aa1-b423-ab6df875a133.png)

### Add Zabbix Plugin DataSource
<img src="https://user-images.githubusercontent.com/83763465/130353543-22740c77-0bc2-4ddf-b743-c174d519bb4c.png" width="40%" >
__http://<zabbix_url>/api_jsonrpc.php__


