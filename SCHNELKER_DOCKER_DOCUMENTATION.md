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
    * ##### Using guide: https://github.com/docker/awesome-compose/blob/master/official-documentation-samples/wordpress/README.md
------------------------------------------
4. #### Checked docker version and made sure it is up-to-date
    * ###### Checked version of docker-compose as well
------------------------------------------
5. #### Created a wordpress directory using mkdir
    * ###### cd into that directory
------------------------------------------
6. #### Created docker-compose.yml file
    * ###### Followed the documentation and pasted the sample content for the .yml file
------------------------------------------
7. #### Used docker compose up -d, which pulls the needed Docker images, and starts the wordpress and database containers.
------------------------------------------
8. #### Pulled up localhost:80 in FireFox, which brought up the WordPress startup wizard.
------------------------------------------
9. #### Completed WordPress startup wizard
------------------------------------------
