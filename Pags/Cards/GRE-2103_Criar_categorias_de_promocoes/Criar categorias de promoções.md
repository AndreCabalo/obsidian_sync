[[Pagbank]]
# Scrip para criação de tabelas

- [x] Criar script

	`-- 1. CRIAÇÃO DA TABELA CATEGORIA`  
	`CREATE TABLE category (`  
	    `IDT_CATEGORY BIGINT NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '[NOT_SECURITY_APPLY] - IDENTIFICADOR DA CATEGORY',`  
	    `NAM_CATEGORY VARCHAR(50) NOT NULL COMMENT '[NOT_SECURITY_APPLY] - NOME DA CATEGORY'`  
	`);`  
	  
	`-- 2. CRIAÇÃO DA TABELA MOBI PROMOTION CATEGORY`  
	`CREATE TABLE mobi_promotion_category (`  
	    `IDT_CATEGORY BIGINT NOT NULL COMMENT '[NOT_SECURITY_APPLY] - IDENTIFICADOR DA TABELA CATEGORY',`  
	    `IDT_MOBI_PROMOTION INT NOT NULL COMMENT '[NOT_SECURITY_APPLY] - IDENTIFICADOR DA TABELA MOBI PROMOTION',`  
	    `PRIMARY KEY (IDT_CATEGORY, IDT_MOBI_PROMOTION),`  
	    `CONSTRAINT FK_CATEGORY`  
	        `FOREIGN KEY (IDT_CATEGORY) REFERENCES category(IDT_CATEGORY)`  
	        `ON DELETE CASCADE`  
	        `ON UPDATE CASCADE,`  
	    `CONSTRAINT FK_MOBI_PROMOTION`  
	        `FOREIGN KEY (IDT_MOBI_PROMOTION) REFERENCES mobi_promotion(IDT_MOBI_PROMOTION)`  
	        `ON DELETE CASCADE`  
	        `ON UPDATE CASCADE);`

	- Codigo sugerido pelo TUCUMAN

	`-- 1. CRIAÇÃO DA TABELA CATEGORIA`
	`CREATE TABLE store_promotion.category (`
	`IDT_CATEGORY BIGINT NOT NULL AUTO_INCREMENT COMMENT '[NOT_SECURITY_APPLY] - IDENTIFICADOR DA CATEGORY',`
	`NAM_CATEGORY VARCHAR(50) NOT NULL COMMENT '[NOT_SECURITY_APPLY] - NOME DA CATEGORY',`
	`PRIMARY KEY CATEGORY_PK (IDT_CATEGORY)`
	`);`
	
	
	`-- 2. CRIAÇÃO DA TABELA MOBI PROMOTION CATEGORY`
	`CREATE TABLE store_promotion.mobi_promotion_category (`
	`IDT_CATEGORY BIGINT NOT NULL COMMENT '[NOT_SECURITY_APPLY] - IDENTIFICADOR DA TABELA CATEGORY',`
	`IDT_MOBI_PROMOTION INT NOT NULL COMMENT '[NOT_SECURITY_APPLY] - IDENTIFICADOR DA TABELA MOBI PROMOTION',`
	`PRIMARY KEY MOBIPROMCATE_PK (IDT_CATEGORY, IDT_MOBI_PROMOTION),`
	`KEY MOBIPROMCATE_IDX01 (IDT_CATEGORY),`
	`KEY MOBIPROMCATE_IDX02 (IDT_MOBI_PROMOTION),`
	`CONSTRAINT CATEGORY_MOBIPROMCATE_FK FOREIGN KEY (IDT_CATEGORY) REFERENCES category(IDT_CATEGORY),`
	`CONSTRAINT MOBIPROM_MOBIPROMCATE_FK FOREIGN KEY (IDT_MOBI_PROMOTION) REFERENCES mobi_promotion(IDT_MOBI_PROMOTION)`
	`);`
- [x] Testar o migration
- [x] Validação do time
	- [x] ==Necessidade de criação de INDEX? Pergunta do Bruno==
- [x] Validação da Migration com [TUCUMAN](https://jiraps.atlassian.net/servicedesk/customer/portal/150/SDAD-34111)
- [x] Mergear a PR
- [x] Fazer a entrega em QA  [Link JENKINS]([https://jenkins.intranet.pagseguro.uol/job/CUSTOMER_SUCCESS/job/ps-store/job/store-promotion-k8s/](https://jenkins.intranet.pagseguro.uol/job/CUSTOMER_SUCCESS/job/ps-store/job/store-promotion-k8s/ "https://jenkins.intranet.pagseguro.uol/job/customer_success/job/ps-store/job/store-promotion-k8s/"))  - tudo dentro do ps-store- k8s 
	- [x] Build with parameters
	- [x] ![[Pasted image 20241009121056.png]]
- [x] bumpversion MINOR
- [x] Se falhar no SONAR, segue gambiarra:
	- [x] Ir em replay.
	- [x] E alterar o stage SONAR na mão, apagar o stage sonar apagado.
- [x] Merger na Master
- [x] Fazer os msm passos de migração no Jenkins, so database migration prod, bumpversion patch (mas nao faz diferença nenhuma)

# Script  exec DML categorizar especiais 

"blackfridaybasico", "blackfridaysupermaxsmart", "blackfridaysupermaxplus", "blackfridaysupermaxpro", "siteoferta2vistapix00", "siteoferta3multipix00", "siteoferta2vistapix0", "siteoferta3multipix0", "sitesupermaxsmart", "sitesupermaxpro", "sitesupermaxplus", "linkacaomaesplus", "linkacaomaespro", "linkacaomaessmart", "siteoferta4pix0", "siteoferta3pix0", "siteoferta2pix0"


- [x] Ids de promoções especiais:
	710236	blackfridaybasico
	16776	    blackfridaygrey
	710239	blackfridaysupermaxplus
	710237	blackfridaysupermaxpro
	710238	blackfridaysupermaxsmart
	16483	    linkacaomaesplus
	16484	    linkacaomaespro
	16485	    linkacaomaessmart
	16343	    siteoferta2pix0
	16583	    siteoferta2vistapix00
	16584	    siteoferta3multipix00
	16353	    siteoferta3pix0
	16344	    siteoferta4pix0
	16554	    sitesupermaxplus
	16555	    sitesupermaxpro
	16553	    sitesupermaxsmart

- [x] SQL para pegar ID destas promoções:
		```SELECT IDT_MOBI_PROMOTION FROM mobi_promotion mp WHERE NAM_PROMOTION IN ("blackfridaygrey","blackfridaybasico","blackfridaysupermaxsmart","blackfridaysupermaxplus","blackfridaysupermaxpro","siteoferta2vistapix00","siteoferta3multipix00","siteoferta3multipix0","siteoferta2vistapix0","sitesupermaxpro","sitesupermaxsmart","sitesupermaxplus","linkacaomaesplus","linkacaomaespro","linkacaomaessmart","siteoferta4pix0","siteoferta3pix0","siteoferta2pix0");```

- [x] Script para criar categoria SPECIAL e SUBSCRIPTION_PLAN e associar promoções especiais
	`-- 2. ASSOCIANDO PROMOÇÕES ESPECIAIS A CATEGORIA ESPECIAL`
	
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY, IDT_MOBI_PROMOTION)`
	`SELECT 1, mp.IDT_MOBI_PROMOTION`
	`FROM mobi_promotion mp`
	`WHERE mp.NAM_PROMOTION IN (`
		`"blackfridaygrey",`
		`"blackfridaybasico",`
		`"blackfridaysupermaxsmart",`
		`"blackfridaysupermaxplus",`
		`"blackfridaysupermaxpro",`
		`"siteoferta2vistapix00",`
		`"siteoferta3multipix00",`
		`"siteoferta3multipix0",`
		`"siteoferta2vistapix0",`
		`"sitesupermaxpro",`
		`"sitesupermaxsmart",`
		`"sitesupermaxplus",`
		`"linkacaomaesplus",`
		`"linkacaomaespro",`
		`"linkacaomaessmart",`
		`"siteoferta4pix0",`
		`"siteoferta3pix0",`
		`"siteoferta2pix0"`
	`);`
- [ ] Aprovação do [TUCUMAN](https://jiraps.atlassian.net/servicedesk/customer/portal/150/SDAD-34221?created=true)

# Alterar consultas das categorias das promoções
- [x] Achar maneira de consultar o tipo da promoção.
- [x] Alterar todos os locais em que o feature gateway é consultado para categorizar as promos especiais, utilizar a nova estratégia.

- [x] Criar regra de elegibilidade para nova categoria
	- [x] Consulta o endpoint do pagControle: [Link](https://api.pagcontrole.qa.intranet.pags/swagger-ui/swagger-ui/index.html#/subscriber-controller/isEligible)
- [x] Desenvolver exception para caso tente verificar eligibilidade da pagcontrole e de ruim
- [x] Alterar as regras de elegibilidade: caso o cliente esteja com uma promoção do tipo assinatura, ele se torna inelegível a todas as outras promos
- [x] Adicionar valor PRO-RATA no end point - **GET /v1/promotions/{promotionName}, quando a promoção for do novo tipo de assinaturas. Caso a promoção não seja do tipo novo de assinaturas, o campo “proRataPrice” deve retornar null. O cálculo é proporcional ao dia da request no mês, considerando D0:**

    - No primeiro dia do mês, o valor é cheio (considerar valor promocional)valor prorata

    - Exemplo considerando exatamente a metade do mês:
	    - Se cheio for 50
	    - se for dia 1 é pago 50
	    - se for dia 15 é pago 25
	    - Saber quantos dias tem o mês,  fazer o calculo

	`{ ... "products": [ { "hash": "5a59efd11053578d", "originalPrice": 16.68, "promotionPrice": 20.00, "proRataPrice": 10.00, "status": "OK" }, { "hash": "5cd31781d153ba42", "originalPrice": 226.8, "promotionPrice": 50.0, "proRataPrice": 25.0, "status": "OK" } ], ... }`
	
	Seria ideal mudar os dois end-points não?
	
		![[Pasted image 20241014120115.png]]
	
- [ ] Ajustar e criar testes para nova verificação.
- [ ] Prorata null se não tiver.
- [x] Excluir os FeatureGatewaY
# Observações e duvidas

- Duvida da query do categoryRepository
	- Se preciso colocar dois JOINs ou um resolveria? pois não tenho a mobi_promotion_category como entidade (class entity msm).
- No PromotionEligibleServiceImpl
	- Adicionar um if else aninhado, melhor fazer de outra forma?
- No promotionV1 (interface)/PromotionV1Response
	- Devo alterar os dois end-points certo? o getPromotion e o getCodePromotion? 
		![[Pasted image 20241014120115.png]]

- Não consigo rodar localmente o app, aponta AdminClient, Broker may not be available.
# Apos ajustar a version no banco promotion

Rodar este commit para ajustar QA

Commit upgrade versão da promotion:  
[https://github.com/ps-store/store-promotion/commit/57287463a8082dfb147d09f1ba50ebeefd7df9ec](https://github.com/ps-store/store-promotion/commit/57287463a8082dfb147d09f1ba50ebeefd7df9ec "https://github.com/ps-store/store-promotion/commit/57287463a8082dfb147d09f1ba50ebeefd7df9ec")

# Dicas Caio

 Sempre que for transacionar entre branch
	 De um git stash para salvar na branch

- [x] Não cria logica em cima de ID
	Por exemplo na tabela CATEGORY, usa o nome ao invés de ID, pois o nome temos controle, ja o ID, não temos, pois o banco em prod pode criar com um ID diferente do local e QA.
	Criar logica sempre em campo mais forte, no caso categoria

- [x] Usar método que chame apenas uma vez o banco, podemos usar JOIN, para passaro name da promoção e ele busca o nome da categoria desta promoção.

- [x] Ao invés de criar dois métodos isSpecial e isSubscriptionPlan, podemos fazer um método que recebe o nome da promoção + categoria da promoção e verifica se esta promoção pertence a esta categoria, retornando um TRUE ou FALSE.

Outras opções: 

Se eu tenho o nome da promotion. posso so dar o get no campo

instanciar...

query que retornar mobi pormotion, e damos oget para pegar categoria




# Dicas Caio 2

Mudar o elegibilite do mgm e promotion
se for ja retorne false
verificar se ele ja ta no pagcontrole

fazer como a notContainsPromotionOrCOntainsDEfaultPromotion

- [x] Colocar o service retornando o nome da categoria, ao inves de verificar se ela é igual a categoria. 

AONDE EU PEGO O PREÇO DA ASSINATURA? PARA O CALCULO PRO RATA?


# Execução com CAIO

Recuperar todo promoção e colocar em um entityDTO e não recuperar apenas o nome da promoção ou a categoria. (Usou o mobiPromotionV0 que é tipo um DTO)
	Fizemos isso usando um repository que retorna toda um entidade



Usamos o método que busca a promoção atual do usaria, que antes usava safepayId para usar codCostumer

| MES COM 31 |             | MES COM 30 |             | MES COM 29 |             |
| ---------- | ----------- | ---------- | ----------- | ---------- | ----------- |
| 1          | R$ 29,90    | 1          | R$ 29,90    | 1          | R$ 29,90    |
| 2          | R$ 28,93548 | 2          | R$ 28,90333 | 2          | R$ 28,86897 |
| 3          | R$ 27,97097 | 3          | R$ 27,90667 | 3          | R$ 27,83793 |
| 4          | R$ 27,00645 | 4          | R$ 26,91000 | 4          | R$ 26,80690 |
| 5          | R$ 26,04194 | 5          | R$ 25,91333 | 5          | R$ 25,77586 |
| 6          | R$ 25,07742 | 6          | R$ 24,91667 | 6          | R$ 24,74483 |
| 7          | R$ 24,11290 | 7          | R$ 23,92000 | 7          | R$ 23,71379 |
| 8          | R$ 23,14839 | 8          | R$ 22,92333 | 8          | R$ 22,68276 |
| 9          | R$ 22,18387 | 9          | R$ 21,92667 | 9          | R$ 21,65172 |
| 10         | R$ 21,21935 | 10         | R$ 20,93000 | 10         | R$ 20,62069 |
| 11         | R$ 20,25484 | 11         | R$ 19,93333 | 11         | R$ 19,58966 |
| 12         | R$ 19,29032 | 12         | R$ 18,93667 | 12         | R$ 18,55862 |
| 13         | R$ 18,32581 | 13         | R$ 17,94000 | 13         | R$ 17,52759 |
| 14         | R$ 17,36129 | 14         | R$ 16,94333 | 14         | R$ 16,49655 |
| 15         | R$ 16,39677 | 15         | R$ 15,94667 | 15         | R$ 15,46552 |
| 16         | R$ 15,43226 | 16         | R$ 14,95000 | 16         | R$ 14,43448 |
| 17         | R$ 14,46774 | 17         | R$ 13,95333 | 17         | R$ 13,40345 |
| 18         | R$ 13,50323 | 18         | R$ 12,95667 | 18         | R$ 12,37241 |
| 19         | R$ 12,53871 | 19         | R$ 11,96000 | 19         | R$ 11,34138 |
| 20         | R$ 11,57419 | 20         | R$ 10,96333 | 20         | R$ 10,31034 |
| 21         | R$ 10,60968 | 21         | R$ 9,96667  | 21         | R$ 9,27931  |
| 22         | R$ 9,64516  | 22         | R$ 8,97000  | 22         | R$ 8,24828  |
| 23         | R$ 8,68065  | 23         | R$ 7,97333  | 23         | R$ 7,21724  |
| 24         | R$ 7,71613  | 24         | R$ 6,97667  | 24         | R$ 6,18621  |
| 25         | R$ 6,75161  | 25         | R$ 5,98000  | 25         | R$ 5,15517  |
| 26         | R$ 5,78710  | 26         | R$ 4,98333  | 26         | R$ 4,12414  |
| 27         | R$ 4,82258  | 27         | R$ 3,98667  | 27         | R$ 3,09310  |
| 28         | R$ 3,85806  | 28         | R$ 2,99000  | 28         | R$ 2,06207  |
| 29         | R$ 2,89355  | 29         | R$ 1,99333  | 29         | R$ 1,03103  |
| 30         | R$ 1,92903  | 30         | R$ 0,99667  |            |             |
| 31         | R$ 0,96     |            |             |            |             |


# Duvidas durante o TEST

SpecialPromotionEligibilityStategyTest
	Metodo testCustomerIsNotEligibleBecauseHisPromotionIsNotDefault
		Esta dizendo que existem mockitos desnecessários, mas se os removo um validação para de funcionar.

SpecialPromotionEligibilityStategy
	Metodo notContainsPromotionOrContainsDefaultPromotion, só esta validando se é igual a promotion, devemos validar se não contem? ou mudar o nome do método?

MobiUserPromotionServiceImpl
	Método givenRequestWhenGetActivePromotionByUser, não esta conseguindo achar a promotion DEFAULT.. não entendi a logica.