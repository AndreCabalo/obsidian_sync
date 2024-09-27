[[Java]][[Estudos]][[Alura]]

É aquele que não precisa de nenhuma instancia da classe para ser chamado.
Ideal para quando não precisamos interagir com os atributos ou métodos de um objeto criado.

Podem ser acessados diretamente a partir da classe.

Exemplo de método:

```java
public class MathUtils {
    public static int add(int a, int b) {
        return a + b;
    }
}
```

Exemplo de uso:

```java
int result = MathUtils.add(5, 10);
```

