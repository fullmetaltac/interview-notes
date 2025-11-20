## Install sandbox db with docker


```shell
# download postgres docker image:
docker pull postgres
# build and run postgres container
docker run -d --name pg -p 5432:5432 -e POSTGRES_PASSWORD=secret postgres
# create dvdrental db
docker exec -i pg psql -h localhost -U postgres -c "CREATE DATABASE dvdrental;"
# populate db with data from the backup file
docker exec -i pg pg_restore -U postgres -v -d dvdrental < dvdrental.tar
# run sample queries
docker exec -i pg psql -h localhost -U postgres -d dvdrental \
 -c "SELECT first_name, last_name FROM customer LIMIT 2;"
```

```shell
# output
 first_name | last_name
------------+-----------
 Jared      | Ely
 Mary       | Smith
(2 rows)
```
```shell
# or use interactive session
docker exec -it pg psql -h localhost -U postgres -d dvdrental
```

<p align="center">
    <img src="images/db-diagram.png" width="60%"> 
</p>