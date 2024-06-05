# This Repo contians solution to some of the docker compose issue.

## `depends_on` property:
- Sometimes, even after using the `depensds_on` property, out next continer is started because, depends on command by default check wether cotainer is running or not.
  > Usually in contianers like mysql, MariaDB, etc container started up, but their service need time to start up completely.
  > in that case, Container is running without proper intialization of service, casue error in dependent container.
- Solution is to set up, healthcheck property on container: `healthcheck.sh` designed by MariaDB to implement healthcheck.
  ```
  services:
    mariadb:
      image: mariadb:latest
      env:
        MARIADB_ALLOW_EMPTY_ROOT_PASSWORD: true
        MARIADB_MYSQL_LOCALHOST_USER: 1
        MARIADB_MYSQL_LOCALHOST_GRANTS: USAGE
      ports:
        - 3306
      healthcheck:
        test: [ "CMD", "healthcheck.sh", "--su-mysql", "--connect", "--innodb_initialized" ]
        start_period: 1m
        interval: 1m
        timeout: 5s
        retries: 3
  ```
- Edit `depends_on` parameter for dependent container:
  ```
  depends_on:
      rabbit:
        condition: service_healthy
  ```
  > So, Now on contaier will, start only when required container up and running with healthy health status.



# Healthcheck for `mysql` container.
```
healthcheck:
      test: ["CMD", "mysqladmin" ,"ping", "-h", "localhost"]
      timeout: 20s
      retries: 10
```
- Depends on functions:
```
depends_on:
    rabbit:
      condition: service_healthy
```
## Referances:
https://stackoverflow.com/questions/31746182/docker-compose-wait-for-container-x-before-starting-y
https://mariadb.org/mariadb-server-docker-official-images-healthcheck-without-mysqladmin/
https://github.com/peter-evans/docker-compose-healthcheck
https://mariadb.com/kb/en/using-healthcheck-sh/
https://stackoverflow.com/questions/42567475/docker-compose-check-if-mysql-connection-is-ready
