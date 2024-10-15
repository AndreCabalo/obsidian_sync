 - Sempre que for transascionar entre branch
	 De um git stash para salvar na branch

- Não cria logica em cima de ID
	Por exemplo na tabela CATEGORY, usa o nome ao invés de ID, pois o nome temos controle, ja o ID, não temos, pois o banco em prod pode criar com um ID diferente do local e QA.
	Criar logica sempre em campo mais forte, no caso categoria

- Ao usar métodos, tente verificar a quantidade de vezes que vc manda um query, talvez você possa usar uma query mais complexa, que apensa com uma query você consiga os dados necessarios ao inves de bater no banco diversas vezes.
