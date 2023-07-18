## How to deploy Bold BI and configure startup manually?

```sh
docker run --name boldbi -p 80:80 -p 443:443 \
     -e APP_URL=https://example.com \
     -e OPTIONAL_LIBS=mongodb,mysql,influxdb,snowflake,oracle,clickhouse,google \
     -e widget_bing_map_enable=true\
     -e widget_bing_map_api_key=<widget_bing_map_api_key> \
     -e AppSettings__CustomSizePDFExport=false \
     -e AppSettings__BrowserTimezone=false \
     -v boldbi_app_data:/application/app_data \
     -v boldbi_nginx_data:/etc/nginx/sites-available \
     -d syncfusion/boldbi
```
  ![advance-command](/docs/images/advance-command.png)

* Refer [this](../README.md#environment-variables-and-its-usage) table to learn more about environment variable.<br>
* After running the command, you can access the Bold BI App by entering `APP_URL` in a browser. To know more about APP_URL, follow this [APP_URL](/README.md#app_url-guidance) Guidance.
* To know more about application startups, refer [here](#application-startup).



## How to use host path as Persistent Volume?

```sh
docker run --name boldbi -p 80:80 -p 443:443 \
     -e APP_URL=<app_base_url> \
     -e OPTIONAL_LIBS=<optional_library_names> \
     -e widget_bing_map_enable=<true/false>\
     -e widget_bing_map_api_key=<widget_bing_map_api_key> \
     -e AppSettings__CustomSizePDFExport=<true/false> \
     -e AppSettings__BrowserTimezone=<true/false> \
     -v <host_path_for_appdata_files>:/application/app_data \
     -v <host_path_for_nginx_config>:/etc/nginx/sites-available \
     -d syncfusion/boldbi
```
![advance-command](/docs/images/advance-command-volume-path.png)

* Refer [this](/docs/environment-variable.md#environment-variables-and-its-usage) table for environment variable.<br>
* After running the command, you can access the Bold BI App by entering `APP_URL` in a browser. To know more about application startups, refer [here](#application-startup).

### Persisting application data

You can store the application data in your host machine to make the Bold BI container a stateful application. Bold BI application will read and write the data in your host machine.
 
Replace the `<host_path_for_appdata_files>` value with a directory path from your host machine in the advanced docker run command.

> **For example**<br/>
> Windows: `-v D:/boldbi/app_data:/application/app_data`<br/>
> Linux: `-v /home/boldbi/app_data:/application/app_data`

### Nginx configuration

You can mount a host directory to the Bold BI container for maintaining the Nginx configuration. You can also store SSL certificates in this directory and can configure Nginx with them.

Replace the `<host_path_for_nginx_config>` value with a directory path from your host machine in the advanced docker run command.

> **For example**<br/>
> Windows: `-v D:/boldbi/nginx:/etc/nginx/sites-available`<br/>
> Linux: `-v /home/boldbi/nginx:/etc/nginx/sites-available`

Once, the Bold BI container started to run, you can check the directory in your host machine. The `boldbi-nginx-config` file will be generated there. You can configure the Nginx inside the container using this file.

## How to deploy Bold BI using Branding variable?

Refer [this](/docs/environment-variable.md#environment-variables-for-configuring-branding-in-backend) table to provide the environment variable with Branding deployment.

```sh
docker run --name boldbi -p 80:80 -p 443:443 \
      -e APP_URL=<app_base_url> \
      -e OPTIONAL_LIBS=<optional_library_names> \
      -e widget_bing_map_enable=<true/false>\
      -e widget_bing_map_api_key=<widget_bing_map_api_key> \
      -e BOLD_SERVICES_UNLOCK_KEY=<Bold_BI_license_key>  \
      -e BOLD_SERVICES_DB_TYPE=<data_base_server_type>  \
      -e BOLD_SERVICES_DB_HOST=<data_base_server_host> \
      -e BOLD_SERVICES_DB_PORT=<data_base_server_port> \
      -e BOLD_SERVICES_DB_USER=<data_base_user_name> \
      -e BOLD_SERVICES_DB_PASSWORD=<data_base_server_password> \ 
      -e BOLD_SERVICES_DB_NAME=<excisting_data_base_name> \
      -e BOLD_SERVICES_POSTGRESQL_MAINTENANCE_DB=<maintenance_db_name> \
      -e BOLD_SERVICES_USER_EMAIL=<Bold_BI_user_email> \
      -e BOLD_SERVICES_USER_PASSWORD=<Bold_BI_user_password> \ 
      -e BOLD_SERVICES_BRANDING_MAIN_LOGO=<branding_image_url> \
      -e BOLD_SERVICES_BRANDING_LOGIN_LOGO=<branding_image_url> \
      -e BOLD_SERVICES_BRANDING_EMAIL_LOGO=<branding_image_url> \
      -e BOLD_SERVICES_BRANDING_FAVICON=<branding_image_url> \
      -e BOLD_SERVICES_BRANDING_FOOTER_LOGO=<branding_image_url> \
      -e BOLD_SERVICES_SITE_NAME=<site_name> \
      -e BOLD_SERVICES_SITE_IDENTIFIER=<site_identifier_name> \
      -v <host_path_for_appdata_files>:/application/app_data \
      -v <host_path_for_nginx_config>:/etc/nginx/sites-available \
      -d syncfusion/boldbi

<b>Example for with Branding variable deployment</b>

```sh
docker run --name boldbi -p 80:80 -p 443:443 \
     -e APP_URL=https://example.com \
     -e OPTIONAL_LIBS=mongodb,mysql,influxdb,snowflake,oracle,clickhouse,google \
     -e widget_bing_map_enable=true\
     -e widget_bing_map_api_key=<widget_bing_map_api_key> \
     -e BOLD_SERVICES_UNLOCK_KEY=<Bold_BI_license_key>  \
     -e BOLD_SERVICES_DB_TYPE=<data_base_server_type_Eg: mssql, mysql and postgresql>  \
     -e BOLD_SERVICES_DB_HOST=localhost \
     -e BOLD_SERVICES_DB_PORT=5432 \
     -e BOLD_SERVICES_DB_USER=boldbi-user \
     -e BOLD_SERVICES_DB_PASSWORD=boldbi@123 \ 
     -e BOLD_SERVICES_DB_NAME=bold-services \
     -e BOLD_SERVICES_POSTGRESQL_MAINTENANCE_DB=<maintenance_db_name> \
     -e BOLD_SERVICES_USER_EMAIL=admin@boldbi.com \
     -e BOLD_SERVICES_USER_PASSWORD=Admin@123 \ 
     -e BOLD_SERVICES_BRANDING_MAIN_LOGO=https://cdn.boldbi.com/wp/pages/boldbi-header-menu-logo.svg \
     -e BOLD_SERVICES_BRANDING_LOGIN_LOGO=https://cdn.boldbi.com/wp/pages/boldbi-header-menu-logo.svg \
     -e BOLD_SERVICES_BRANDING_EMAIL_LOGO=https://cdn.boldbi.com/wp/pages/boldbi-header-menu-logo.svg \
     -e BOLD_SERVICES_BRANDING_FAVICON=https://cdn.boldbi.com/wp/pages/boldbi-header-menu-logo.svg \
     -e BOLD_SERVICES_BRANDING_FOOTER_LOGO=https://cdn.boldbi.com/wp/pages/boldbi-header-menu-logo.svg \
     -e BOLD_SERVICES_SITE_NAME=bold-dashboards \
     -e BOLD_SERVICES_SITE_IDENTIFIER=branding \
     -v D:/boldbi/app_data:/application/app_data \
     -v D:/boldbi/nginx:/etc/nginx/sites-available \
     -d syncfusion/boldbi
```



## Application Startup

Configure the Bold BI On-Premise application startup to use the application. Please refer to the following link, for more details on configuring the application startup.

https://help.boldbi.com/embedded-bi/application-startup