[[Pagbank]]
## Contexto

Atualmente para validar se uma promoção é especial ou não, é preciso acessar o feature gateway e verifica se o nome da promoção se encontra na lista de promoções especiais.

**O intuito é remover** estas promoções **especiais do feature gateway** e **criar** uma estrutura de **categoria no banco**. Na qual permita que a consulta, sem a necessidade de acessar o feature gateway.

## Pontos de preocupação e dúvida

1. Criamos um scrip migration para adicionar uma nova tabela ou podemos utilizar alguma tabela existente, como por exemplo a tabela promotion (Esta tabela não possui referência no código atualmente. Aparentemente serviu para um fluxo conhecido como Desconto Progressivo)?
    
2. Somos os únicos que utilizam a feature gateway para buscar esta lista de promoções especiais?
    
3. Como excluir a lista de promoções do feature gateway?
    

## Estrategia sugerida

1. Criar um scrip no migration para adicionar uma tabela ou usar uma tabela existente.
    
2. Pedir aprove do Tucuman , tanto para alterar uma tabela existente ou criar nova.
    
3. Criar uma entity/dto para representar a tabela e colunas?
    
    - Caso criemos uma nova tabela/entity, adicionaríamos os campos:
        
        1. Nome
            
        2. Flag active
            
        3. Data criação
            
        4. Data atualização
            
        5. Criar método/endpoint para verificar se ela é especial ou não.
            
    - Caso possamos utilizar a tabela PROMOTION:
        
        - Adicionar campo category ou editar o campo type, para setar se é especial ou não.
            
4. Essa mudança causara impacto nos seguintes itens:
    
    1. End-point:
        
        1. [**/v1/promotions/{promotionName}/eligible**](https://store-promotion-api.qa.intranet.pags/swagger-ui.html#/operations/promotion-v-1-impl/eligiblePromotionUsingGET)
            
    2. Classes e métodos:
        
        1. Interface - FeatureGatewayService
            
        2. Classe - FeatureGateServiceImpl, método isEspecialPromotion
            
        3. Classe - PromotionEligibleServiceImpl, método
            
5. Desenvolver teste unitários e testes de integração.
    
6. Atualizar documentação.
    

## Conteúdos relacionados

  
[https://jiraps.atlassian.net/wiki/spaces/GRE/pages/75318461273](https://jiraps.atlassian.net/wiki/spaces/GRE/pages/75318461273)

[https://jiraps.atlassian.net/wiki/spaces/GRE/pages/74773856359](https://jiraps.atlassian.net/wiki/spaces/GRE/pages/74773856359)

[https://jiraps.atlassian.net/wiki/spaces/GRE/pages/74770449513](https://jiraps.atlassian.net/wiki/spaces/GRE/pages/74770449513)

[https://jiraps.atlassian.net/wiki/spaces/EST/pages/74392502906](https://jiraps.atlassian.net/wiki/spaces/EST/pages/74392502906)