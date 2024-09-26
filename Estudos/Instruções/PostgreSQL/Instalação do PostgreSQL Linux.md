### Baixar as atualizações e infos dos pacotes de todas as fontes
```sudo apt update```

### Instalar as atualizações disponiveis atualmente no sitema
```sudo apt upgrade```

### Instalar o postgresql
```sudo apt install postgresql-12``` 

### Verificar o status (deve estar rodando)
```sudo service postgresql stats```

### Se não estiver enable, ativar com o seguinte comando:
```sudo sistemctl enable postgresql.service```

### Após estar enable start o serviço 
```sudo systemctl start postgresql.service```

### Acessando postgre
```sudo -u postgres psql```

### Alterando user e password
```ALTER USER postgres PASSWORD 'meupassword';```

### CTRL+ D , CTRL + D ,  Para fechar
