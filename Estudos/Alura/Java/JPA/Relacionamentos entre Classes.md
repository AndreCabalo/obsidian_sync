[[Estudos]] [[Alura]] [[Java]]  [[JPA e Hibernate]]
Temos quatro principais tipos de relações:
### **One-To-Many (Um-Para-Muitos):**
Neste tipo de relação, um registro em uma tabela pode se relacionar com muitos registros em outra tabela. Por exemplo, um professor pode dar aulas para muitos alunos e criar uma relação um-para-muitos entre o professor e os alunos.

Nesse código, estamos dizendo que um professor pode possuir muitos alunos. 
A propriedade **mappedBy** é usada para indicar o campo que representa o professor na entidade Aluno.

```java
@Entity
public class Professor {
    @Id
    private Long id;
    private String nome;
    
    @OneToMany(mappedBy = "professor")
    private List<Aluno> alunos;
}
```

### **Many-To-One (Muitos-Para-Um):**
Aqui, muitos registros em uma tabela podem se relacionar com um registro em outra tabela. Usando o exemplo anterior, muitos alunos podem ter aula com um mesmo professor, estabelecendo uma relação muitos-para-um.

```java
@Entity
public class Aluno {
    @Id
    private Long id;
    private String nome;
    
    @ManyToOne
    private Professor professor;
}
```

### **Many-To-Many (Muitos-Para-Muitos):** 
Nesta relação, muitos registros em uma tabela podem se relacionar com muitos registros em outra tabela. Bem, um aluno pode ter aulas com vários professores e vice-versa, certo? Esta é uma relação muitos-para-muitos.

Esta relação é um tanto mais complexo, pois requer uma tabela intermediária para sua implementação. 

Nesse case, estamos dizendo que u malino pode ter muitos professores e um professor pode ter muitos alunos.

A tabela intermediária é criada automaticamente pela JPA.

```java
@Entity
public class Aluno {
    @Id
    private Long id;
    private String nome;
    
    @ManyToMany
    private List<Professor> professores;
}

@Entity
public class Professor {
    @Id
    private Long id;
    private String nome;

    @ManyToMany(mappedBy = "professores")
    private List<Aluno> alunos;
}
```
### **One-To-One (Um-Para-Um)**: 
Neste tipo de relação, um registro em uma tabela se relaciona com apenas um registro em outra tabela, e vice-versa. Por exemplo, um usuário pode ter apenas um endereço, e este endereço pertence a apenas um usuário.

Nesse exemplo o usuario possui apenas um endereço e um endereço pertence a apenas um user.

O atributo cascade = CascadeType.ALL indica que as operações de persistência (salvar, atualizar, remover) no objeto user serão propagadas para o obj endereço.

```kotlin
@Entity
public class Usuario {
    @Id
    private Long id;
    private String nome;
    
    @OneToOne(cascade = CascadeType.ALL)
    private Endereco endereco;
}

@Entity
public class Endereco {
    @Id
    private Long id;
    private String logradouro;
    private String bairro;
    private String cidade;
    // outros atributos...
    
    @OneToOne(mappedBy = "endereco")
    private Usuario usuario;
}
```

