SE O SQL BUGAR:

verificar se tem algum container rodando:

```
docker ps
```

verificar se tem alguem na porta 3306:

```
sudo lsof -iTCP:3306 -sTCP:LISTEN
```

Parar a aplicação forçadamente:

```
sudo kill <NUMERO PID>
```

Não esqueça de remover o container existente com:

```
docker container rm mysql 
```

Inicie um novo com:

```
docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=cart mysql:9.0.1
```

pode ser tbm o comando a seguir, para criar o banco sem nenhum nome :

```
docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root mysql:latest
```