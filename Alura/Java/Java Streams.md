Uma caracteristica poderosa que oferece a capacidade de eralizar operações de processamento de dados complexas de forma eficiente e em paralelo, sobre collections, arrays e I/O Channels.

## Streams infinitos
São streams que nào possuem um tamanho definido.
São utéis quando queremos gerar uam sequência de números ou valores.

```java
Stream.iterate(0, n -> n + 1)
     .limit(10)
     .forEach(System.out::println);
```

No exemplo a cima, começamos com o número 0 e adicionamos 1 a cada interação para gerar um sequência númerica. E usamos limit() para restringir o steam a 10 elementos e forEach para imprimi-los.

## FlatMap

O método flatMap é uma operação intermediária que é usada para transformar um Stream de coleções em um stream de elementos.

```java
List<List<String>> list = List.of(
  List.of("a", "b"),
  List.of("c", "d")
);

Stream<String> stream = list.stream()
  .flatMap(Collection::stream);

stream.forEach(System.out::println);
```

No exemplo a cima, transformamos um Stream de List para um Stream de Strings.


## Redução de Streams

Stream.reduce() é uma operação terminal que é utilizada para reduzir o conteúdo de um Stream para um único valor.

```java
List<Integer> numbers = List.of(1, 2, 3, 4, 5);
Optional<Integer> result = numbers.stream().reduce(Integer::sum);
result.ifPresent(System.out::println); //prints 15
```

No exemplo a cima, somamos todos os números da lista usando o método reduce().


