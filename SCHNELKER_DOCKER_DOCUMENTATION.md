    Eric Schnelker
    Codi West
    System Administration
    12/18/2023
## <ins><p style="text-align: center;"> Docker -- Install Documentation</ins></p>
1. #### Installed Ubuntu on VMWare Workstation
  * ###### Used Ubuntu’s website and downloaded latest stable .iso
------------------------------------------
2. #### Updated Ubuntu software and packages to latest versions
------------------------------------------
3. #### Installed Docker through terminal
  * ###### Installed docker-compose package as well
  * ###### Note: docker-compose-plugin does not exist in Ubuntu's latest LTS, it's just docker-compose
  * ##### Using guide: https://www.atlantic.net/vps-hosting/install-wordpress-with-docker-on-ubuntu/#:~:text=Install%20WordPress%20with%20Docker%20on%20Ubuntu%201%20Step,6%20Step%206%20%E2%80%93%20Access%20WordPress%20Interface%20
------------------------------------------
4. #### Checked docker version and made sure it is up-to-date
  * ###### Checked version of docker-compose as well
------------------------------------------
5. #### Downloaded MariaDB image
  * ###### Used sudo docker pull mariadb
------------------------------------------
6. #### Created file structure for wordpress
  * ###### Made directory /wordpress using mkdir ~/wordpress
  * ###### Made two subdirectories /wordpress/database and /wordpress/html using mkdir -p
------------------------------------------
7. #### Created a MariaDB Container with name wordpressdb
  * ###### Used sudo docker run -e MYSQL_ROOT_PASSWORD=root-password -e MYSQL_USER=wpuser -e MYSQL_PASSWORD=password -e MYSQL_DATABASE=wpdb -v /root/wordpress/database:/var/lib/mysql --name wordpressdb -d mariadb
------------------------------------------
8. #### Checked IP of MariaDB container
  * ###### Used docker inspect -f '{{ .NetworkSettings.IPAddress }}' wordpressdb
------------------------------------------
9. #### Installed MariaDB core tools (including mySQL)
  * ###### Used sudo apt install mariadb-client-core-10.6
------------------------------------------
10. #### Connected to the MariaDB container
  * ###### Used mysql -u wpuser -h 172.17.0.2 -p
------------------------------------------
11. #### Verified the database
  * ###### Used show databases;
  * ###### Exited container using EXIT;
------------------------------------------   
12. #### Download wordpress image
  * ###### Used sudo docker pull wordpress:latest
------------------------------------------
13. #### Created a wordpress container named wpcontainer
  * ###### Used docker run -e WORDPRESS_DB_USER=wpuser -e WORDPRESS_DB_PASSWORD=password -e WORDPRESS_DB_NAME=wpdb -p 8081:80 -v /root/wordpress/html:/var/www/html --link wordpressdb:mysql --name wpcontainer -d wordpress
------------------------------------------
14. #### Installed curl using sudo apt install curl
------------------------------------------
15. #### Verified wordpress container using curl -I localhost:8081
------------------------------------------
16. #### Configured NGinx as a reverse proxy
  * ###### Installed NGinx using sudo apt-get install nginx -y
  * ###### Created a new Nginx virtual host configuration file using sudo nano /etc/nginx/sites-available/wordpress with the content: server  listen 80;  server_name wp.example.com;  location /  proxy_pass http://localhost:8081;  proxy_set_header Host $host;  proxy_set_header X-Real-IP $remote_addr;  proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    * ###### Note: Removed brackets from above config file to avoid issues with markdown. 
  * ###### Activated the virtual host using sudo ln -s /etc/nginx/sites-available/wordpress /etc/nginx/sites-enabled/
  * ###### Restarted the Nginx service to apply the changes
------------------------------------------
