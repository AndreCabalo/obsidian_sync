[[Java]][[Estudos]][[Alura]]
Criar um sistema de clasificação de projetos.

Usaremos enums, para classificar:
- Iniciante
- Intermediário
- Avançado
Além disso devemos associar uma pontuação para cada nível.

Para isso faremos:

```java
public enum Nivel {
    Iniciante(1), 
    Intermediario(2), 
    Avancado(3);
    
    private int pontuacao;
    Nivel(int pontuacao) {
        this.pontuacao = pontuacao;
    }
}
```

Onde a pontuação é corretamente definida como um atributo para cada nível enum.
O enum tem um construtor que permite atribuir um valor a este atributo.