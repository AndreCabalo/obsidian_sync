
## Arquivo de propriedades

Por padrão, o Spring Boot acessa as configurações definidas no arquivo `application.properties`, que usa um formato de `chave=valor`:

```ini
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver
spring.datasource.url=jdbc:mysql://localhost:3306/clinica
spring.datasource.username=root
spring.datasource.password=root
```

Cada linha é uma configuração única, então é preciso expressar dados hierárquicos usando os mesmos prefixos para nossas chaves, ou seja, precisamos repetir prefixos, neste caso, `spring` e `datasource`.

## YAML Configuration

YAML é um outro formato bastante utilizado para definir dados de configuração hierárquica, como é feito no Spring Boot.

Pegando o mesmo exemplo do nosso arquivo `application.properties`, podemos convertê-lo para YAML alterando seu nome para `application.yml` e modificando seu conteúdo para:

```yaml
spring:
  datasource:
    driver-class-name: com.mysql.cj.jdbc.Driver
    url: jdbc:mysql://localhost:3306/clinica
    username: root
    password: root
```

Com YAML, a configuração se tornou mais legível, pois não contém prefixos repetidos. Além de legibilidade e redução de repetição, o uso de YAML facilita o armazenamento de variáveis de configuração de ambiente, conforme recomenda o _[12 Factor App](https://12factor.net/)_, uma metodologia bastante conhecida e utilizada que define 12 boas práticas para criar uma aplicação moderna, escalável e de manutenção simples.
