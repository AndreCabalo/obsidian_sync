# Infos
Não precisamos ter um carrinho criado

# Validação
Havera validação e ja existe check point, passando o customerId, se não for elegivél, retornamos algum link por exemplo carrinho vazio ou próprio site. Com provavel feedback generico.

# Calculo de preço
Calculo do preço, será regra D0
	Primeiro dia do mes, preço cheio
	Fim do mês menor valor que seria R$0,48 (com valor de R$50 no ultimo dia do mês)

# Metodos de pagamento
Apenas cartão de credito.
	Flag de pagamento apenas por cartão.
	Parcelamento, é possivel limitar as parcelas via parametro? pois aparentemente esta liberado até 10x.

# Cenário de cancelamento
Terá central onde podem cancelar.
Se cancelar ela não poderá assinar novamente.

# Elegibilidade
Se ja foi assinante e cancelou, não será elegivel
	Não existe upgrade e downgrade.
	Cancelamento, apos o user cancelar, se ele quiser assinar novamente não será elegivel a assinatura.
	Gatilha ao cancelar assinatura o user volta para a taxa padrão.
Se o cliente assinante acessar a landing page, será barrado.

