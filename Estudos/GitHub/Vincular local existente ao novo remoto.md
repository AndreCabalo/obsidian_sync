[[Estudos]]
Podemos iniciar um repositório remoto lá no próprio git hub
Em seguida construir meu código aqui localmente
Quando eu quiser vincular meu local ao remoto existente, preciso fazer os seguintes passos:

Dentro do meu projeto local:

# Iniciar o repositório local
```
Git init
```

# Adicionar o conteúdo local no repositório local

```
git add .
```

# Commit localmente

```
git commit -m "comentario qualquer"
```

# Criar branch principal

```
git branch -M main
```

# Vincular local ao projeto remoto

```
git remote add origin hhtps:github.com/nome/repositorioname.git
```

# Push local para remoto

```
git push -u origin main
```
