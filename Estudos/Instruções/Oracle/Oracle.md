[[Estudos]]
docker ```
docker run -d --name oracle-db -p 1521:1521 -e MYSQL_ROOT_PASSWORD=storeproductsubr

-e MYSQL_DATABASE=cart mysql:9.0.1

```

`docker run --name cl-database -d -p 1521:1521 -e ORACLE_PASSWORD=oracle repo.intranet.pags/customer-docker/circularization-letter/cl-database`

docker run -d -p 1521:1521 -e ORACLE_PASSWORD=oracle gvenzl/oracle-xe
