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
- [x] Testar o migration
- [x] Validação do time
	- [x] ==Necessidade de criação de INDEX? Pergunta do Bruno==
- [ ] Validação da Migration com TUCUMAN

# CRIAR SCRIPT PARA EXECUÇÃO DML PARA CATEGORIZAR AS PROMOS ESPECIAIS

"blackfridaygrey", "blackfridaybasico", "blackfridaysupermaxsmart", "blackfridaysupermaxplus", "blackfridaysupermaxpro", "siteoferta2vistapix00", "siteoferta3multipix00", ~~"siteoferta3multipix0"~~, ~~"siteoferta2vistapix0",~~ "sitesupermaxpro", "sitesupermaxsmart", "sitesupermaxplus", "linkacaomaesplus", "linkacaomaespro", "linkacaomaessmart", "siteoferta4pix0", "siteoferta3pix0", "siteoferta2pix0"

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

- [ ] Aprovação do time
- [ ] Aprovação do Tucuman

# Alterar consultas das categorias das promoções
- [ ] Alterar todos os locais em que o feature gateway é consultado para categorizar as promos especiais, utilizar a nova estratégia.
- [ ] Configurar ambiente de execução local (Banco MYSQL e KAFKA)
- [ ] Ajustar e criar testes para nova verificação.



# Observações e duvidas
- Nome das tabelas da promotion estão todas em lowercase, matenho este padrão ou sigo as demais apps com tudo em maisculo?
- Crio uma copia com tabelas_aud?
- Vi que usam BIGINT para IDT, mas no nosso caso serão poucos, posso usar INT ou TINYINT?

## Observação Extra
Notei que a tabela JA EXISTENTE mobi_user_promotion_code_active_aud tem mais de 30carateres. isso não gera nenhum problema certo? 

