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
- [ ] Validação do time
	- [ ] ==Necessidade de criação de INDEX? Pergunta do Bruno==
- [ ] Validação da Migration com TUCUMAN

# CRIAR SCRIPT PARA EXECUÇÃO DML PARA CATEGORIZAR AS PROMOS ESPECIAIS

"blackfridaygrey", "blackfridaybasico", "blackfridaysupermaxsmart", "blackfridaysupermaxplus", "blackfridaysupermaxpro", "siteoferta2vistapix00", "siteoferta3multipix00", "siteoferta3multipix0", "siteoferta2vistapix0", "sitesupermaxpro"

- [ ] Ids de promoções especiais:
	- 710236
	- 16776
	- 710239
	- 710237
	- 710238
	- 16583
	- 16584
	- 16555

- [ ] SQL para pegar ID destas promoções:
	```SELECT IDT_MOBI_PROMOTION FROM mobi_promotion mp WHERE NAM_PROMOTION IN ("blackfridaygrey","blackfridaybasico", "blackfridaysupermaxsmart", "blackfridaysupermaxplus","blackfridaysupermaxpro", "siteoferta2vistapix00", "siteoferta3multipix00","siteoferta3multipix0", "siteoferta2vistapix0", "sitesupermaxpro")```

- [ ] Script para criar categoria SPECIAL e SUBSCRIPTION_PLAN e associar promoções espciais

	`-- 1. INSERIR CATEGORIAS`  
	`INSERT INTO category (NAM_CATEGORY) VALUES ('special');`  
	`INSERT INTO category (NAM_CATEGORY) VALUES ('subscription_plan');`  
	
	`-- 2. ASSOCIANDO PROMOÇÕES ESPECIAIS A CATEGORIA SPECIAL`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,710236);`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,16776);`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,710239);`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,710237);`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,710238);`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,16583);`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,16584);`  
	`INSERT INTO mobi_promotion_category (IDT_CATEGORY,IDT_MOBI_PROMOTION) VALUES (1,16555);`

- [ ] Alterar todos os locais em que o feature gateway é consultado para categorizar as promos especiais, utilizar a nova estratégia.
- [ ] Configurar ambiente de execução local (Banco MYSQL e KAFKA)
- [ ] Ajustar e criar testes para nova verificação.



# Observações e duvidas
- Nome das tabelas da promotion estão todas em lowercase, matenho este padrão ou sigo as demais apps com tudo em maisculo?
- Crio uma copia com tabelas_aud?
- Vi que usam BIGINT para IDT, mas no nosso caso serão poucos, posso usar INT ou TINYINT?

## Observação Extra
Notei que a tabela JA EXISTENTE mobi_user_promotion_code_active_aud tem mais de 30carateres. isso não gera nenhum problema certo? 

