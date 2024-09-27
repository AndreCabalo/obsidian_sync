[[Pagbank]]
## Analisar Pagmon, o contexto que você ira atuar
[Pagmon](https://pagmon.intranet.pags/d/sPmipFUVk/la-palma-red-metrics?orgId=1&refresh=1m)

## Verfi
car qual das ordens deve ser feita:

### Mergear Develop na Master antes
Rodar jenkins na Branch que vc criou, caso tenha opção de selecionar a branch e roda pipeline
### Mergear Develop na Master depois
Mergear Develop na Master e depois disso rodar a pipeline


Após pipe rodar sem quebrar, continuar para o proximo passo
### Conferir os pods
Verificar se a versão gradle properties é compativel(não fiz isso ainda pq tava sem acesso ao kubectl)

Comandos:

```
kubectx
```

```
kubectl get pods
```


### Comunicar no teams no chat acquisition delivery

[Canal Delivery da Acquisiton]([Acquisition | Delivery | Microsoft Teams](https://teams.microsoft.com/l/channel/19%3A5bb4335547fc446bbcc758e0a4a4c73c%40thread.tacv2/Delivery?groupId=0e3278af-191a-469f-88a4-4d44d7d29c7c))
