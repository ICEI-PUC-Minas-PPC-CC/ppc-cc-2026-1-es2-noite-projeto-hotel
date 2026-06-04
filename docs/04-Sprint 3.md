

# Sprint 3 — Definição da Arquitetura do Sistema
---

## 1. Arquitetura Escolhida

O Hospfy adota a **Arquitetura em Camadas** (*Layered Architecture*), organizando o sistema em cinco camadas verticais com dependência unidirecional: cada camada só se comunica com a imediatamente abaixo, nunca pulando níveis.

---

## 2. Estrutura das Camadas


![Diagrama UML](https://raw.githubusercontent.com/ICEI-PUC-Minas-PPC-CC/ppc-cc-2026-1-es2-noite-projeto-hotel/main/docs/img/Diagrama_da_Estrutura.png)


---

## 3. Responsabilidades por Camada

### Frontend
Camada de apresentação. Responsável por todas as interfaces visuais do sistema, sem conter lógica de negócio. Exibe dados e captura ações do usuário.

- Interface do hóspede: catálogo de serviços, acompanhamento de pedidos, notificações
- Interface do funcionário: lista de tarefas atribuídas, atualização de status
- Interface do gestor: painel administrativo, relatórios, atribuição de tarefas, filtros

### Controller
Ponto de entrada das requisições HTTP vindas do Frontend.

- Receber requisições HTTP
- Executar validações básicas de formato e estrutura dos dados
- Acionar a camada de serviço correspondente
- Retornar a resposta adequada (sucesso ou erro) ao cliente

> O Controller **não** toma decisões de negócio. Apenas orquestra a entrada e saída da requisição.

### Service
Camada central da lógica de negócio. Define o comportamento do sistema.

- Criar e cancelar pedidos
- Atualizar status de pedidos
- Atribuir pedidos a funcionários
- Gerar relatórios operacionais
- Enviar notificações para hóspedes e funcionários
- Verificar disponibilidade de serviços

### Repository
Responsável exclusivamente pelo acesso e persistência dos dados. Abstrai as operações de banco de dados, isolando o Service dos detalhes de infraestrutura.

- Salvar novos registros
- Atualizar registros existentes
- Consultar dados por filtros e períodos
- Excluir registros

### Banco de Dados
Camada de infraestrutura onde as entidades do sistema são persistidas.

Entidades armazenadas: `Pedido`, `Hospede`, `Servico`, `Categoria`, `Funcionario`, `Gestor`, `Notificacao`, `Relatorio`, `AtribuicaoPedido`, `InformacaoHotel`

---

## 4. Comunicação entre os Componentes

A comunicação entre o Frontend e o backend segue o estilo **API REST** sobre HTTP, com dados trafegando em formato **JSON**.

### Fluxo de uma requisição

```
Frontend  →  Controller  →  Service  →  Repository  →  Banco de Dados
         ←              ←           ←              ←
```

### Verbos HTTP utilizados

| Verbo HTTP    | Uso no Hospfy                                        |
|---------------|------------------------------------------------------|
| `GET`         | Consultar catálogo, acompanhar pedido, listar relatórios, visualizar informações do hotel |
| `POST`        | Criar pedido, solicitar serviço, enviar notificação  |
| `PUT / PATCH` | Atualizar status do pedido, atribuir funcionário     |
| `DELETE`      | Cancelar pedido                                      |

### Exemplo de fluxo: Hóspede solicita um serviço

1. **Frontend** envia `POST /pedidos` com dados do serviço e observações
2. **Controller** recebe a requisição, valida os campos obrigatórios e aciona o `PedidoService`
3. **Service** aplica as regras de negócio: verifica disponibilidade do serviço, cria o pedido e aciona o envio de notificação
4. **Repository** persiste o novo pedido e a notificação no banco de dados
5. A resposta percorre o caminho inverso até o Frontend, que exibe a confirmação ao hóspede

---

## 5. Justificativa da Arquitetura

A escolha da Arquitetura em Camadas se justifica por quatro razões diretamente ligadas às características do Hospfy:

**Separação de responsabilidades**
Cada camada tem um papel bem definido, evitando que lógica de negócio apareça no Controller ou que consultas ao banco apareçam no Service — problemas comuns em sistemas que crescem sem estrutura.

**Manutenibilidade**
Alterações em uma camada não propagam impacto desnecessário nas demais. Trocar o banco de dados, por exemplo, exige mudança apenas no Repository, sem tocar no Service ou no Controller.

**Aderência aos requisitos não funcionais**
A escalabilidade (RNF04) e a segurança dos dados (RNF05) são facilitadas pela separação em camadas: é possível escalar componentes de forma independente e aplicar autenticação de maneira centralizada no Controller.

**Adequação ao porte do projeto**
O Hospfy possui complexidade média, com domínio bem delimitado e fluxo de dados previsível. A Arquitetura em Camadas entrega organização suficiente sem a sobrecarga operacional de abordagens mais complexas, como microsserviços.

---

## 6. Rastreabilidade com os Requisitos

| Requisito | Camada responsável |
|-----------|--------------------|
| RF01 – Visualizar catálogo de serviços | Frontend + Controller + Service |
| RF02 – Solicitar serviço | Frontend + Controller + Service + Repository |
| RF03 – Adicionar observações ao pedido | Frontend + Controller + Service |
| RF04 – Acompanhar status do pedido | Frontend + Controller + Service + Repository |
| RF05 – Cancelar pedido | Frontend + Controller + Service + Repository |
| RF06 – Visualizar painel administrativo | Frontend + Controller + Service |
| RF07 – Atribuir tarefas para funcionários | Controller + Service + Repository |
| RF08 – Gerar relatórios | Controller + Service + Repository |
| RF09 – Receber notificações | Service + Repository |
| RF10 – Consultar informações do hotel | Frontend + Controller + Repository |
| RNF01 – Atualização em tempo real | Service + Repository |
| RNF04 – Escalabilidade | Arquitetura em camadas (separação de responsabilidades) |
| RNF05 – Segurança dos dados | Controller (validação) + Repository (acesso isolado) |
