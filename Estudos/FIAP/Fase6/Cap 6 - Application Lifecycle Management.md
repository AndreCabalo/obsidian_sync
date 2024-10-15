Serão estudados nesse capítulo, os ciclos de vida do software em duas situações portanto:

- Ciclo de vida de desenvolvimento de software.
- Ciclo de vida do software em uso.

	Todo software que um dia foi inovador e desejado, chegará ao ponto de sua aposentadoria de uso, em função de fatores como:
	- Obsolescência tecnológica.
	- Obsolescência de negócio.
	- Elevados custos de manutenção.
	Na maioria das vezes, em casos como os citados a cima, é mais rápido e barato construir um novo software, ao invés de tentar fazer adaptações neste.

# 4 modelos de ciclo de vida

## Cascata
- Execução de projeto Burocrática
- Evita mudança de escopo
- Administração mais tranquila
- Mudanças são postergadas para outras etapas, ou seja, entregamos o combinado e se tiver mudanças, serão tratadas posteriormente em um novo ciclo de projeto.
- Caminha entre etapas, onde a equipe trabalha junto em cada uma dessas fases:
	- Analise.
	- Desenho da solução, explicando o funcionamento previsto, protótipo e documentação.
	- Implementação, construção, programação da aplicação, testes unitários.
	- Testes de integração da aplicação, homologação com o cliente final.
	- Implantação, finalizar manuais, helps de sistemas, treinamento e treinamento suporte, carregar dados do legado, conectar com legado para pegar funções do legado.
	- Manutenção/Sustentação do sistema.
## Incremental
- Evolução cascata, onde quebramos o projeto em módulos(rh, controle de estoque, fluxo caixa).
- Com módulos independentes e que fazem comunicação com os demais.
- Burocracia, mínima mudança.
- Maior flexibilidade, com varias frentes de trabalho, cada um rodando sua cascata, paralelizado.
- Entregas parciais de cada módulo, se desejar.
	- Etapas do desenvolvimento similar ao cascata
## Evolutivo
- Ja temos um certo conceito ágil.
- Agora não quebramos mais por módulos, mas sim por funcionalidades, onde prototipamos cada função (tela), não pegamos o modulo RH todo, mas sim a função admite funcionário.
- Entrega por função, não por modulo e muito menos todo de uma só vez.
- Etapas
	- Etapa de analise, pegamos o funcionamento das funcionalidades.
	- Desenhos de engenharia e protótipos para validar cada função.
	- Construção de cada função.
	- Teste de cada função.
	- Entrega de cada função.
## Espiral
- Definitivamente trouxe o cenário Agile.
- Scrum, extreme programing, são modelo espiral.
- Trabalhamos agora com componente, e não uma função como todo. Por exemplo consulta no banco e traga info (isso é um componente).
- Componentes entregáveis. Para que outros pedaços do software possam usar.
- Um pagina de formulário é um componente entregável, a função por traz do botão é outro componente entregável. Guardar essas infos no banco de dados é outro componente entregável. 
- Quebramos em 3x entregas diferente. Front, Back, Banco.


# Plano de projeto

## Cascata
Usamos o MS Project.
![[Pasted image 20241010203931.png]]![[Pasted image 20241010204011.png]]

## Incremental
Por módulo, cada modulo, temos um cascata.
![[Pasted image 20241010204436.png]]![[Pasted image 20241010204541.png]]

## Evolutivo
Não usaremos mais MS Project.
Agora trabalharemos por função.
Método ágil, por tanto usaremos o painel Azure Boards.
- Módulos = Epic.
	- Funções = Feature.
		- Produto backlog = Aplicação.		
![[Pasted image 20241010205426.png]]![[Pasted image 20241010205501.png]]

## Espiral
SCRUM -> 
Entrega a cada componente útil.
Entregas constantes.
Permite redefinição/adaptar o projeto.
Equipes pequenas que possamos acompanhar dia-a-dia.
	Epic -> Assunto - Recrutamento de seleção de colaboradores
		Função-> Feature - Função publicar vaga
			Produto Backlog -> Componentes (tipo um método criado, ex: validar senha)
Uma função - Feature é uma sprint.

![[Pasted image 20241010211821.png]]
![[Pasted image 20241010211511.png]]![[Pasted image 20241010212043.png]]

# Ciclo de vida de Software em uso

![[Pasted image 20241010212410.png]]

Manutenções e atualizações podem aumentar o a vida durante o declínio.

## Introdução
Surgem os primeiros interesses pelo software, ainda podem existir problemas com a aplicação (bugs) e a equipe focada á liberação de uso (imediate after-go-live)


## Crescimento
Os clientes atuais satisfeitos ajudam a impulsionar o aumento da clientela.
A equipe de devs passa ser liberada para outras atividades dada a estabilização do software e da sua qualidade.

Nesse momento a desenvolvedora deve então, iniciar um novo projeto para a geração/versão do seu produto, dado que a totalidade ou grande parte da equipe de devs está liberada de trabalhos de manutenção do sistema em operação.

Os serviços de suporte técnico e serviços de operação estão em pleno exercício.
## Maturidade
A comunidade confia no produto e ele alcança sua quantidade máxima de user.
No ápice da maturidade, a comercialização do software não cresce mais.

A partir desse momento a expectativa é que o interesse dos clientes caia e novos potenciais clientes percam interesse em adquiris o software.

É A HORA que a empresa desenvolvedora do sistema libera para o mercada um nova geração de produto para ocupar o espaço que começa a ser deixado pelo produto que alcançou sua maturidade de emprego.

## Declínio
Quando a quantidade de clientes que aderem ao produto é menor do que a que abandona, até alcançar um momento no qual ninguém mais se interesse pelo software, ocorrendo sua aposentadoria.

Essa curva de declínio de utilização pode ser atenuada e a vida do software prolongada por ações de manutenção feitas pelo fabricante do sistema.

Manutenções que o sistema pode passar são:
- Corretivas
- Adaptativas
- Evolutivas
- Perfectivas

Importante ressaltar que o ciclo de vida bem administrado permite:

- Que compradores do software saibam o melhor momento de adquiria uma nova aplicação, como forma de obter uso pelo maior período possível dos devs trazendo excelente relação custo/benefíco.
- Que a empresa mantenha seus devs ocupados, ocupe o espaço no mercado e dificulte a entrada de concorrentes que substituam sua solução. Garantindo maiores retornos sobre investimentos em pesquisa de desenvolvimento e melhor equalização e custos operacionais.

	![[Pasted image 20241010221201.png]]

# Ciclo de vida de software Produção

Tipos de ciclo de vida e software diferentes apontam para Framework diferentes

## RUP (Rational Unified Process)

- Criado para o ciclo cascata de projeto (Phases)
- Adaptado para o ciclo incremento (Iterations)
	![[Pasted image 20241014200141.png]]
	![[Pasted image 20241014201432.png]]
## Scrum

- Criado para evolutivo/espiral.
- Sprint não é elástica, se não cumprir o time box, a tarefa é enviada para a próxima sprint tbm.
![[Pasted image 20241014201504.png]]

# Melhores práticas de gerenciamento do ciclo de vida em Devops

![[Pasted image 20241014201718.png]]![[Pasted image 20241014201728.png]]

# Ciclo de vida de Software Tendências


- Não existe premissa de um ciclo de vida especifico.
- Oque irá te guiar para um tipo de ciclo são as os fatores:
	- Burocracia
	- Prazo
	- Definição ou falta de definição
	- Flexibilidade do projeto.