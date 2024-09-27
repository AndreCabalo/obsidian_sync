[[Estudos]]
Se ao tentar iniciar o mysql docker atraves do comando :
```
docker start mysql
```

E dar o erro:

```
Error response from daemon: driver failed programming external connectivity on endpoint mysql (73da438e27e20ce897d4eb1045dfcec964e33a40c1fb42a9e6e0424f6b7fe5c7): failed to bind port 0.0.0.0:3306/tcp: Error starting userland proxy: listen tcp4 0.0.0.0:3306: bind: address already in use
```

Damos:

```
sudo lsof -i :3306

```

E se apontar que tem um na porta, rodamos:

```
sudo systemctl stop mysql
```

e depois iniciamos novamente o container com:

```
docker start mysql
```

