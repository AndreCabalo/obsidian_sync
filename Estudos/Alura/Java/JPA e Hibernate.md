[[Java]][[Estudos]][[Alura]]
## JDBC
JDBC (java Database Connector) - Solução nativa para lidar com conexões em bancos de dados.

No entanto, a utlização deste tipo de solução começou a ficar maçante pois uma configuração não era simles, nem epquena e tinha que ser repetida N vezes de forma idêntica.
## ORM
Por isso, passaram a surgir alternativas, como o ORM (Mapamento Objeto Relacionalque ao invés de aprensaterem uma conexão CRUA, ou seja, que exija a escrita de consulta e comando SQL na mão., passou a se utilizar soluções que encapsulava grande parte deste processo manual. com funções prontas, nem a necessidade de misturá-la com SQL.

Em java o ORM mais utilizado é o JPA ou Java Persistence API.

## JPA
 Criado com inutito de simplificar a conexão de banco de dados em aplicações Java., a apartir de definifição de uma interface comum a ser utilizada para persistência de dados na linguagem

Fornece uma API para realizar as operações CRUD. Bastar que sua classe extenda a JPA.

Para entender seu funcionamento é importante familiarizar-se com alguns conceitos chave: 
####  Entity
Envolve nossa regra de negocio
Nosso dominio
#### EntityManager
Interface central do JPA, que é usada para realizar operações de persistencia, ou seja CRUD
#### Repository
Responsavel pela persistencia no banco de dados, precisamos criar uma INTERFACE repositor com a nomenclatura NomeClasseRepositoty e sempre EXTENDS  a **JPARepository<NomeClaSse, tipoDadoId>**

Dedicada ao mapeamento no banco de dados
Ao CRUD da classe
#### Service
Os serviços que a classe executa

#### JPQL
Linguagem de consulta da JPA, permite escrever, consultas personalizadas, uma mistura de JAVA e SQL, ou uma SQL orientada a objetos


## Hibernate
Uma implementação popular da JPA, que fornece uma biblioteca baseada em JPA que permite acesso ao banco de dados de forma simplificada. Oque melhora a produtividade no ciclo de desenvolvimento.

Hibernate é distribuído em Open Source.

### Anotações hibernate

#### @Entity
Cada entidade corresponde a uma tabela no banco

```java
@Entity
@Table(name = "minha_tabela")
public class MinhaEntidade { ... }
```

##### @Table
Anotação que permite especificar o nome da tabela, o esquema e as restrições de chave prímaria.


#### @id
Marca um campo como chave prímaria da entidade, identifica exclusivamente os registros no banco.

###### @GeneratedValue
Usada em conjunto com o @id, especifica como a chave primária é gerada automaticamente. 

Pode ser usada estratégias como :
- Auto
- Identity
- Sequence
- Table
Dependendo do banco de dados.

```java
@Id
@GeneratedValue(strategy = GenerationType.IDENTITY)
private Long id;
```

#### @Column

Similar ao que acontece na @Table utiliza o nome dos atributos e os converte como sendo idênticos aos nomes das colunas no banco, caso seja necessário utilizar nome diferentes, pode configurar o noem da coluna, bem como seu tipo, se ela é obrigatória:

```typescript
@Column(name = "nome_completo", nullable = false)
private String nome;
```

#### @OneToMany e @ManytoOne
Usadas para mapear relacionamento de um-para-muitos e muitos-para-um entre entidades.
```java
@Entity
public class Autor {
    @OneToMany(mappedBy = "autor")
    private List<Livro> livros;
}

@Entity
public class Livro {
    @ManyToOne
    @JoinColumn(name = "autor_id")
    private Autor autor;
}
```

#### @ManyToMany
Usada para mapear relacionamentos muitos-para-muitos entre entidades

#### @OneToOne
Usada para mapear relacionamentos um-para-um entre entidades

#### @JoinColum
Usada para especificar a coluna que será usada para representar um relacionamento entre entidades. 
Frequentemente usada em conjunto com o @ManyToOne e @OneToOne

```java
@ManyToOne
@JoinColumn(name = "autor_id")
private Autor autor;
```

##### @JoinTable
Usada para mapear tabelas de junção em relacionamentos muitos-para-muitos. 
Ela especifica a tabela intermediária que liga duas entidades
```less
@Entity
public class Estudante {
    @ManyToMany
    @JoinTable(name = "inscricao",
               joinColumns = @JoinColumn(name = "estudante_id"),
               inverseJoinColumns = @JoinColumn(name = "curso_id"))
    private List<Curso> cursos;
}
```

#### @Transient
Usada para marcar uma propriedade como NÃO PERSISTENTE, ou seja, a propriedade não será mapeada para uam coluna no banco de dados.

```java
@Transient
private transientProperty;
```

#### @Enumerated
Usada para mapear campos enumerados(enum) para colunas do banco de dados.

```java
@Enumerated(EnumType.STRING)
private Status status;
```

#### @NamedQuery
Usada para definir consultas JPQL, nomeadas que podem ser reutilizadas em várias partes do código.

```java
@Entity
@NamedQuery(name = "Cliente.findAll", query = "SELECT c FROM Cliente c")
public class Cliente { ... }
```

#### @Cascade
Usada para especificar o comportamento cascada das operações de persistência, como salvar e excluir, em relacionamentos.

Por exemplo, configrar para que as operações de salvar em cascata afetem entidades relacionadas.

```java
@OneToMany(mappedBy = "departamento")
@Cascade(CascadeType.SAVE_UPDATE)
private List<Funcionario> funcionarios;
```

#### @Embeddable e @Embedded
Usadas para representar tipos incorporados (embeddabke types) que podem ser usados como componenetes em entidades.


```java
@Embeddable
public class Endereco { ... }

@Entity
public class Cliente {
    @Embedded
    private Endereco endereco;
}
```

#### Outras
Além destas existem outras que podem ser consultadas aqui:

[DOC Hibernate](https://docs.jboss.org/hibernate/stable/annotations/reference/en/html/)

