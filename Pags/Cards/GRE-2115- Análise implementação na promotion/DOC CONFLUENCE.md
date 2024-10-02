## Contexto

Existe um intuito de diminuir a dependência do **feature gateway** na store-promotion. Pois atualmente ao verificar se uma programação é especial, precisamos acessar uma lista do feature gateway, afim de buscar se o nome da promoção consta nesta lista.

Para sanar esta dependência planejamos criar a tabela **category** no banco da **store_promotion**, solução esta que facilitara não só esta dependência com o feature gateway, mas também compõem uma estratégia para a implementação do pagcontrole, onde poderemos descobrir a qual categoria a promoção pertence (especial, pagcontrole, default).

## Estrategia sugerida

1. Script para criar tabela de **category**, com relação N:N com a **mobi_promotion.**
    
2. Esta relação N:N dará origem a uma nova tabela **promotion_category**, que fará a associação dos ids das tabelas category e mobi_promotion.
    

3. Criar endpoint para criar promoção.
    
4. Criar endpoint para vincular promoção a categoria.
    

## Dúvidas

// DEFAULT EM CATEGORIA DE PROMOÇOES?

// CRIAREMOS END POINT PARA CRIAR PROMO E OUTRO PARA VINCULAR? OU SERAO FEITO VIA SCRIPT?