
Ter checkout para nao ter tela intermediaria para capturar token

Dificuldade stoke-checkout 
- Atualmente p
- Preço puxa da promoção
- Querem preço PRORATA (quanto falta para o mês acabar)
- Pensamos em  criar nova Purchase para ter uma regra especifica para ela.
- Atenção ao fluxo backoffice
- Não podemos deixar sobreescrever a promoção caso ele compre outra maquininha, pode mandar mgm etc, só não pode tirar a promoção valida do pagControle, ambas maquininhas contam o valor da franquia pagcontrole.
- Tabela Promotion_Category, para guardar promotion do tipo:
	- Default
	- Especiais
	- Assinatura (PagControlle)



## Anotações Caio

- Impactos store-checkout 
	- Criar nova categoria de Purchase 
	- Seller diferente 
	- Calcular preço proporcional (pro-rata) 
	- Checkout apenas com cartão de crédito 
	- Atenção ao fluxo da backoffice, job e tópicos 
	- Categoria vinculada a "tipo" de promoção 
	- Verificar o link promocional para não alterar em caso de PagControle 
- Impactos loja 
	- Adicionar promoção no endpoint do Estocolmo 
		- Confirmar com o Esto 
- Impactos Promotion 
	- Criar tabela associada à mobi_promotion 
	- Endpoint para associar/alterar a categoria de promoção 
	- Categorizar as promoções especiais e Assinatura 
	- Alterar endpoint de elegibilidade para tornar clientes com promo pag_controle inelegíveis a qualquer outra promo. 
		- Confirmar com o Esto

### Dúvidas

- Consultar Elegibilidade 
	- Pagcontrole implementar um endpoint - OK 
- O que fazer quando não é elegível 
	- Mandar pro carrinho - OK 
	- O que fazer caso compre outra maquininha? 
	- O que fazer com outra promoção Duas ou mais maquininhas com as condições do pagControle? 
	- Permitir desde que não sobrescreva a promoção 
- Notificação do checkout 
	- Usar tópico/pagcontrole receber a notificação do checkout 
- Criação da Promoção 
	- Ver quem pode apoiar


Ideia é passar um previsão nossa. para ver se bate com a deles.
Motor de calculo de preço na promotion
Promotion tbm tera que calculos o preço, consdierando, promoção prorata, se não tiver promoção pega o valor direto da products