[[Pagbank]]

### Dependências
Time Tucuman - Para autorização do script migration para alteração no banco de dados

### Dúvidas acessos

##### Para ambiente de desenvolvimento local, mas falha
Sigo as instruções:
	- Navegue até seu workspace: `cd ~/workspace/store-promotion/docker`
	- Inicie o ambiente: `docker-compose up --build -d`
	- MAS não temos nenhum docker-compose
##### Migrations falhando:

No readme dizem para rodar o comando
	`./gradlew databaseMigration -Dserver=[AMBIENTE]`
	
Por tanto coloquei:
	`./gradlew databaseMigration -Dserver=local`
	
E recebo essa exceção:
	
`FAILURE: Build failed with an exception.`
<<<<<<< HEAD
=======

* `What went wrong:`
`Could not initialize class org.codehaus.groovy.runtime.InvokerHelper`
> `Exception java.lang.NoClassDefFoundError: Could not initialize class org.codehaus.groovy.reflection.ReflectionCache [in thread "Daemon worker"]`

* `Try:`
`Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.`

* `Get more help at https://help.gradle.org`

##### Como acessar o banco local do store promotion?

Segui a url do applicaiton-local da store-promotion-packager
	Pórem ao tentar acessar o banco aparece o erro: 
		Access denied for user 'root'@'172.30.35.182' (using password: NO)


### Duvidas sobre as tabelas de Store Promotion
>>>>>>> 0b3a780b7d9536df20b36a3651e50b8c3c05b858

* `What went wrong:`
`Could not initialize class org.codehaus.groovy.runtime.InvokerHelper`
> `Exception java.lang.NoClassDefFoundError: Could not initialize class org.codehaus.groovy.reflection.ReflectionCache [in thread "Daemon worker"]`

* `Try:`
`Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.`

* `Get more help at https://help.gradle.org`

##### Como acessar o banco local do store promotion?

Segui a url do applicaiton-local da store-promotion-packager
	Pórem ao tentar acessar o banco aparece o erro: 
		Access denied for user 'root'@'172.30.35.182' (using password: NO)


### Duvidas sobre as tabelas de Store Promotion

1. Podemos usar a tabela PROMOTION ou a MOBI_PROMOTION(replica do legado) para armazenar as promoções especiais que iremos tirar do feature-gateway?

2. Possui um campo COD_BC_CONTRACT (que podemos apagar?)

3. No type, podemos setar se é especial?

	![[TPromotion.png]]

### Dúvidas sobre featuregateway

Como excluir a lista de promoções especiais de la?
<<<<<<< HEAD
=======



>>>>>>> 0b3a780b7d9536df20b36a3651e50b8c3c05b858
## Passos para desenvolvimento:

1. Criar um scrip no migration para adicionar um tabela ou usar uma tabela atual
2. Pedir aprove do Tucumam , tanto para alterar um tabela existente ou para criar nova
3. Criar uma entity/dto para representar a tabela e colunas
	1. Nome
	2. Flag active
	3. Data criação
	4. Data atualização
	5. Criar método para verificar se ela é especial ou não.
4. Remover ou renomear o featuregatewayServiceImpl e seu metodo que busca se uma promocao é valida.


### Resumo sobre o trecho que irei operar

[Conteúdo falando do fluxo que irei alterar ao verificar lista do featuregateway](https://jiraps.atlassian.net/wiki/spaces/GRE/pages/75318461273/Elegibilidade)

Em resumo a uma lista de promoções no feature-gateway, ao verificar a elegibilidade de um cliente a uma promoção, se ela constar na lista de promos especiais, a elegibilidade terá algumas regras(Consulta o feature-toogle na verificação.):

Foi passado código MGM na request?
SE NÃO, consulta o feature-toggle para saber se é uma promoção especial.
	SE NAO for uma consulta especial, é uma promoção comum, por tanto elegivel
	SE SIM, verifica se a promoção é DEFAULT
		SE NÃO, então não é elegivel!
		SE SIM,  dispara threads para ambas verficações:
			Verifica se possui algum transacao no ultimo 180 dias
			Verifica se o contrato atual é Default (consultando o API de Business Contract)
			SE AMBOS TRUE, é elegivel
			SE ALGUM FOR FALSE, Inelegivel.
SE SIM, consulta a API do MGM para verificar se é elegivel utilizando o código passado

<<<<<<< HEAD

## Quem usa o feature gateway para validar promoções especiais?

### End-points

Interface PromotionV1
Classe PromotionV1Impl - eligiblePromotion
Endpoint: [**/v1/promotions/{promotionName}/eligible**](https://store-promotion-api.qa.intranet.pags/swagger-ui.html#/operations/promotion-v-1-impl/eligiblePromotionUsingGET "https://store-promotion-api.qa.intranet.pags/swagger-ui.html#/operations/promotion-v-1-impl/eligiblePromotionUsingGET")

#### Interface
Promotion-core>core>service>FeatureGatewayService

### Classe 
Promotion-core>core>service>impl>FeatureGatewayServiceImpl

- Método isSpecialPromotion(String promotionName)

### Classe que usa
Promotion-core>core>service>impl> PromotionEligibleServiceImpl

- Método chooseEligibilityStrategy
=======
>>>>>>> 0b3a780b7d9536df20b36a3651e50b8c3c05b858



