[[Estudos]]
[[Solução erro do MYSQL DOCKER]]
[[SQL Bugado]]
[[Desinstalar mysql local (conflito com docker mysql)]]


Subir MySQL no docker na porta 3306:3306


```
docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=cart mysql:9.0.1

```

```sudo apt update```


Após confirmar se o `apt` está atualizado podemos fazer a instalação do MySQL.

``` sudo apt install mysql-server 
```


Com isso, podemos verificar se o MySQL está funcionando:

```
service mysql status
```

Caso seja necessário parar o serviço de banco de dados MySQL:

```
sudo service mysql stop
```

E para iniciar o serviço de banco de dados MySQL:

```
sudo service mysql start
```

Caso necessite configurar o MySQL:

```
sudo mysql_secure_installation



