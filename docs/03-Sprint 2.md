
## Diagrama UML


![Diagrama UML](https://raw.githubusercontent.com/ICEI-PUC-Minas-PPC-CC/ppc-cc-2026-1-es2-noite-projeto-hotel/main/docs/img/Diagrama.jpg)

---

# Descrição do Diagrama

O diagrama de classes do sistema **Hospfy** representa a estrutura principal do aplicativo de gerenciamento de solicitações de hotéis. A classe **Pedido** foi definida como a classe central do sistema, pois concentra o registro das solicitações realizadas pelos hóspedes, o controle de status, as datas de acompanhamento e as observações relacionadas ao atendimento.

Ao redor dela, estão as classes responsáveis por complementar o fluxo do sistema. A classe **Hospede** representa o usuário que realiza solicitações e acompanha pedidos. A classe **Servico** define os serviços disponíveis no hotel, organizados por meio da classe **Categoria**. Já a classe **Funcionario** se relaciona com os pedidos por meio da classe intermediária **AtribuicaoPedido**, permitindo registrar qual funcionário foi responsável por determinada tarefa.

A classe **Gestor** representa o usuário administrativo, responsável por acompanhar os pedidos, atribuir tarefas e visualizar relatórios. A classe **Notificacao** registra as mensagens enviadas ao hóspede ou funcionário, principalmente em alterações de status. A classe **Relatorio** utiliza os pedidos para gerar métricas operacionais, como tempo médio de atendimento e quantidade de cancelamentos. Por fim, a classe **InformacaoHotel** armazena orientações, regras e horários que podem ser consultados pelos hóspedes.

Esse modelo organiza as principais entidades do Hospfy, seus atributos e relacionamentos, permitindo uma visão clara da estrutura do sistema e servindo como base para documentação, implementação e evolução do projeto.

---

# Principais Relacionamentos

* Um **Hospede** pode possuir vários **Pedidos**
* Um **Pedido** pertence a um único **Hospede**
* Um **Pedido** está associado a um **Servico**
* Um **Servico** pertence a uma **Categoria**
* Um **Gestor** pode gerenciar vários **Pedidos**
* Um **Pedido** pode possuir várias **AtribuicoesPedido**
* Um **Funcionario** pode possuir várias **AtribuicoesPedido**
* Um **Pedido** pode gerar várias **Notificacoes**
* **Hospedes** e **Funcionarios** podem receber notificações
* Um **Relatorio** utiliza vários **Pedidos**
* **Hospedes** podem consultar várias **InformacoesHotel**

