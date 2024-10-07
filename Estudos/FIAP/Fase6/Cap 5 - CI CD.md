[[Estudos]] [[FIAP]]

### Processo sem CD

Os desenvovledores estão na extremidade esquerda deste espectro e o pessoal de operações está na extremidade receptora.
Ha um atraso em cada entraga que leva a equipes frutadas e clientes insatisfeitos.

![[Pasted image 20240930152900.png]]

### Processo com CD

Com a pipeline de entrega contínua os desenvolvedores escrevem o código do seu laptop, confirmam as mudanças para um repositório de código-fonte, como GITHUB.

![[Pasted image 20240930153556.png]]


# Criando imagem docker

Constroi a imagem usando Dockerfile presente no diretório atual e marca com a tag api:

```
docker build -t api
```

Para executar app, o container é iniciado a partir de imagem construida, com configuração de rede e variáveis de ambiente específicas que controlam os detalhes da conexão ao banco de dados e o perfil da aplicação

```
	docker run -p 8080:8080 --net=host \
	-e PROFILE=prd \
	-e DATABASE_URL=jdbc:mysql://localhost:3306/api?createDatabaseIfNotExist=true \
	-e DATABASE_USER=root \
	-e DATABASE_PWD=1234 \
	api
```

# Docker File

	
	`FROM maven:3.9.8-eclipse-temurin-21 AS build`
	`RUN mkdir /opt/app`
	`COPY . /opt/app`
	`WORKDIR /opt/app`
	`RUN mvn clean package`
	`FROM eclipse-temurin:21-jre-alpine`
	`RUN mkdir /opt/app`
	`COPY --from=build  /opt/app/target/app.jar /opt/app/app.jar`
	`WORKDIR /opt/app`
	`ENV PROFILE=prd`
	`EXPOSE 8080`
	`ENTRYPOINT ["java", "-Dspring.profiles.active=${PROFILE}", "-jar", "app.jar"]`

Explicando o DOCKER FILE

	# Dockerfile com Comentários

```dockerfile
# Define a imagem base para a construção da aplicação usando Maven e JDK Eclipse Temurin
FROM maven:3.9.8-eclipse-temurin-21 AS build

# Cria um diretório onde o código da aplicação será armazenado
RUN mkdir /opt/app

# Copia todos os arquivos do diretório atual para o diretório na imagem
COPY . /opt/app

# Define o diretório de trabalho para os próximos comandos
WORKDIR /opt/app

# Executa o Maven para limpar e empacotar a aplicação
RUN mvn clean package

# Inicia uma nova fase de construção com uma imagem leve do JRE
FROM eclipse-temurin:21-jre-alpine

# Cria o diretório onde o arquivo JAR será armazenado
RUN mkdir /opt/app

# Copia o arquivo JAR gerado na fase de construção anterior para o novo contêiner
COPY --from=build /opt/app/target/app.jar /opt/app/app.jar

# Define o diretório de trabalho novamente na nova imagem
WORKDIR /opt/app

# Define uma variável de ambiente para o perfil da aplicação
ENV PROFILE=prd

# Indica que a aplicação escutará na porta 8080
EXPOSE 8080

# Define o comando que será executado ao iniciar o container
ENTRYPOINT ["java", "-Dspring.profile.active=${PROFILE}", "-jar", "app.jar"]

````

## Build stage:

Utilizamos uma imagem base do Maven para compilar o projeto Java e empacotá-lo em um arquivo JAR

## Runtime Stage

Em seguida partimos de uma imagem base do JRE Alpine para manter a imagem final leve.
O arquivo JAR é copiado para a nova imagem, configurado para rodar no ambiente de produçao.

## Intro ao Github Actions

[Documentação]([Documentação do GitHub Actions - GitHub Docs](https://docs.github.com/pt/actions))

## Componentes

Podemos configurar um fluxo de trabalho, para ser disparado por eventos específicos no seu repo, como abertura de uma solicitação de pull ou a criação de um problema.

Cada trabalho opera em um executor próprio, seja máquina virtual ou um contêiner e inclui várias etapas que executam scripts definidos por vc ou ações , que são extensões reutilizáveis projetadas para simplificar seu processo.

![[Pasted image 20241004204241.png]]

## Fluxo de trabalho

É um processo automatizado configurável que executa um ou mais trabalhos.
Esses são definidos por por um arquivo YAML no diretório .github/workflows de um repo e serão executados quando acionados por uma evento no repo, manualmente ou conforme um cronograma pré definido.

Um repo pode ter múltiplos fluxos de travalho, cada um realizando diferentes tarefas, como:

- Compilar e testar pull requests
- Implantar a aplicação sempre que uma versão for criada.
- Adicionar um rótulo sempre que um novo problema for aberto.
- Podemos tambem referenciar um fluxo de trabalho dentro do outro, aumenta a modularidade e a reutilização das tarefes.

## Eventos
São atividades específicas no repo que disparam a execução de um fluxo de trabalho

## Trabalhos
Um trabalho é um conjunto de etapas dentro de um fluxo de trabalho, todas executadas no mesmo executor.
Cada etapa consiste em um script de shell ou uma ação predefinida que é executada
Estas etapas são executas em sequência e cada um depende da conclusão da anterior para o seu ínicio.

## Ações
Uma ação é um aplicativo personalizado dentro da plataforma github actions, projetado para executar tarefas complexas que são frequentemente necessárias nos processos de desenvolvimento.

Use uma ação para minimizar a quantidade de código repetido.

Além de construir suas próprias ações vc, pode explorar uma variedade de ações predefinadas disponíveis no github marketplace.

## Executores

É um servidor dedicado que processo seus fluxos de trabalho assim que são acionados.
Cada executor é capaz de gerenciar um único trabalho por vez, garantindo que cada tarefa receba os recursos necessários para sua execução.

O github oferece um gama de executores padrão, incluindo sistemas operacionais como UBUNTO LINUX, MACOS, WINDOWS, para acomodas a diversidade de fluxos de trabalhos.

Cada tarefa dentro de um fluxo de trabalho é realizada em um máquina virtual recém provisionada e isolada, garantindo um ambiente limpo e controlado para cada execução.


# Github Personal Acess Token

Icone com foto na page do github > settings > developer settings> personal access tokens > classic > generate new token classic:

xxxxxxxxxxxxxxxxx

Esse token é essencial para garantir operações seguras e automatizadas, como git push e git pull, em repos remotos.

Este token substitui a autenticação tradicional com user e password, proporcionando um método mais seguro e controlável de acesso ao github.


# Primeiro Workflow

Vamos detalhas como definir e executar um workflow inicial no githubactions, composto por dois jobs distintos, ambos executando em um ambiente UBUNTO.

Comece acessando o terminal, clonando o reposit''orio e configurando suas credenciais com os seguintes comandos:

```
git clone https://github.com/antonioclj/simple-api-java.git
cd simple-api-java
git config user.email "seuemail@dominio.com"  
git config user.name "Seu Nome"
```


## PRIMEIRO WORKFLOW

1. GIT Clonando repo
2. GIT Config user email
3. GIT Config user name 
4. Cria branch com base na checkout
5. GIT push para subir o local para remoto

6. Criar pasta na raiz do projeto ".github/workflows"
7. Nesta pasta criamos um novo arquivo "meu-primeiro-workflow.yaml" ou .yml
8. Colamos o codigo:

```
	on: push
	jobs:
	    job1-hello:
	        runs-on: ubuntu-latest
	        steps:
	        - name: Imprimir mensagem
	          run: echo "Olá, Mundo"
	    job2-goodbye:
	        runs-on: ubuntu-latest
	        steps:
	        - name: Step 1 - Sequencia de instruções
	          run: |
	            echo "Uma nova instrução"
	            ls            
	        - name: Step 2 - Imprimir mensagem
	          run: echo "Até logo!" 
```

1. O código a cima diz:

```
	on: push                                  SEMPRE QUE FOR DADO UM PUSH
	jobs:
	    job1-hello:
	        runs-on: ubuntu-latest            RODA UM SERVIC OP UBUNTO
	        steps:
	        - name: Imprimir mensagem         NAME DO STEP
	          run: echo "Olá, Mundo"          INSTRUC DO STEP
	    job2-goodbye:
	        runs-on: ubuntu-latest
	        steps:
	        - name: Step 1 - Sequencia de instruções
	          run: |
	            echo "Uma nova instrução"
	            ls            
	        - name: Step 2 - Imprimir mensagem
	          run: echo "Até logo!" 
```

1. Adicionar o item para o git com git add .
2. git commit para adicionar as modificações
3. git push
4. Inserir senha do personal acess token
5. Abrir o browser e navegar até o repositório
6. Voltar no código e adiconar um name na primeira linha do arquivo .yaml

	1. name: Meu primeiro workflow

7. git add .
8. git commit -m 
9. git push
10. Acessar repositorio remoto pelo navegador
11. Na aba action temos os workflows
12. Click em um dos jobs
13. Expanda e verá que ao expandir ele executara os comandos.

##  Componentes do Workflow

1. **Name** - Não é explicitamente mostrado neste arquivo YAML, mas geralmente é definido no topo do arquivo para identificar o workflow dentro do github.
2. **On** -	ESta chave define o evento que dispara o workflow. No exemplo fornecido, o worrkflow é ativado por qualquer ação de push no repositório.
3. **Jobs** - Esta secção contém as definições dos jobs que serão executados quando o workflow for disparado. Cada job pode ser configurado para rodar em diferentes ambientes ou executores.
	1. **job1-hello**: Este job roda no ambiente ubunto-latest e possui uma única etapa que executa o comando para imprimir 'Olá Mundo"
	1. **job2-goodbye**: Este job tamém roda um ubunto-latest e é composto por duas etapas. A primeira executa um sequência de comandos que inclui imprimir uma msg e listar arquivos no diretório atual, enquanto a segundo imprime um "Até logo!"

## Workflow de eventos filtrados

1. Podemos configurar que pushes em branches com prefixo FREATURE disparem jobs de testes unitários, enquanto os pushes em branches DEVELOP acionem apenas jobs de validação do container.

2. O Github Actions permite que workflows sejam configuradas para serem disparadas por evento em branches específicas.

### Passos:

1. Na branch develop
2. git pull -r
3. criar nova branch com git checkout -b feature/filtra
4. criar branch no repo remoto com git push ou segundo a orientação por exemplo:
	1. git push --set-upstream origin nomeDaBranch
5. senha do personal acess token

### Criar Workflow

1. criar a pasta .github/workflows
2. criar o arquivo 02-workflow-filtro.yaml
3. colar o script:

```
	name: 02 - Workflow Filtro
	on:
	  push:
	    branches: 'feature/**'    EXECUTADO COM PREFIXO FEATURE/QUALQUERCOISA
	jobs:
	  echo:
	    runs-on: ubuntu-latest
	    steps:
	      - name: Exibir o evento
	        run: echo "Workflow disparado por ${{ github.event_name }}"
```

1. adicionando o arquivo com git add.
2. git commit
3. git push
4. No browser acesse o repo remoto, clique em action
5. Localiza seu workflow, clique sobre ele

## Ações Pré-Configuradas