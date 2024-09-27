[[Estudos]][[Alura]]

As variáveis de ambiente têm niveis diferentes.

### Variáveis de Usuário
Muitos apps e scripts personalizáveis usam varáveis de ambeinte especificas do usuário para armazenar confgs personalizadas, como preferência de cores, atalhos teclado e config de inicialização.

### Variáveis Globais do Sistema
Os adms de sistemas frequentemente usam variáveis de ambients globais para definir configs globais que afetam todos os user do sistema. 

Isso pode incluir configs de rede, configs de segurança e parâmetros de incialização.

### Variaveis de ambientes Windows

Acessando a barra de busca> "variaveis"> "editar variaveis de ambiente para sua conta"

### Variaveis de ambiente no Linux e Mac

Em sistemas Unix (que englobam tanto Linux quanto MacOs), a config de varáveis de ambiente ocorre editando um arquivo de texto.

1. abra o terminal> ```nano~/.bashrc``` 
2. Ao final do arquivo deve digitar:
3. ```export nomeDaVariavel=valorDaVariavel```
4. Fazendo substituições necessárias, adicionei as seguintes variaveis :
5. ```export MINHA_SENHA=senhaAplicacao
6. Salve o arquivo e volte no terminal, para que as mudanças seja aplicadas, digite o comando:
7. ```source~/.bashrc```
8. POdemos ver nossas variaveis de ambiente, digitando:
9. ```printenv```

### Variaveis de ambiente no IntelliJ

- Configuraiton edit > enviromnet variables> e aponta suas variaveis com seus valores atribuidos

- No código aponte um deva ser substituido com ${nomeVariabel}

![[Pasted image 20240927160158.png]]
