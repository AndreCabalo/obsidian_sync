
## Recreate Deployment

Desativa todas as instâncias da versão atual da app antes de ativas a nova versão
Isso garante que não haja coexistência de versões diferentes

### Processo
Paralisa todas as instâncias da versão atual da aplicação.
Implanta a nova versão da aplicação
Inicia as novas instâncias.
### Vantagens
Simples de implementar e gerenciar
Evita problemas de compatibilidade entre versões diferentes

### Desvantagens
Causa tempo de inatividade, pois todas as instâncias antigas são desativadas antes que as novas sejam ativadas.
Pode não ser adequado para aplicações que exigem alta disponibilidade.

![[Pasted image 20240919154020.png]]

## Shadow Deployment

Implanta a nova versão da app em paralelo com a versão atual.
O tráfego é espelhado (copiado) para a nova versão para testes, mas as respostas não são retornadas aos usuários.

### Processo
Implanta a nova versão da aplicação em paralelo com a versão atual.
Espelha o tráfego do usuário para a nova versão.
Monitora a nova versão para verificar o desempenho e identificar problemas.
Após a validação, promove a nova versão para produção.

### Vantagens
Permite testes em condições reais sem impactar os usuários.
Facilita a identificação de problemas de desempenho e compatibilidade.

### Desvantagens
Pode ser complexo e caro de configurar.
Requer recursos adicionais para executar ambas as versões simultaneamente.

![[Pasted image 20240919154957.png]]

## Dark Launching

Implanta a nova versão da app em produção, mas novos recursos são mantidos ocultos, para a maioria dos user até que estejam prontos para serem lançados.

### Processo
Implanta a nova versão da aplicação em produção.
Usa feature flags para manter novos recursos desativados.
Ativa os novos recursos para um subconjunto de user ou em fases.
Monitora o uso e desempenho dos new resources.
Gradualmente, ativa os new resources para todos user.

### Vantagens
Permite testar new resouces em um ambiente de produção real.
Reduz o risco de falhas catastróficas ao lançar novos recursos gradualmente.

### Desvantagens
Requer um gerenciamento cuidadoso de recursos ocultos.
Pode ser difícil de monitorar e testar completamente.


# Ferramentas e serviços para deployment na nuvem


## Azure APP Services

Solução de plataforma como serviço (PaaS) que facilita a construção e hospedagem de aplicções web e APIs em diversas linguagens e frameworks. 

Oferece escalabilidade automática que ajusto os recursos conforme a demanda, sem intervenção manual, e suporta CI/CD com ferramentas como Azure DEvops e Github Actions.

Aém disso o Azure App Service suporta uma ampla gama de linguagens como .NET, Java, PFP, Node.js, Python e Ruby.

No entenato, pode ser mais custosos do que gerenciar diramente a infra, especialmente para aplicações de larga escala.

Também pode aprsentar limitações em termos de config e personalização, pois os user estão restritos aos templates e config predefinidos pela plataforma

## Google APP Engine

Também é uma plataforma como serviço (PaaS), que permite aos devs criar e hospedar app diretamente na infra do Google.

Suporta várias linguagens de programação, como Python, Java, PHP, Node.js, Ruby, Go e outras.

Realiza escalabilidade automática, conforme carga de trabalho aumenta ou diminui.

Gerenciamento das app é simplificado com automações para balaceamento de carga, monitoramento e atualizações de segurança.

Há limite em termo de personalização de configs, que podem ser um desafio para projetos que necessitam de ajustes mais específicos.

## AWS Elastic Beanstalk

Oferece uma abordagem de plataforma como servi;o (PaaS) dentro do ecossistema da AWS.

SUporta múltiplas linguagens de programação e frameworks como Java, .NET, Node.js, Python, Ruby, Go e containers Docker.

A plataforma automatiza vários aspectos do deploy, desde o provisionamento de recursos até a escalabilidade e monitoramento, permitindo aos devs se concentrarem no código ao invés da infra.

Elastic Beanstalk se intragra facilmento com outros services da AWS, como RDS para bancos de dados, S3 para armazenamento e CloudWatch para monitoramento.

Pórem os user tem um controle menor sobre a infra subjacente em comparação com soluções IaaS, e os custos podem ser mais altos do que gerenciar a infra diretamente.


# CI/CD

Objetivo de automatizar e melhorar o processo de desenvolvimento de software, desde a codificação até a entrega em prod.

## Integração continua (CI)
Prática onde os devs combinam seu trabalho em um repositório compartilhado.
Cada integração é verificada por meio de builds automatizados e testes, para detectar rapidamente problemas de integração. 

Esse processo reduz os riscos de implantação, pois faz a integração de pequenas mudanças e forma mais frequente, com isso os devs conseguem testar e receber um feedback mais rápido sobre a qualidade do software.

## Entrega continua (CD)

Garanteque o software esteja sempre pronto para ser lançado, promovendo entregas mais rápidas, consistentes e de alta qualidade.

A entrega contínua estende os princípos da intregração continua ao assegurar que cada alteração no código permaneça em um estado pronto para produção.

Envolve a automoção de todas as fases do processo de deploy até a fase final, que geralmente é uma implantação manual. Reduzindo significamente o tempo entre a concepção e a utiliza,ão pelo user e também minimiza os riscos através da automação extensiva.


## Ferramentas comuns de CI/CD

### Jenkins
- Uma das ferramenta open-source mais utilizadas para automação de CI/CD.
- Possui uma grande comunidade e muitos plugins.
- Permite personalização extensa para atender ás necessidade espec;ificas de diferentes projetos.
- Manutenção e config podem ser complexas, exigindo conhecimento técnico aprofundado para aproveitar plenamente as funcionalidades.

### Github Actions
- Integrada diretamente ao Github, facilita a automação de workflows de CI/CD dentro do próprio repositório do projeto.
- Valorizada por sua integração nativa com o Github, simplificando a config de pipelines.
- Embora seja fácil usar e configurar, pode apresentar limitações em comparação com outras plataformas de C/CD mais robustas, especialmente em projetos complexos ou de grande escala.

### GitLab CI/CD
- Embutido no GItlab, oferece uma solução altamente integrada que permite os devs configurar pipelines detalhadas, diretamente através de arquivos YAML no repositório do projeto.
- A integração nativa com o GitLab simplifica muitos aspectos do processo, mas a riqueza de funcionalidades e a flexibilidade dos pipelines podem ser desafiadores para usuários iniciantes.

### Azure DevOps

- Conjunto (da Microsoft) completo de ferramentas que suportam não apenas CI/CD mas também gerenciament ode projetos e colaboração de equipes.
- Se destaca pela sua integração com outros serviços Azure e pela sua robustez de suas funcionalidades, incluindo pipelines complexos e gestão detalahda de artefatos.
- Contudo a plataforma pode ter uma curva de aprendizado íngreme e dependendo da config, pode ser mais cara do que outras soluções.

# Preparação para o Deploy na Nuvem

Objetivo, orientar a criar e implatar app desenvolvimento em Python na nuvem Azure, utilizando github como ferramenta de controle de versão.

Pré-requisitios e etapas de config:

- Conta na Microsoft Azure
- Conta no GitHub
- Instalacação de bilbioteca Git
	- Necessário instalar a biblioteca Git em sua máquina.
	-
## Video - Construção e disponibilização de app na nuvem 6/11

