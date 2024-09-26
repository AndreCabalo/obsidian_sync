### Origem do bug Método attachTagToProduct
Não estava setando o novo nameAgent
Não estava setando o novo log

### Dúvidas
#### Mudar nome do método?
Este método ja existia porém, aparentemente ele ja não atualizava nameAgent e log.
O método se chama attachTagToProduct, ==deveriamos mudar o nome==? pois ele não apenas associar uma tag a um produto, como tambem atualiza toda relacão (com ativa a relação, seta prioridade, nameAgent e log)

#### Fazer testes unitários?
Devo fazer testes unitarios para essa atualizacao de nameAgent e log?

## Teste unitário


### Teste unitário com parte comentada

        @Test  
        @DisplayName("Deve e atualizar os campos de uma relação ja existente")  
        void attachTagSuccessfullyAndUpdatedFields() {  
            ProductTagEntity productTagEntity = ProductTagEntityMockHelper.defaultProductTagEntityBuilder().isActive(true).build();  
            TagEntity tagEntity = productTagEntity.getTag();  
            ProductEntity productEntity = productTagEntity.getProduct();  
  
//            ArgumentCaptor<ProductTagEntity> productTagEntityAC = ArgumentCaptor.forClass(ProductTagEntity.class);  
  
            when(tagRepository.findByName(DEFAULT_TAG_NAME)).thenReturn(Optional.of(tagEntity));  
            when(productRepository.findByCodHash(DEFAULT_HASH)).thenReturn(Optional.of(productEntity));  
            when(productTagRepository.findByTagNameAndProductHash(DEFAULT_TAG_NAME, DEFAULT_HASH)).thenReturn(Optional.of(productTagEntity));  
//            when(productTagRepository.save(productTagEntityAC.capture())).thenAnswer(i -> i.getArguments()[0]);  
  
            assertDoesNotThrow(() ->  
                    tagService.attachTagToProduct(DEFAULT_TAG_NAME, DEFAULT_PRODUCT_TAG_PRIORITY, DEFAULT_HASH, "AgentUpdated", "LogUpdated"));  
  
//            ProductTagEntity productTagEntitySaved = productTagEntityAC.getValue();  
  
            verify(productTagRepository, times(1)).save(productTagEntity);  
            assertTrue(productTagEntity.getIsActive());  
            assertEquals("AgentUpdated", productTagEntity.getChangeAgent());  
            assertEquals("LogUpdated", productTagEntity.getChangeLog());  
  
        }





