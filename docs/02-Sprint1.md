# Sprint 1 — Análise dos Requisitos e Identificação das Classes


# 1. Levantamento de Requisitos

## 1.1 Requisitos Funcionais

| Código | Requisito Funcional | Descrição |
|---|---|---|
| RF01 | Catálogo de Serviços | O sistema deve permitir que o hóspede visualize categorias e serviços disponíveis no hotel. |
| RF02 | Solicitação de Serviços | O hóspede deve conseguir solicitar serviços diretamente pelo aplicativo. |
| RF03 | Observações no Pedido | O sistema deve permitir adicionar observações durante a solicitação. |
| RF04 | Acompanhamento de Status | O hóspede deve acompanhar o status do pedido em tempo real. |
| RF05 | Cancelamento de Pedido | O hóspede poderá cancelar pedidos ainda não iniciados. |
| RF06 | Painel Administrativo | A gestora deve visualizar todas as solicitações em andamento. |
| RF07 | Distribuição de Tarefas | A gestora deve atribuir pedidos aos funcionários. |
| RF08 | Relatórios | O sistema deve gerar relatórios básicos sobre atendimentos e cancelamentos. |
| RF09 | Notificações Push | Funcionários devem receber notificações sobre novas tarefas. |
| RF10 | Aba de Informações | O aplicativo deve disponibilizar informações importantes do hotel. |

---

# 2. Requisitos Não Funcionais

## RNF01 — Tempo Real
O sistema deve atualizar os status das solicitações em tempo real.

## RNF02 — Usabilidade
A interface deve ser simples e intuitiva para hóspedes e funcionários.

## RNF03 — Disponibilidade
O sistema deve estar disponível durante toda a estadia do hóspede.

## RNF04 — Escalabilidade
A arquitetura deve suportar múltiplos hotéis e usuários simultaneamente.

## RNF05 — Segurança
As informações dos usuários e solicitações devem ser protegidas.

---

# 3. Histórias de Usuário Analisadas

| ID | História |
|----|-----------|
| H1 | Catálogo de Serviços |
| H2 | Aba de Informações |
| H3 | Painel de Controle |
| H4 | Campo Observações |
| H5 | Acompanhamento de Status |
| H6 | Cancelar Pedido |
| H7 | Relatório Básico |
| H8 | Notificações Push |

---

# 4. Identificação das Classes

Com base nos requisitos e histórias de usuário, foram identificadas as seguintes classes principais.

---

## 4.1 Classe Hóspede

### Responsabilidades
- Solicitar serviços
- Consultar informações
- Acompanhar pedidos
- Cancelar solicitações

### Principais Atributos
- id
- nome
- numeroQuarto

### Relacionamentos
- Possui vários pedidos

---

## 4.2 Classe Pedido

### Responsabilidades
- Registrar solicitações
- Controlar status
- Armazenar observações

### Principais Atributos
- id
- status
- observacoes
- dataCriacao
- dataInicio
- dataFinalizacao
- dataCancelamento

### Relacionamentos
- Pertence a um hóspede
- Está associado a um serviço

---

## 4.3 Classe Serviço

### Responsabilidades
- Representar serviços disponíveis no hotel

### Principais Atributos
- id
- nome
- descricao
- prazoEstimado
- disponivel

### Relacionamentos
- Pertence a uma categoria

---

## 4.4 Classe Categoria

### Responsabilidades
- Organizar serviços por grupo

### Principais Atributos
- id
- nome

### Relacionamentos
- Possui vários serviços

---

## 4.5 Classe Funcionário

### Responsabilidades
- Executar tarefas
- Atualizar status dos pedidos
- Receber notificações

### Principais Atributos
- id
- nome
- cargo

### Relacionamentos
- Pode atender vários pedidos

---

## 4.6 Classe Gestor

### Responsabilidades
- Gerenciar solicitações
- Atribuir tarefas
- Visualizar relatórios

### Principais Atributos
- id
- nome
- login

### Relacionamentos
- Gerencia funcionários e pedidos

---

## 4.7 Classe Relatório

### Responsabilidades
- Gerar métricas operacionais
- Calcular tempo médio de atendimento
- Exibir cancelamentos

### Principais Atributos
- dataInicio
- dataFim

### Relacionamentos
- Utiliza informações dos pedidos

---

## 4.8 Classe InformaçãoHotel

### Responsabilidades
- Exibir regras e informações do hotel

### Principais Atributos
- titulo
- conteudo

### Relacionamentos
- Disponível para hóspedes

---

## 4.9 Classe Notificação

### Responsabilidades
- Enviar notificações aos usuários
- Registrar mensagens do sistema
- Informar alterações de status

### Principais Atributos
- id
- mensagem
- tipo
- dataEnvio
- status

### Relacionamentos
- Pode ser enviada para hóspedes ou funcionários

---

## 4.10 Classe AtribuicaoPedido

### Responsabilidades
- Relacionar pedidos aos funcionários
- Registrar distribuição de tarefas
- Controlar atribuições

### Principais Atributos
- id
- dataAtribuicao
- statusAtribuicao

### Relacionamentos
- Relaciona Pedido e Funcionário

---

# 5. Relacionamento Entre Classes

O relacionamento principal do sistema ocorre da seguinte forma:

- O hóspede realiza um pedido
- O pedido referencia um serviço
- O serviço pertence a uma categoria
- O gestor visualiza os pedidos
- O gestor atribui pedidos aos funcionários
- O funcionário atualiza o status do pedido
- O sistema envia notificações aos usuários
- O relatório utiliza os dados dos pedidos

---

# 6. Arquitetura Inicial

Foi definida uma arquitetura em camadas para melhorar organização e manutenção do sistema.

---

## 6.1 Controller

Responsável por receber requisições do usuário.

### Exemplos
- PedidoController
- ServicoController
- RelatorioController

---

## 6.2 Service

Responsável pelas regras de negócio.

### Exemplos
- PedidoService
- RelatorioService
- NotificacaoService

---

## 6.3 Repository

Responsável pela persistência dos dados.

### Exemplos
- PedidoRepository
- ServicoRepository
- RelatorioRepository

---

# 7. Estrutura Organizacional das Classes

Para melhorar a organização do sistema e reduzir o acoplamento entre as entidades, algumas responsabilidades foram separadas em classes específicas.

---

## 7.1 Classe PedidoService

Responsável pelas regras de negócio relacionadas aos pedidos.

### Principais Métodos
- criarPedido()
- cancelarPedido()
- atualizarStatus()
- atribuirFuncionario()

---

## 7.2 Classe RelatorioService

Responsável pela geração de métricas e relatórios operacionais.

### Principais Métodos
- calcularTempoMedioAtendimento()
- contarPedidosCancelados()
- filtrarPedidosPorPeriodo()
- gerarRelatorioOperacional()

---

## 7.3 Classe NotificacaoService

Responsável pelo gerenciamento das notificações do sistema.

### Principais Métodos
- enviarParaFuncionario()
- enviarParaHospede()
- registrarNotificacao()
