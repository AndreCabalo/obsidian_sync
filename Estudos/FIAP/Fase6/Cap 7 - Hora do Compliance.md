
# Práticas da Qualidade

## Planejamento, Monitoramento e Controle

## Execução de processos

## Técnicas para identificação de problemas

## Rastreabilidade dos impactos dos problemas

## Auditoria de qualidade



# Entendendo Bugs

Termos surgiu em 1947 onde a pioneira da computação Grace Hooper encontrou um inseto (mariposa), preso em um relé do computador Mark II na Universidade de Harvard. Assim foi marcado o primeiro caso documentado do termo "bug"

## Classificação de bugs

### Bugs funcionais
Relacionados a funcionalidades específicas do software. Por exemplo um botão que deveria salvar dados, mas não realiza essa operação.

### Bugs desempenho
Afetam a velocidade e eficiência do software. Por exemplo um arquivo demorando muito para carregar.

### Bugs de interface
Envolvem problemas na interface gráfica que afetam a usabilidade. Por exemplo elementos na interface que estão fora de lugar ou botões que não respondem ao clique.

### Bugs de segurança
Refere-se a vulnerabilidade no software. Por exemplo uma falha que permite o acesso não autorizado a dados sensíveis.

### Bugs de compatibilidade
Quando o software não funciona corretamente em diferentes ambientes ou dispositivos. Por exemplo um app que opera em iOS, mas apresenta problemas em Android.

### Bugs de conectividade
Problemas na comunicação entre o software e outros aplicações ou redes. Por exemplo a falha na conexão com um servidor ou a dificuldade de integrar corretamente com APIs de terceiros.

### Bugs de dados
Problemas na manipulação e armazenamento de dados, como quando dados são corrompidos durante a gravação ou infos são lidas incorretamente do banco de dados.

### Bugs de lógica
Falhas na lógica da programação. Por exemplo um cálculo que retorna um valor errado devido a um erro na fórmula implementada.

### Bugs usabilidade
Afetam a facilidade com que os usuário interagem com o software. Por exemplo um fluxo de navegação confuso ou difícil de entender.

### Bugs de instalação
Problemas que afetam a instalação ou atualização do software. Por exemplo durante o processo de instalação ocorre uma falha que impede que o software seja instalado corretamente.

### Bugs de integração
Quando módulos ou sistemas são combinados e enfrentam problemas. Por exemplo quando módulos funcionam bem de forma independente, mas falham ao serem integrados. 


# Tipos de testes

Exemplo 1- 
![[Pasted image 20241015193820.png]]

Exemplo 2 - 
![[Pasted image 20241015194022.png]]

## Testes unitários
- Realizados a nível de código e focados em métodos e funções individuais.
- Conhecidos por sua automação eficiente, rápida execução e facilidade de diagnóstico
- Exemplo:
	Um teste de unidade que verifica se uma função retorna o resultado correto, retornando 8 ao somar 3 e 5.
## Testes de integração
- Complementam os testes unitários ao avaliar como diferentes módulos de serviço interagem quando combinados.
- Este teste identifica problemas nas interfaces entre módulos, como incompatibilidade de dados ou falhas de comunicação.
- Exemplo:
	Em um aplicativo de lista de tarefas, um teste de integração verifica se uma nova tarefa adicionada parece corretamente na lista, garantindo que os módulos de adicionar e exibir tarefas funcionem bem juntos.

## Teste Funcional
- Objetivo assegurar que os objetivos das tasks estão sendo atendidos
## Teste Não Funcional
- Testando elementos externo do software
- Que impactam na experiencia de uso do usuário
- Por exemplo, testes de segurança.
## Testes de regressão/ confirmação
- Sempre que um componente de software é editado.
- Testas a integração com todos componentes que trabalham em conjunto com este software, afim de garantir a integração.
-  Sempre que houver alterações, rodar os testes antigos para ver se ele continua atendendo os requisitos.
## Testes de desempenho
- Focado em escalabilidade, verificamos como o sistema se comporta sob diferentes cargas de trabalho, medindo a confiabilidade, velocidade, escalabilidade e a capacidade de resposta do aplicativo.
- Exemplo:
		Testar o desempenho de um aplicativo de streaming de vídeo pode revelar gargalos na capacidade do servidor ao lidas com muitos usuários simultâneos, indicando a necessidade de melhorias na infra.

## Testes de segurança
- Essenciais para garantir que o software esteja protegido contra ameaças e vulnerabilidades.
- Eles incluem testes de penetração para simular ataque e identificar falhas de segurança.
- Verifica também as normas de segurança.
- Exemplo:
		Um app bancário online, um teste de penetração pode relevar uma vulnerabilidade na autenticação de dois fatores, destacando a necessidade de correção para proteger os dados financeiros dos usuários.
## Testes exploratórios
- Permite que os testadores explorem o software de forma criativa e intuitiva, sem seguir um roteiro predefinido.
- Exemplo:
		Um app de e-commerce, pode identificar que a aplicação apresenta lentidão ao aplicar vários filtros de pesquisa rapidamente, um problema que pode passar despercebido em testes automatizados.

# Técnicas de testes

Existem duas técnicas bem conhecidas, a de caixa branca e caixa preta.

Exemplo 1 -
![[Pasted image 20241015200135.png]]

Exemplo 2 - 
![[Pasted image 20241015200242.png]]
## Testes de caixa branca/ Estrutural
- Dev possui acesso ao código-fonte, verifica a lógica técnica.
- Um teste que se preocupa com oque acontece dentro do software para analisar desempenho.
- Desenvolvedor se preocupa com as entradas, a forma como o software as trata.
- Trabalham com telemétria.
	(Como o software vai se desenvolvendo, entendendo tempo de resposta e dados de desempenho)
## Testes de caixa preta
- O testador não possui conhecimento sobre o código-fonte e foca apenas nas atendas e saídas.
- Lembra o conceito da avião, oque acontece aqui dentro não é conhecido, mas todos os dados são armazenados aqui, se necessários abrir, temos todas as infos aqui dentro.


# Pirâmide de testes

Sugere a proporção ideal de diferentes testes para garantir uma cobertura eficiente e eficaz.
A medida que se sobe na pirâmide, os testes tornam-se mais lentos e caros, por isso devem ser menos numerosos.
Essa distribuição ajuda a detectar e corrigir problemas de forma eficiente e econômica.

![[Pasted image 20241015200821.png]]

# Norma Internacional ISO/IEC 25010:2011
Amplamente conhecida e utilizada na indústria para assegurar que os produtos de software sejam seguros, eficientes e satisfatórios.

Divide a qualidade em duas categorias principais:

## Qualidade do uso
- Concentra-se na experiência do usuário final.
- Composto por 5 características 
![[Pasted image 20241015213711.png]]
	 **Eficácia** - 
		Exemplo Positivo:
			Google Search onde as pesquisas são relevantes e eficientes. 
		Exemplo Negativo:
			Apple Mapas, com direções imprecisas e dados incorretos.
	 **Eficiência** - 
		Exemplo Positivo:
			Amazon Prime, oferecendo entregas rápidas com custo baixo para os usuários.
		Exemplo Negativo:
			Checkout automatizado de algumas redes de supermercado, que frequentemente tem problemas técnicos.
	**Satisfação** -
		Exemplo Positivo:
			Aplicativo de mensagens Slack, com sua interface intuitiva e experiência agradável.
		Exemplo Negativo:
			Windows Vista, interface confusa e problemas de desempenho.
	**Segurança** -
		Exemplo Positivo:
			Gerenciador e cofre de senhas LastPass, com suas robustas medidas de segurança.
		Exemplo Negativo:
			Vazamento de dados do Facebook em 2018.
	**Cobertura do contexto** - 
		Exemplo Positivo:
			Microsoft office, oferecem suporte para diversas plataformas e dispositivos, exemplo em cobertura do contexto.
		Exemplo Negativo:
			Apple Maps por sua imprecisão, falta de suporte para diferentes contextos e usos, especialmente quando comparado ao Google Maps da época.
		
## Qualidade do produto
- Abrange as características inerentes ao software.
- Composto por 8 principais categorias:
![[Pasted image 20241017180945.png]]
	- Adequação funcional
		- Podendo ser analisado sob 3x princiais dimensões:
			- Completude funcional, verifica se o software tem todas as funções necessárias para realizar as tarefas previstas.
			- Correção funcional, refere-se á precisão dos resultados produzidos pelas funções do software.
			- Pertinência funcional, avalia se as funções do software são adequadas para as tarefas que se propõem a realizar.
	- Desempenho
		- Avaliamos a rapidez com que o software responde e o quão eficiente utiliza os recursos. Este aspecto pode ser analisado sob três principais dimensões:
			- Comportamento em tempo avalia a rapidez com que o software responde ás ações dos usuários e executa suas funções.
			- Recursos utilizados
			- Capacidade, refere-se á habilidade do software em lidar com grandes volumes de dados e transações esperadas.
	- Compatiblidade
		- Pode ser dividido em duas principais dimensões:
			- Coexistência, refere-se á capacidade do software de operar sem conflitos junto a outros produtos no mesmo sitema.
			- Interoperabilidade, diz a respeito da habilidade em se comunicar e operar com outros sistemas ou produtos.
	- Usabilidade
		- Capacidade de ser entendido avalaia se os usuários conseguem compreender como usar o software.Sendo intuitivo.
		- Capacidade de aprendizagem.
		- Operacionalidade, mede a facilidade com que os user podem operar e controlar o software.
		- Estética da interface
		- Acessibilidade analise se o software é acessível a todos os user, incluindo aqueles com deficiência.
	- Confiabilidade
		- Capacidade de recuperar-se de falhas, divida em quatro dimensões:
			- Maturidade, nivel de refinamento do software ao longo do tempo.
			- DIsponibilidade.
			- Tolerância a flahas, mede a capacidade de lidar com falhar de maneira controlada.
			- Capacidade de recuperaçãso, eficácia em se recuperar rapidamente de falhas. Exemplo o banco Oracle.
	- Segurança
		- Confidencialidade
		- Integridade, prevenir modificações não autorizadas nos dados.
		- Não-repúdio envolve a capacidade de fornecer provas de ações realizadas, por exemplo o blockchain do Bitcoin que ofeere um registro imutável e verificável de todas as transações.
		- Autenticidade é a verificação de identidade do user, por exemplo o multifator da microsoft e da google.
		- Responsabilidade, refere-se a capacidade do software de rastrear ações dos user.
	- Manutenibilidade
		- Garante que o software possa ser facilmente ajustado ao longo do tempo
		- Cinco dimensões:
			- Modularidade
			- Reusabilidade
			- Analisabilidade, facilitar o diagnostico.
			- Modificabilidade, facilidade com que o software possa ser alterado.
			- Testabilidade.
	- Portabilidade
		- Avaliar a adaptação do software, divida em três dimensões:
			- Adaptabilidade, habilidade de se ajustar a diferentes ambientes e plataformas.
			- Instabilidade, capacidade de ser instalado em diferentes ambientes, por exemplo a combinação de ferramentas com maven e gradle no java.
			- Substitutibilidade, capacidade de subistituir por outro produto de software em determinado ambiente.


# Norma ISO/IEC 29119 Testes de Software

Estabele norams internacionais que uniformizam os processos de testes de software.

## Componentes principais

3/9 