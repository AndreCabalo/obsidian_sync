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


## Parei no vídeo PRIMEIRO WORKFLOW

