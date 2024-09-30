[[Estudos]][[FIAP]]
Azure DevOps da Microsoft oferece uma série de ferramentas integradas, projetadas para suportar o desenvolvimento, teste, implantação e a monitoração de apps, sejam na nuvem ou sistemas locais

Ofere recursos integrados que você pode acessar por meio do seu navegador web ou do cleinte de IDE. 

Podendo escolher apenas oque precisa para complementar seus fluxos de trabalho existente

Segue alguns serviços

| **Serviço**          | **Descrição**                                                                                                                                                              |
| :------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **Azuera Boards**    | Conjunto de ferramentas Agile para dar apoio ao trabalho de planejamento e acompanhamento, aos defeitos de código e aos problemas de uso dos métodos Kanban e Scrum.       |
| **Azuera Repos**     | Repositórios Git ou Team Foundation Version Control (TFVC) para controle da fonta do seu código.                                                                           |
| **Azure Pipelines**  | Fornece serviços de compilação e lançamento para dar suporte á integração contínua e á distribuição de seus aplicativos.                                                   |
| **Azure Test Plans** | Fornece várias ferramentas para testar seus apps, incluindo testes manuais/exploratórios e testes contínuos.                                                               |
| **Azure Artifacts**  | Permite que as equipes compartilhem pacotes como o Mavem, npm, NuGet e muitos outros de fontes públicas e privadas e integrem o compartilhamento de pacotes aos pipelines. |
[Manifesto para o Desenvolvimento Ágil de Software](https://agilemanifesto.org/iso/ptbr/manifesto.html)


## Ambiente Azure DevOps

## Preparação do ambiente

 - Conta github 
 - Acesso ao email institucional
 - Conta Azure

### Configuração da Conta Azure

1. Acesso ao [Portal Azure](https://portal.azure.com/#home)
2. Login com @fiap.com.br
3. Benefícios do aluno, Explorar > iniciar processo para ativar seu perfil de estudante (credito de US$ 100) > Experimentação gratuia > autenticar usando o email da @fiap
4. Redirecionamento para a tela de "Visão Geral"

## Azure boards (Pique Kanban)

![[Pasted image 20240926134233.png]]
### Basic 
Ideal para pequenas equipes ou projetos com requisitos simples, focando em tarefas básica e gerenciamento de bugs.

### Scrum
Perfeito para metodologias Scrum, facilitando a gestão de sprints, planejamento de produto e revisões de sprint.

### Ágil
Adequado para equipes que implementam práticas ágeis, mas com maior flexibilidade do que o estrito SCRUM, permitindo abordagem mais fluida ao planejamento iterativo.

### CCMI (Capability Maturity Model Integration)
Recomendado para organizações que necessitam de processos rigorosos de gerenciamneto de projetos e qualidade, suportando gerenciamento detalhado de requisitos e controle de mudanças.

### Processos no Azure Boards


![[Pasted image 20240930134639.png]]

### Principais diferenças entre os quatros processos padrão

![[Pasted image 20240930134813.png]]

### BASIC

![[Pasted image 20240930135843.png]]
Modelo ideal para equipes que necessitam de um processo de gerenciamento de tarefas direto e sem complicações.

Foca em proporcionar uma bisualização clara do ciclo de vida do item de trabalho, poucos estados e transições simplificadas, facilitando para equipes prequenas ou menos complexas.

#### Critérios para escolha

- Busca abordagem direta e sem complicações
- Problema, Tarefa e Épico
- Ideal para projetos menores ou equipes que não necessitam de processos complexos de gerenciamento.

### SCRUM

![[Pasted image 20240930141026.png]]
Para equipe que seguem a metodologia Scrum, enfatiza sprints, backlogs de sprint e revisões de spring.
Projetado para suportar o ritmo rápido e itrerativo do SCRUM, com estados que refletem as fases de planejamento, desenvolvimento, revisão e laçamento de software.

#### Critérios para escolha

- Equipes que ja implemetam metodologia ágil.
- Eficaz para gerencia a lista de pendências do produto e bugs.
- Utiliza um quadro Kanban para visualizar o fluxo de trabalho.
- Suporta sprints e ajuda a manter todos na equipe alinhados com os objetivos do sprint e do projeto.
### AGILE

![[Pasted image 20240930141043.png]]

Suporta abordagem mais flexivel do que o SCRUM, ideal para equipes que utiizam práticas ágeuis, mas necessitam de mais liberdade do que as estruturas tradicionais do SCRUM.
Permite maior variedade de tipos de itens de trabalho e transições mais fluidas, suportando um ambiente dinâmico de desenvolvimento.

#### Critérios para escolha

- Planejamento mais flexivel.
- Permite rastrea histórias de user e opcional bugs de maneira eficiente.
- Por meio de um quadro Kanban
- Favorece equipe que precisam de flexibilidade para adaptar seus processos de trabalho conforme o projeto evolui.

### CMMI (Capability Maturity Integration)

![[Pasted image 20240930141439.png]]

Destinado a projeto que requerem um alto nível de governaça e documentação.
Este modelo é caracterizado por processos mais formais e um controle rigoro sobre as alterações, adequado para indústrias e projeto que necessitam de aderência estrita e padrões e regulamentações.

#### Critérios para escolha

- Para projetos que exigem mais aderência a processo formais e proporcionam uma estrutura rigorosa para aperfeiçoamento continuo. 
- Recomendado para equipes que seguem metodologias de projetos mais estruturadas e que necessitam de um registro auditável de decisões e mudanças.
- Muitas vezes preferido em ambientes que requerem altos níveis de conformidade e governança.

## Azure Repos

![[Pasted image 20240926134743.png]]
Controle e colaboração no gerenciamento de código
Suporta dois principais tipos de controle de versão:

- Git
- TFVC (Team Foundation Version Control), um sistema de controle de versão centralizado, que mantém um único repo no servidor. Ideal para projeto que necessitam de uma política centralizada de acesso e controle sobre as operações de check-in.

### Benefícios do Azure Repos

- Se integra perfeitamente com Azure Pipelines, proporcionando um cíclo de vida de desenvolviment contínuo e eficiente.
- Historico de versões
- Colaboração aprimorada
- Segurança e controle


## Azure Pipelines

![[Pasted image 20240926140721.png]]
Automatizando o ciclo de vida do desenvolvimento de software

É uma ferrramente esencial no ecossistema Azure DevOps
Desenhada para automatizar não apenas o processo de build e test, mas também a implantação de aplicações em qualquer ambiente, nuvem, híbrido ou on-premises.
Atráves do CI/CD, facilita a imlpementação de práticas DevOps, permitndo que squads entreguem software de forma mais rápida.

### Principais caracteristicas:

- Suporte a múltiplos idiomas e plataformas

- Integração continua, automatiza a compilação e o teste do seu código sempre que uma mudança é feita, proporcionando feedback imediato sobre a saúde do código.

- Entrega contínua, permite que mudanças de código aprovadas sejam automaticamnete enviadas para produção

- Config flexível, através de pipelines definidos com código (YAML), permite que você configure detalhamente cada etapa do processo de build e release, desde a execução de testes automatizados até a implantação em diferentes ambientes.


## Azure Test Plans

![[Pasted image 20240926142857.png]]
Aprimorando a qualidade de software com testes colaborativos
Solução baseada em navegador, acessivel a todos os membros da equipe.
Oferece conjunto robusto de funcionalidades para gestão de testes exploratórios e até coleta de feedback de stakeholders.

### Principais caracteristicas

- Testes manuais planejados
- Testes de aceitação do usuário
- Testes exploratórios
- Coleta de feedback

## Azure Artifacts

![[Pasted image 20240926144145.png]]
Gestão de pacotes e integrações em DevOps
Desenvolvedores podem publicas, consumir e gerenciar pacotes de uma variedade de fontes e formatos, incluind feeds públicos como PyPl, Maven Central, NuGet.
Permite uma intergração perfeita de componenetes de software, garantindo que as equipes possam faciltmente compartilhar e reutilizar código dentro e fora de suas organizações.

Integração com Azure Pipelines é outro recurso significativo, que permite automatizar a criação, teste e implantação de pacotes no decorrer de um pipeline CI/CD

### Alguns benefícios

- **Centralização de dependências**, mantendo todas dependências em um repositório centralizado, facilitando o acesso e a gestão por parte de toda equipe.
- **Controle de versão**
- **Segurança e conformidade**



## Visão geral do Azure DevOps

Fazer o passo a passo 4/8
### Organização

Podemos criar organizações para toda empresa, para um grupo selecionado ou para uso individual, oque facilita gerenciamento de permissões, políticas e a visibilidade dos processos em difernetes níveis. Promovendo a govenança de TI eficiente e centralizada.

**Assisti o video Explorando e Navegando nas ORGS 3/8**
### Projeto

Contém diversos recursos, incluindo quadros e backlogs para planejamento ágil, pipelines para integração e implantação continua, repo para controle de version e gerenciamneto de código fonte, além da integração contínua de testes em todo o ciclo de vida do projeto.
Permite a configuração detalhada de seguran,a e controle de acesso.

### Equipe

É um unidade dentro do Azure DevOps que sporta diversas ferramentas configuráveis pela própria equipe.
Auxiliam no planejamento e gerenciamento do trabalho, facilitando a colaboração.
Cada equpe possui seu próprio backlog e pode configurar suas próprias sprints, metas e utilizar dashboards custom para monitorar o progresso e métricas chave.


