[[Java]][[Estudos]]
Problemas com migrações com erros em SQL

Para resolver esse problema será necessário acessar o banco de dados da aplicação e executar o seguinte comando sql:

```sql
delete from flyway_schema_history where success = 0;
```

Pode ser preciso apagar o banco de dados atual e replica-lo, caso o problema persista!