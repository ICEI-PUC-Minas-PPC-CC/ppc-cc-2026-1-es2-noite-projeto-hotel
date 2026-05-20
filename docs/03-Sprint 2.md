# Metodologia

O desenvolvimento do projeto Hospfy será realizado utilizando metodologias ágeis, com foco em organização incremental das funcionalidades e colaboração entre os integrantes da equipe. O grupo definiu uma estrutura baseada em arquitetura em camadas, buscando melhorar a manutenção, escalabilidade e separação de responsabilidades do sistema.

O projeto possui como objetivo desenvolver uma aplicação móvel para gerenciamento de solicitações e comunicação interna em hotéis, permitindo integração entre hóspedes, funcionários e gestores por meio de uma plataforma digital centralizada.

A equipe utilizará ferramentas modernas para desenvolvimento mobile, versionamento, comunicação e gerenciamento das tarefas do projeto, visando melhorar a produtividade e organização durante todas as etapas do desenvolvimento.

---

## Relação de Ambientes de Trabalho

| Ambiente | Plataforma | Finalidade | Link |
|---|---|---|---|
| Desenvolvimento Front-end Mobile | React Native + Expo | Desenvolvimento da aplicação móvel | https://reactnative.dev |
| Desenvolvimento Back-end | Node.js | Desenvolvimento da API e regras de negócio | https://nodejs.org |
| Banco de Dados | Firebase Firestore | Persistência de dados em tempo real | https://firebase.google.com |
| Controle de Versão | GitHub | Hospedagem do repositório e versionamento | https://github.com |
| Editor de Código | Visual Studio Code | Desenvolvimento do código-fonte | https://code.visualstudio.com |
| Comunicação da Equipe | WhatsApp | Comunicação rápida entre os integrantes | https://www.whatsapp.com |
| Modelagem e Diagramas | Draw.io | Criação de diagramas UML e fluxos | https://app.diagrams.net |
| Gerenciamento do Projeto | GitHub Projects | Organização e acompanhamento das tarefas | https://github.com/features/issues |

---

## Controle de Versão

A ferramenta de controle de versão adotada no projeto foi o
[Git](https://git-scm.com/), sendo que o [Github](https://github.com)
foi utilizado para hospedagem do repositório.

O projeto segue a seguinte convenção para o nome de branches:

- `main`: versão estável já testada do software
- `unstable`: versão já testada do software, porém instável
- `testing`: versão em testes do software
- `dev`: versão de desenvolvimento do software

Quanto à gerência de issues, o projeto adota a seguinte convenção para etiquetas:

- `documentation`: melhorias ou acréscimos à documentação
- `bug`: uma funcionalidade encontra-se com problemas
- `enhancement`: uma funcionalidade precisa ser melhorada
- `feature`: uma nova funcionalidade precisa ser introduzida

A configuração do projeto no GitHub foi estruturada visando facilitar o desenvolvimento colaborativo e a organização do código-fonte. Cada integrante trabalha em funcionalidades específicas dentro da branch `dev`, realizando commits frequentes e descritivos para facilitar o acompanhamento das alterações realizadas no sistema.

Após o desenvolvimento das funcionalidades, as alterações passam pela branch `testing`, onde são realizados testes e validações. Posteriormente, as funcionalidades são integradas à branch `unstable` e, após validação completa, são enviadas para a branch `main`, que representa a versão estável do projeto.

Os commits seguem um padrão descritivo, facilitando o entendimento das alterações realizadas. Exemplos:

- `feat: criação da tela de solicitação de serviços`
- `fix: correção no acompanhamento de status`
- `docs: atualização da documentação da sprint 2`

Os merges são realizados após validação das funcionalidades implementadas, buscando reduzir conflitos e manter a estabilidade do sistema.

O gerenciamento de issues é realizado utilizando o GitHub Issues, permitindo o acompanhamento de bugs, melhorias, documentação e novas funcionalidades do projeto. As etiquetas facilitam a categorização e organização das tarefas desenvolvidas pela equipe.

> **Links Úteis**:
> - [Microfundamento: Gerência de Configuração](https://pucminas.instructure.com/courses/87878/)
> - [Tutorial GitHub](https://guides.github.com/activities/hello-world/)
> - [Git e Github](https://www.youtube.com/playlist?list=PLHz_AreHm4dm7ZULPAmadvNhH6vk9oNZA)
> - [Comparando fluxos de trabalho](https://www.atlassian.com/br/git/tutorials/comparing-workflows)
> - [Understanding the GitHub flow](https://guides.github.com/introduction/flow/)
> - [The gitflow workflow - in less than 5 mins](https://www.youtube.com/watch?v=1SXpE08hvGs)

---

## Gerenciamento de Projeto

### Divisão de Papéis

A equipe utiliza metodologias ágeis, tendo escolhido o Scrum como base para organização do processo de desenvolvimento do projeto.

A equipe está organizada da seguinte maneira:

- Scrum Master: Vinicius Dias Oliveira;
- Product Owner: Matheus Eduardo Silva;
- Equipe de Desenvolvimento: Luis Ricardo Cardoso, Vinicius Dias Oliveira e Matheus Eduardo Silva.

> **Links Úteis**:
> - [11 Passos Essenciais para Implantar Scrum no seu Projeto](https://mindmaster.com.br/scrum-11-passos/)
> - [Scrum em 9 minutos](https://www.youtube.com/watch?v=XfvQWnRgxG0)
> - [Os papéis do Scrum e a verdade sobre cargos nessa técnica](https://www.atlassian.com/br/agile/scrum/roles)

---

### Processo

O processo de desenvolvimento do Hospfy será baseado em sprints incrementais, onde as funcionalidades serão divididas em pequenas entregas ao longo do desenvolvimento do sistema.

A equipe utiliza o GitHub Projects como ferramenta principal para gerenciamento das tarefas e acompanhamento do progresso do projeto. As atividades são organizadas em colunas que representam o fluxo de desenvolvimento, como:

- Backlog
- Em Desenvolvimento
- Em Teste
- Concluído

As tarefas são cadastradas como issues dentro do GitHub, permitindo melhor rastreabilidade das funcionalidades, correções e melhorias implementadas no sistema.

Durante as sprints, a equipe realiza reuniões periódicas para alinhamento das atividades, acompanhamento do progresso e resolução de possíveis dificuldades encontradas durante o desenvolvimento.

Além disso, o Scrum foi adotado visando melhorar a organização, comunicação e divisão das responsabilidades entre os integrantes do grupo.

> **Links Úteis**:
> - [Planejamento e Gestáo Ágil de Projetos](https://pucminas.instructure.com/courses/87878/pages/unidade-2-tema-2-utilizacao-de-ferramentas-para-controle-de-versoes-de-software)
> - [Sobre quadros de projeto](https://docs.github.com/pt/issues/organizing-your-work-with-project-boards/managing-project-boards/about-project-boards)
> - [Project management, made simple](https://github.com/features/project-management/)
> - [Sobre quadros de projeto](https://docs.github.com/pt/github/managing-your-work-on-github/about-project-boards)
> - [Como criar Backlogs no Github](https://www.youtube.com/watch?v=RXEy6CFu9Hk)
> - [Tutorial Slack](https://slack.com/intl/en-br/)

---

### Ferramentas

As ferramentas empregadas no projeto são:

- Editor de código
- Ferramentas de comunicação
- Ferramentas de desenho de tela (_wireframing_)

As principais ferramentas utilizadas no desenvolvimento do projeto foram escolhidas buscando melhorar a produtividade, facilitar a comunicação entre os integrantes e organizar o desenvolvimento do sistema.

| Ferramenta | Finalidade | Justificativa |
|---|---|---|
| Visual Studio Code | Desenvolvimento do código-fonte | Possui integração com Git e suporte a diversas extensões |
| GitHub | Controle de versão e gerenciamento do projeto | Facilita o desenvolvimento colaborativo |
| React Native | Desenvolvimento mobile | Permite criação de aplicações multiplataforma |
| Expo | Execução e testes da aplicação móvel | Simplifica os testes durante o desenvolvimento |
| Firebase Firestore | Banco de dados em tempo real | Facilita sincronização de informações |
| Draw.io | Modelagem UML e diagramas | Ferramenta gratuita e simples para diagramas |
| WhatsApp | Comunicação da equipe | Comunicação rápida entre os integrantes |

O editor de código Visual Studio Code foi escolhido por possuir integração com Git e suporte às tecnologias utilizadas no projeto. O GitHub foi adotado para versionamento e gerenciamento das tarefas do sistema. Já o Draw.io foi utilizado para criação dos diagramas UML e modelagem das classes do projeto.

As ferramentas de comunicação foram escolhidas visando facilitar a troca de informações entre os membros da equipe durante o desenvolvimento das sprints.
