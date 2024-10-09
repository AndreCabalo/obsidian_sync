[[Pagbank]]
# CRIAR SCRIPT PARA CRIAÇÃO DE TABELAS

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
- [ ] Merger na Master
- [ ] Fazer os msm passos de migração no Jenkins, so database migration prod, bumpversion patch (mas nao faz diferença nenhuma)

# CRIAR SCRIPT PARA EXECUÇÃO DML PARA CATEGORIZAR AS PROMOS ESPECIAIS

"blackfridaybasico", "blackfridaysupermaxsmart", "blackfridaysupermaxplus", "blackfridaysupermaxpro", "siteoferta2vistapix00", "siteoferta3multipix00", "siteoferta2vistapix0", "siteoferta3multipix0", "sitesupermaxsmart", "sitesupermaxpro", "sitesupermaxplus", "linkacaomaesplus", "linkacaomaespro", "linkacaomaessmart", "siteoferta4pix0", "siteoferta3pix0", "siteoferta2pix0"


"blackfridaybasico", "blackfridaysupermaxsmart", "blackfridaysupermaxplus", "blackfridaysupermaxpro", "siteoferta2vistapix00", "siteoferta3multipix00", "siteoferta2vistapix0", "siteoferta3multipix0", "sitesupermaxsmart", "sitesupermaxpro"

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
- [ ] Alterar todos os locais em que o feature gateway é consultado para categorizar as promos especiais, utilizar a nova estratégia.
- [ ] Alterar as regras de elegibilidade: caso o cliente esteja com uma promoção do tipo assinatura, ele se torna inelegível a todas as outras promos
- [ ] Adicionar valor PRO-RATA no end point - **GET /v1/promotions/{promotionName}, quando a promoção for do novo tipo de assinaturas. Caso a promoção não seja do tipo novo de assinaturas, o campo “proRataPrice” deve retornar null. O cálculo é proporcional ao dia da request no mês, considerando D0:**
    
    - No primeiro dia do mês, o valor é cheio (considerar valor promocional)
        
    - Exemplo considerando exatamente a metade do mês:
        

	`{ ... "products": [ { "hash": "5a59efd11053578d", "originalPrice": 16.68, "promotionPrice": 20.00, "proRataPrice": 10.00, "status": "OK" }, { "hash": "5cd31781d153ba42", "originalPrice": 226.8, "promotionPrice": 50.0, "proRataPrice": 25.0, "status": "OK" } ], ... }`
- [ ] Ajustar e criar testes para nova verificação.
- [ ] Prorata null se não tiver.



# Observações e duvidas

PRECISO QUE APROVEM A PR DA FEATURE -> DEVELOP
NA SEQUÊNCIA ABRO OUTRA PR DA DEVELOP -> MASTER 
APOS IR PARA MASTER RODO A PIPE COM O MIGRATION PARA A DEVELOP


NAO ESQUECER DE DAR UM GIT PULL DEVELOP NA BRANCH DA SUB DE CONSULTA
