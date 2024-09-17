
## Passos:

### Ler Confluence
- [x] Ler sobre a Store-promotion

### Duvidas sobre Store Promotion

1. Podemos usar a tabela PROMOTION para armazenar as promoções especiais que iremos tirar do feature-gateway?

2. Possui um campo COD_BC_CONTRACT (que podemos apagar?)

3. No type, podemos setar se é especial?

![[TPromotion.png]]

### Resumo sobre o trecho que irei operar

[Conteúdo falando do fluxo que irei alterar ao verificar lista do featuregateway](https://jiraps.atlassian.net/wiki/spaces/GRE/pages/75318461273/Elegibilidade)

Em resumo a uma lista de promoções no feature-gateway, ao verificar a elegibilidade de um cliente a uma promoção, se ela constar na lista de promos especiais, a elegibilidade terá algumas regras(Consulta o feature-toogle na verificação.):

SE NÃO - é promoção comum e será elegivel.
SE SIM, verifica se a promoção é DEFAULT
	SE NÃO, então não é elegivel!
	SE SIM,  dispara threads para ambas verficações:
		Verifica se possui algum transacao no ultimo 180 dias
		Verifica se o contrato atual é Default (consultando o API de Business Contract)
		SE AMBOS TRUE, é elegivel
		SE ALGUM FOR FALSE, Inelegivel.


# PAREI AQUI
### TAREFAS AINDA PENDENTES PARA A ANALISE DA SPIKE

- [ ] Ler sobre feature-gateway
- [ ] Ler o ReadMe do repositório
	- [ ] Migration que apontam no ReadMe não funfa.
	- [ ] Preciso ter acesso ao banco Stage da AWS?
	- [ ] Posso subir um banco local pra enxergar a estrutura do banco?
- [ ] Análisar o código na IDE
	- [ ] Parece que terei que mudar algo no arquivo  FeatureGatewayServiceImpl


Análise de nova implementação de categoria de promoções.

### Anotações durante refinamento.

- Remover promoções especiais do feature-gateway
    
- Criar estrutura de categoria no banco
    
Adicionar provalvemente TABELA COM colunas:

- Nome
    
- Criacao
    
- Atualizacao
    
- Flag de ativo



