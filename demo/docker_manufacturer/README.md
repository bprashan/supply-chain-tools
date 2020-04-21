## License ##

License agreement is described in Intel OBL Internal Use License.pdf - main directory.

# Manufacturer Toolkit Docker Configuration

## System Requirements

* Operating system: **Linux Ubuntu 18.04**.

* Linux packages:

    `Docker engine (minimum version 18.06.0)`

    `Docker-compose (minimum version 1.23.2)`

* Internet connection

## Instructions

### Get dependent files

If you are working from the Release Package, these files have already been copied to this folder and you need not do anything.

If you are working from the source repository, copy the following sql files from the Supply Chain Tools repository scripts/mysql
folder into this folder.  The manufacturer-webapp*.war file must also be copied here.

Modify mt_config.sql and rt_config.sql following instructions given in the respective files to customize for your environment.

1. manufacturer-webapp*.war
2. mt_create.sql
3. rt_create.sql
4. mt_config.sql
5. rt_config.sql

### Create Java keystore file

See instructions in the Intel Secure Device Onboard Keystore Setup Guide.  Once the file is created, update 
docker-compose.yml to reflect the file name, path and password.  The default configured is /keys/mtk_keystore.p12 and
the default password is 123456.

The manufacturer will not start if the keystore is not present.

### Modify docker-compose.yml configuration as needed
Review the docker-compose.yml file and follow instructions in the file to customize for your environment.

### Modify settings.xml configuration as needed
Edit settings.xml file and add your user and their password.

### Modify tomcat-users.xml configuration as needed
Edit tomcat-users.xml file and add your admin user and their password.

### Start/Stop Docker

* Use the following command to start the docker container.

      $ sudo docker-compose up -d --build

* Use the following command to stop all running docker containers.

      $ sudo docker stop $(sudo docker ps -a -q)

* Use the following command to delete all the docker artifacts. (Note: docker containers must be stopped before deleting
them)
      $ sudo docker system prune -a

Your Docker container is now ready to support DI Protocol and voucher operations.  Additional information is available 
in the Intel Secure Device Onboard Manufacturing Enablement Guide.


