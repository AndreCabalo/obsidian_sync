
[[Duvidas]]

 [ ] Projeto Onboarding
- [x] Construir uma API para cadastro e manipulação de items de um carrinho.
- [x] Requisitos do Projeto
- [x] Passos para Implementação
- [x] 1. Tecnologias Utilizadas:
	- [x] Java 21
	- [x] Spring Boot
	- [x] Spring Data JPA
	- [x] Banco de dados MySQL em Docker
	- [x] Docker
	- [x] RESTful API
- [x] 1. Entidades Principais:
	- [x] Item
		- [x] ID (UUID)
		- [x] Nome
		- [x] Preço
		- [x] Quantidade em estoque
	- [x] Carrinho
		- [x] ID (UUID)
		- [x] Lista de Itens (muitos para muitos)
		- [x] Data de criação
		- [x] Valor total (calculado)
- [x] 1. Regras de Negócio:
	- [x] Não pode adicionar ao carrinho itens com quantidade maior do que a disponível em estoque.
	- [x] O valor total do carrinho deve ser recalculado cada vez que um item é adicionado ou removido.
	- [x] Não pode haver itens duplicados no carrinho.
	- [x] Deve ser possível criar, atualizar e deletar itens no estoque.
- [x] 1. Operações da API:
	- [x] Item:
		- [x] Criar item
		- [x] Atualizar item
		- [x] Deletar item
		- [x] Listar todos os itens
		- [x] Buscar item por ID
	- [x] Carrinho:
		- [x] Criar carrinho
		- [x] Adicionar item ao carrinho
		- [x] Remover item do carrinho
			- [x] **Remover carrinho tbm?**
		- [x] Listar todos os carrinhos
		- [x] Buscar carrinho por ID

 **Passo para implementação**
 
- [x] 1. Configuração do Ambiente:
	- [x] Configurar o ambiente de desenvolvimento com Java 21, Spring Boot e Docker.
	- [x] Criar um contêiner Docker para o banco de dados MySQL.
	- [x] Criar repositório no Github para subir o projeto. Seguir boas práticas de commit: evitar commitar muitos arquivos ao mesmo tempo e utilizar mensagens descritivas.
- [x] 1. Inicializar o Projeto Spring Boot:
	- [x] Usar o Spring Initializr para criar um novo projeto Spring Boot com dependências de Spring Web, Spring Data JPA e MySQL Driver.
- [x] 1. Configuração do Banco de Dados:
	- [x] Configurar as propriedades do banco de dados no application.properties ou application.yml do Spring Boot.
	- [x] Configurar o Docker Compose para iniciar o contêiner do MySQL Database.
	- [x] docker run -d --name mysql -p 3306:3306 -e MYSQL_ROOT_PASSWORD=root -e MYSQL_DATABASE=cart mysql:9.0.1
- [x] 1. Criar Entidades e Repositórios:
	- [x] Criar classes de entidade para Item e Carrinho .
	- [x] Criar interfaces de repositório para Item e Carrinho que estendem JpaRepository .
- [x] 1. Criar Serviços:
	- [x] Implementar serviços para gerenciar a lógica de negócio de Item e Carrinho .
	- [x] Garantir a validação de regras de negócio, como quantidade em estoque e cálculo de valor total.
	- [x] Adicionar logs ao longo da execução para ter tracking das execuções.
	- [x] Configurar o Exception Handler para capturar e expor de maneira consistente os erros.
1. Criar Controladores REST:
	1. [x] Criar controladores REST para expor endpoints para as operações de Item e Carrinho .
	2. [x] Seguir as melhores práticas RESTful, como usar os verbos HTTP adequados (GET, POST, PUT, DELETE) e status HTTP corretos.
		1. [x] **Fiquei com dúvida no add e remove item do cart, se é put ou delete, considerei put, pois não apaga o carrinho, apenas tira tal item dele**
2. 10. Testar a API:
	1. [x] Usar o Postman ou outra ferramenta similar para testar todos os endpoints da API.
	2. [x] Escrever testes unitários para garantir que as regras de negócio estão sendo aplicadas corretamente

- [x] Usar Lombook
- [x] Usar Flyway
- [x] Tudo em engish
- [x] asssociar ao handlerexception
- [x] deixar a mensagem na exceção ao inves de criar uam excetion
- [x] passar bad requestion (cliente fez requisição errada)
- [x] fazer tracking com slf4j

CRIAR UMA NOVA PULL REQUEST
