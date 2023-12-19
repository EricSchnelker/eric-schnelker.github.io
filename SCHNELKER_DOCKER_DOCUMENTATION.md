    Eric Schnelker
    Codi West
    System Administration
    12/18/2023
## <ins><p style="text-align: center;"> Docker -- Install Documentation</ins></p>
1. #### Installed Ubuntu on VMWare Workstation
    * ###### Used Ubuntu’s website and downloaded latest stable .iso
------------------------------------------
2. #### Updated and upgraded Ubuntu software and packages to latest versions
``` bash
      $ sudo apt update
      $ sudo apt upgrade
```
------------------------------------------
3. #### Installed Docker through terminal and Docker Compose
    * ##### Using guide: https://github.com/docker/awesome-compose/blob/master/official-documentation-samples/wordpress/README.md
    * ###### Had to manually install docker compose as docker-compose-plugin was not found
    * ###### Docker:
``` bash
    $ sudo apt install docker.io
```
  * ###### Docker Compose:
``` bash
    $ sudo curl -L https://github.com/docker/compose/releases/download/1.21.0/docker-compose-$(uname -s)-$(uname -m) -o /usr/local/bin/docker-compose
    $ sudo chmod +x /usr/local/bin/docker-compose
    $ sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose
```
------------------------------------------
4. #### Checked docker version and made sure it is up-to-date
``` bash
      $ docker version
```
------------------------------------------
5. #### Created a wordpress directory using mkdir
    * ###### cd into that directory
``` bash
      $ cd my_wordpress/
```
------------------------------------------
6. #### Created docker-compose.yml file
``` bash
      $ sudo nano docker-compose.yml
```
``` yaml
services:
  db:
    # We use a mariadb image which supports both amd64 & arm64 architecture
    image: mariadb:10.6.4-focal
    # If you really want to use MySQL, uncomment the following line
    #image: mysql:8.0.27
    command: '--default-authentication-plugin=mysql_native_password'
    volumes:
      - db_data:/var/lib/mysql
    restart: always
    environment:
      - MYSQL_ROOT_PASSWORD=somewordpress
      - MYSQL_DATABASE=wordpress
      - MYSQL_USER=wordpress
      - MYSQL_PASSWORD=wordpress
    expose:
      - 3306
      - 33060
  wordpress:
    image: wordpress:latest
    volumes:
      - wp_data:/var/www/html
    ports:
      - 80:80
    restart: always
    environment:
      - WORDPRESS_DB_HOST=db
      - WORDPRESS_DB_USER=wordpress
      - WORDPRESS_DB_PASSWORD=wordpress
      - WORDPRESS_DB_NAME=wordpress
volumes:
  db_data:
  wp_data:
```
------------------------------------------
7. #### Pulled the needed Docker images, and starts the wordpress and database containers.
``` bash
    $ docker compose up -d
```
------------------------------------------
8. #### Pulled up localhost:80 in FireFox, which brought up the WordPress startup wizard.
------------------------------------------
9. #### Completed WordPress startup wizard
------------------------------------------
10. #### Admin console screenshot:
    ![admin screenshot](admin_screenshot.png?raw=true "admin screenshot")
------------------------------------------
11. #### Final Product:
    ![Home Screenshot](homepage_screenshot.png?raw=true "home screenshot")

