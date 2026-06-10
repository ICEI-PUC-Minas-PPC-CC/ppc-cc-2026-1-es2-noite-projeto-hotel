# Sprint 4 — Organização, Integração e Planejamento do MVP

## 1. Definição do Escopo do MVP

O Produto Mínimo Viável (MVP) do *Hospfy* será focado no fluxo primário de geração de valor do sistema: a capacidade do hóspede de solicitar um serviço e a capacidade da equipe do hotel de receber e atualizar o status dessa solicitação.

### ✅ O que ENTRA no escopo do MVP

#### Catálogo de Serviços (RF01)
Visualização das categorias e serviços disponíveis para o hóspede.

#### Solicitação de Serviços (RF02 e RF03)
Criação de pedidos diretamente pelo aplicativo, com possibilidade de adicionar observações.

#### Acompanhamento de Status (RF04)
Visualização do andamento atual do pedido pelo hóspede.

#### Painel Administrativo Básico (RF06)
Visualização das solicitações em andamento pela gestora e equipe do hotel.

#### Atualização de Status
Permite que funcionários alterem o status dos pedidos (ex.: Pendente, Em Andamento e Concluído) por meio das regras de negócio implementadas no PedidoService.

---

### ❌ O que NÃO ENTRA no escopo do MVP

#### Relatórios e Métricas (RF08)
A geração de indicadores operacionais e cálculo de tempo médio (RelatorioService) será implementada em versões futuras.

#### Notificações Push (RF09)
O envio automático de notificações (NotificacaoService) não estará disponível nesta versão inicial. As atualizações dependerão da recarga da tela.

#### Aba de Informações do Hotel (RF10)
A exibição de regras, horários e informações estáticas (InformacaoHotel) será implementada posteriormente.

#### Distribuição Automática de Tarefas (RF07)
A atribuição formal e automatizada de funcionários (AtribuicaoPedido) será simplificada. Os colaboradores visualizarão uma fila geral de pedidos no painel.

---

# 2. Descrição do Fluxo Principal do Sistema

O fluxo principal seguirá rigorosamente a Arquitetura em Camadas definida para o projeto.

## 2.1 Entrada de Dados (Frontend)

1. O hóspede acessa o aplicativo.
2. Visualiza os serviços organizados por categoria.
3. Seleciona um serviço.
4. Adiciona observações ao pedido.
5. Confirma a solicitação.

Após a confirmação, o sistema envia uma requisição:

http
POST /pedidos


contendo os dados em formato JSON.

---

## 2.2 Recepção e Validação (Controller)

O PedidoController recebe a requisição e:

- Valida a estrutura dos dados recebidos;
- Encaminha a solicitação para a camada de serviços.

---

## 2.3 Processamento (Service)

O PedidoService recebe a requisição e executa as regras de negócio através do método:

java
criarPedido()


Nesta etapa:

- Um objeto Pedido é criado;
- O pedido é associado ao Hospede;
- O pedido é associado ao Servico selecionado.

---

## 2.4 Persistência (Repository)

O PedidoService envia o objeto finalizado para o:

java
PedidoRepository


Responsabilidades:

- Abstrair o acesso ao banco de dados;
- Persistir o pedido;
- Definir o status inicial da solicitação.

---

## 2.5 Confirmação

Após a gravação bem-sucedida:

1. O banco retorna sucesso ao repositório.
2. O repositório retorna ao serviço.
3. O serviço retorna ao controlador.
4. O controlador responde ao Frontend.

O hóspede recebe a confirmação da criação do pedido.

---

## 2.6 Atualização pela Equipe

1. O funcionário acessa o painel administrativo.
2. Visualiza os pedidos pendentes.
3. Inicia ou conclui uma tarefa.
4. Envia uma requisição:

http
PUT /pedidos/{id}


ou

http
PATCH /pedidos/{id}


O PedidoService utiliza o método:

java
atualizarStatus()


para refletir a mudança no banco de dados.

Dessa forma, o hóspede consegue acompanhar a evolução da solicitação em tempo real.

---

# 3. Planejamento Técnico da Implementação

A implementação conectará diretamente as classes do modelo UML à Arquitetura em Camadas, mantendo responsabilidades bem definidas e facilitando a manutenção do sistema.

---

## 3.1 Infraestrutura e Persistência (Banco de Dados e Repository)

Serão criadas as tabelas relacionais para armazenar as entidades essenciais do MVP:

- Hospede
- Pedido
- Servico
- Categoria
- Funcionario

### Repositórios

Os repositórios serão a única camada responsável pelo acesso aos dados:

- PedidoRepository
- ServicoRepository

#### Responsabilidades

- Realizar consultas ao banco;
- Inserir registros;
- Atualizar informações;
- Isolar o restante da aplicação de comandos SQL.

---

## 3.2 Lógica de Negócio (Service)

A classe:

java
PedidoService


será responsável por centralizar toda a lógica de negócio.

### Principais responsabilidades

- Validar regras do sistema;
- Garantir integridade dos relacionamentos;
- Verificar que cada pedido pertence a um único hóspede;
- Garantir associação com apenas um serviço ativo;
- Controlar transições de status.

---

## 3.3 Controladores e API REST (Controller)

Serão implementados os seguintes controladores:

- PedidoController
- ServicoController

### Endpoints essenciais

#### Listagem de serviços

http
GET /servicos


#### Criação de pedidos

http
POST /pedidos


#### Atualização de status

http
PUT /pedidos/{id}


ou

http
PATCH /pedidos/{id}


Esses endpoints serão utilizados tanto pelo aplicativo do hóspede quanto pelo painel da equipe.

---

## 3.4 Interfaces de Usuário (Frontend)

Serão desenvolvidas duas interfaces principais, seguindo o requisito de usabilidade *RNF02*.

### Visão do Hóspede

Funcionalidades:

- Visualizar catálogo de serviços;
- Criar solicitações;
- Adicionar observações;
- Acompanhar status dos pedidos.

### Visão da Equipe

Funcionalidades:

- Visualizar fila de solicitações;
- Gerenciar pedidos;
- Atualizar status das tarefas.

### Responsabilidade do Frontend

A interface não conterá regras de negócio.

Seu papel será apenas:

- Exibir informações;
- Capturar ações dos usuários;
- Enviar e receber dados da API através de JSON.
