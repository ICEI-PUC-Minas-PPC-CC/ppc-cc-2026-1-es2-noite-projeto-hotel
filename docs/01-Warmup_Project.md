# 1. Funcionalidade escolhida

A funcionalidade escolhida foi a **solicitação de serviços pelo hóspede**, pois ela representa o núcleo do sistema Hospfy, conectando diretamente o usuário final (hóspede) com a operação interna do hotel.

---

# 2. Descrição do fluxo completo

O fluxo se inicia quando o hóspede acessa o aplicativo para solicitar algum serviço durante sua estadia.

Primeiro, o usuário entra no **Catálogo de Serviços**, onde visualiza as categorias disponíveis, como limpeza, manutenção ou serviço de quarto. Em seguida, ele seleciona uma categoria e escolhe um serviço específico (por exemplo, limpeza de quarto).

Ao selecionar o serviço, o sistema exibe os detalhes e permite que o hóspede adicione observações, como instruções específicas. Após isso, ele confirma a solicitação.

O sistema então cria um **pedido** com status inicial "Pendente" e o envia para o sistema interno do hotel. Esse pedido passa a ser exibido no painel da gestora, que é responsável por organizar as demandas.

A gestora visualiza o pedido, analisa as informações e atribui a tarefa a um funcionário disponível. A partir disso, o funcionário recebe uma notificação e pode iniciar o atendimento, alterando o status para "Em atendimento". Quando o serviço é finalizado, o status é atualizado para "Concluído".

Durante todo esse processo, o hóspede consegue acompanhar o status da solicitação em tempo real pelo aplicativo.

---

# 3. Mapeamento técnico

## Classes envolvidas

As principais classes identificadas no fluxo são:

- Hóspede  
- Pedido  
- Serviço  
- Categoria  
- Gestor  
- Funcionário  
- Notificação (como suporte ao fluxo)

---

## Papel de cada classe

**Hóspede:**  
Responsável por iniciar o fluxo, realizando a solicitação de serviços, adicionando observações e acompanhando o status do pedido.

**Pedido:**  
É a entidade central do sistema. Armazena todas as informações da solicitação, como serviço escolhido, hóspede, status e observações. Também concentra parte das regras relacionadas ao ciclo de vida do pedido.

**Serviço:**  
Representa o serviço que pode ser solicitado, contendo descrição, prazo estimado e disponibilidade.

**Categoria:**  
Organiza os serviços em grupos, facilitando a navegação no catálogo.

**Gestor:**  
Visualiza os pedidos no painel e realiza a distribuição das tarefas para os funcionários.

**Funcionário:**  
Executa o serviço solicitado e atualiza o status do pedido conforme o andamento.

**Notificação:**  
Responsável por comunicar eventos importantes, como atribuição de tarefas.

---

## Comunicação entre classes

O fluxo de comunicação ocorre da seguinte forma:

- O Hóspede cria um Pedido com base em um Serviço  
- O Pedido é visualizado pelo Gestor  
- O Gestor associa o Pedido a um Funcionário  
- O Funcionário interage com o Pedido, atualizando seu status  

---

# 4. Organização arquitetural

Para estruturar o sistema, foi adotado o padrão de **arquitetura em camadas**, separando responsabilidades entre Controller, Service e Repository.

## Controller

Camada responsável por receber as requisições do usuário.

Exemplos:
- PedidoController  
- ServicoController  

Sua função é atuar como ponto de entrada, recebendo dados e encaminhando para a camada de serviço.

---

## Service

Camada onde ficam as regras de negócio.

Exemplo:
- PedidoService  

Responsável por validar dados, aplicar regras (como restrições de cancelamento) e coordenar o fluxo entre controller e persistência.

---

## Repository

Responsável pela comunicação com o banco de dados.

Exemplos:
- PedidoRepository  
- ServicoRepository  

Realiza operações de persistência, como salvar, buscar e atualizar registros.

---

## Fluxo geral da arquitetura

Usuário → Controller → Service → Repository → Banco de Dados

---

## Exemplo aplicado

1. Usuário solicita um serviço  
2. PedidoController recebe a requisição  
3. PedidoService processa e valida  
4. PedidoRepository salva no banco  

---

# 5. Identificação de problemas

Durante a análise, foram identificados alguns pontos de melhoria:

**Acoplamento entre Pedido e Funcionário:**  
O Pedido depende diretamente do Funcionário, o que pode dificultar alterações futuras na lógica de atribuição.

**Classe Pedido sobrecarregada:**  
A classe concentra muitas responsabilidades (dados + regras de negócio), o que vai contra o princípio de responsabilidade única.

**Ausência de uma camada explícita de notificação:**  
Apesar de existir no fluxo, não está bem estruturada no modelo.

**Falta de controle temporal:**  
Informações como tempo de atendimento não estão completamente modeladas, o que impacta diretamente nos relatórios.

---

# 6. Definição e melhoria das classes

Com base nos problemas identificados, algumas melhorias podem ser propostas.

## Pedido

Adicionar atributos mais completos:

- id  
- status  
- observacoes  
- dataCriacao  
- dataInicio  
- dataFinalizacao  
- hóspede  
- serviço  

---

## PedidoService

Centralizar regras de negócio:

- criarPedido()  
- cancelarPedido()  
- atualizarStatus()  

---

## NotificacaoService

Responsável pelo envio de notificações:

- enviarParaFuncionario()  
- enviarParaHospede()  

---

## RelatorioService

Responsável pelo cálculo de métricas:

- calcularTempoMedio()  
- contarCancelamentos()  

---
