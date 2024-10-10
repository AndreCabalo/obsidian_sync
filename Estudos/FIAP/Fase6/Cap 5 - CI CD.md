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

![[Pasted image 20241008202736.png]]

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

Disponíveis no marketplace do github [Marketplace (github.com)](https://github.com/marketplace?type=actions)

Criamos nova branch, passamos um novo script yaml na pasta github workflow:

```
	name: 03 - Actions
	
	on: 
	    push:
	        branches: "feature/**"
	
	jobs:
	    checkout_java_docker:
	        runs-on: ubuntu-latest
	        steps:            
	            - name: Git Checkout
	              uses: actions/checkout@v4
	
	            - name: Setup Java SDK
	              uses: actions/setup-java@v4
	              with:
	                distribution: 'temurin' 
	                java-version: '21'
	
	            - name: Build
	              uses: docker/build-push-action@v6
	              with:
	                push: false                    
	
	            - name: Executar scripts
	              run: |
	                git branch
	                java --version 
	                mvn clean package
```

Onde:
	no step Git Checkout, usamos a actions "actions/checkout@v4"
	no step Setup Java, usamos a actions "actions/setup-java@v4"
	no step Build, usamos o uses "docker/build-push-actiont@v6"
	A seguir executamos o script para ver a versão do java e comando maven que limpa e empacota a aplicação java

Com isso adiconamos no nosso github e comitamos, damos push por final.
Indo no repositorio pelo navegador, temos a aba actions, onde podemos ver a execução do serviço em cada etapa.

# Azure e Docker Hub

Acessar [Docker Hub Container Image Library | App Containerization](https://hub.docker.com/?_gl=1*z69foj*_gcl_au*MTgwNTA3MzQwMS4xNzI3NzQwNTE4*_ga*NzczMDAzMzkzLjE3Mjc3NDA1MjE.*_ga_XJWPQMJYHQ*MTcyODM0NDQzMC4zLjEuMTcyODM0NDQzNi41NC4wLjA.)
Create repository > de o name e deixe como public.

## Criar token no dockerhub
- Clique no perfil > account settings > personal acess token> generate new token
- De um nome e deixa opção de permissão READ & WRITE
- Copie o comando docker login..no terminal teste o comando e em password cole o token

## Azure criando resource group

Acesse Azure [Página inicial - Microsoft Azure](https://portal.azure.com/#home)
Pesquise por resource groups ou grupo de recursos> criar

## Criar banco de dados MYSQL no Azure

Pesquise no Azure por MYSQL Flexibe server ou Servidor Flexivel
Criação rápida
![[Pasted image 20241007205913.png]]
seguir> aguardar o deployment

## Criar webApp na Azure

Pesquisar por APP SERVICE
Create WebApp> 

![[Pasted image 20241007210518.png]]

Não criaremos banco de dados>
Em container:
![[Pasted image 20241007210711.png]]
Em network, mantenha acesso publico
Em monitoramento e segurança, mantenha os valores
Em tags, mantenha os valores
Avance para create e clique em create, a aplicação esta sendo submetida a deploymente da aplicação.

Com isso nosso banco mysql esta rodando e nossa aplicação tbm, vc pode consutlar isso pesquisando por MYSQL para ver o banco e pesquisar serviço de aplicativos para ver o app em execução.

## Configurações de app acesso a banco de dados

![[Pasted image 20241007211240.png]]
[fiap-simple-java-api - Microsoft Azure](https://portal.azure.com/#@fiap.com.br/resource/subscriptions/6da110e7-2136-474e-9f25-1fe885121da1/resourceGroups/rs-fiap-on/providers/Microsoft.Web/sites/fiap-simple-java-api/appServices)

Acesse configurações variáveis de ambiente
Indo na IDE em resourcer da aplicação teremos application-xx.properties
![[Pasted image 20241007211736.png]]

### Variavel de profile
Com isso vamos em add (azure variavel de ambiente)
	Nome = PROFILE
	Valor = dev
Aplicar

### Variavel banco
DATABASE_URL = bd-fiap-api-dev-andre.mysql.database.azure.com

![[Pasted image 20241007212146.png]]
Cole esse valor neste intervalo na sua IDE:

![[Pasted image 20241007212339.png]]
Copie desde JDBC até o final para jogarmos no na variavel de ambiente da Azure
Coloque as demais variaveis de ambiente, como:
	Database_USER = fiap
	Database_PWD = Azure1992!
	WEBSITES_PORT = 8080                 (Definido no compose)


# Script de Continuos Integration (CI)

Tarefas
	Teste unitários
	Validação de código
	Coberturas de código
	
Cria as pastas .github/workflows na raiz do projeto
Crie o arquivo "continuos_integration.yaml"
Cole o seguinte código:

```
name: Continuous Integration  
on:  
  pull_request:  
    branches:  
      - develop  
jobs:  
  tests:  
    runs-on: ubuntu-latest  
    steps:  
      - name: Git Checkout  
        uses: actions/checkout@v4  
  
      -   name: Setup Java SDK  
          uses: actions/setup-java@v4  
          with:  
            distribution: 'temurin'  
            java-version: '21'  
      -   name: Unit tests  
          run: mvn test
            
```

Executado sempre em pull requests da branch Develop
Git checkout, setup java e os tests
git add. commit e push
criamos outra branch, enviamos ela para remoto 
e fazemos uma PR para a develop
e ao tentar mergear deve passar pelo teste ccriado com workflow:

![[Pasted image 20241007223604.png]]
Apenas se aprovado, poderemos mergear!
Caso falhe, não será permitido seguir com a PR!

# Script de Continuos Delivery (CD)

## Config de segurança
Azure no nosso webApp (encontrado em app service)
Achando o projeto, vamos em settings, configurações>
SCM Basic Publishing Credentials para ON


Acesse Deployment> Deployment Center> Manage Publish Profile, Download Profile (faça o download em sua pasta de preferencia)

Abra este arquivo com o editor, vera que ele é uma composição XML.
Copie o conteudo do arquivo (iremos colar no github)

Acesse o repositorio> Settings > Security > Actions
Criar New Repository Secret>
	name - DOCKERHUB_USERNAME
	secret - seu nome no dockerhub (andrecabalo)
Criar New Repository Secret>
	name - DOCKERHUB_TOKEN
	secret - cole sua secret criada no dockerhub
Criar New Repository Secret>
	name - AZURE_PROFILE
	secret - cole o conteudo do arquivo que baixamos no passo ali em cima do download profile azure

## Criaremos nosso workflow de continuos delevery
Ir para branch develop, git pull
Criar novo arquivo continuos_delevery.yaml
Colar o código:
```
on:  
  push:  
    branches:  
      - develop  
  
env:  
  IMAGE_NAME: simple-api-java                  NOME DA IMAGEM NO DOCKERHUB
  AZURE_WEBAPP_NAME: fiap-simple-java-api      NOME DO APP NO AZURE
  
jobs:  
  build:  
    runs-on: ubuntu-latest  
    steps:  
      -  
        name: Git Checkout  
        uses: actions/checkout@v4  
  
      -   name: Setup Java SDK  
          uses: actions/setup-java@v4  
          with:  
            distribution: 'temurin'  
            java-version: '21'  
      -  
        name: Login to Docker Hub  
        uses: docker/login-action@v3  
        with:  
          username: ${{ secrets.DOCKERHUB_USERNAME }}  
          password: ${{ secrets.DOCKERHUB_TOKEN }}  
      -  
        name: Build  
        uses: docker/build-push-action@v6  
        with:  
          push: true  
          tags: ${{ secrets.DOCKERHUB_USERNAME }}/${{ env.IMAGE_NAME }}:latest  
  deploy:  
    runs-on: ubuntu-latest  
    needs: build  
    steps:  
      -  
        name: Deploy to Azure Web App  
        id: deploy-to-webapp  
        uses: azure/webapps-deploy@v2  
        with:  
          app-name: ${{ env.AZURE_WEBAPP_NAME }}  
          publish-profile: ${{ secrets.AZURE_PROFILE }}  
          images: 'github.io/${{ secrets.DOCKERHUB_USERNAME }}/${{ env.IMAGE_NAME }}:latest'

```

Analise se o app-name esta correto, pode seta-lo diretamente
Assim como o campo de images do ultimo step
git add. git commit git push (na develop emm!)
Ve se subiu esse workflow la no repositorio do github


Se tiver algum erro, configura se os token do dockerhub esta correto, se não tiver crie um novo e altere em settings do github em setting? security na variavel dockerhub_token

Acesse o workflow e reforce o inicio do workflow para ver se desta vez ira funcionar

Verifique se a imagem ja foi criada, olhando diretamente no dockerhub, dentro da imagem que ja havia feito

Verifique se o deploy foi feito..

No github olhando o conitnuos delevery, podemos ter acesso a url do deploy e acessa-lo ou se preferir busque por web service, acesse sua aplicação >  overview > em default domain tera a URL de acesso, pórem é preciso completar a URL com :
	`/swagger-ui/index.html`

APARENTEMENTE NÃO FUNCIONOU... MAS SEGUIMOS