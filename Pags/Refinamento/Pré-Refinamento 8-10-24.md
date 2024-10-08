# Inativar um checkout

Se link tiver aberto, ao inativar, ele da erro em todos os meios de pagamento, mesmo que o cliente esteja no meio do fluxo. Exceto se ele ja tiver qr-code pix ou boleto.
Impede que ele acesse a tela de checkout e impede o pagamento.

# Intuito
Adicionar coluna com flag para ver se esta ativa ou inativado.
Evitando alterar o status da purchase.
Quando o checkout Expira

Por usar o V1 da checkout não recebemos os status de checkout (EXPIRED)
SE usar a V2 da checkout receberemos todos os status 

Pix não aparece na tela de conclusão.
No v1 checkout se escolher o pix ele força o usuário a logar
No v2 checkout se escolher o pix, ja mostra o pix na tela generica 

Para migra para v2, precisaram implementar essa gambiarra, ou remover com afiliados para não precisar do pix esta na tela de conclusão.(não tem esse comportamento na v2)

Em algum momento precisaremos migrar para a v2 da checkout


Sem migrar para v2 temos limitação da flag