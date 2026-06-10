Sprint 4 — Organização, Integração e Planejamento do MVP

1. Definição do Escopo do MVP
O Produto Mínimo Viável (MVP) do Hospfy será focado no fluxo primário de geração de valor do sistema: a capacidade do hóspede de solicitar um serviço e a capacidade da equipe do hotel de receber e atualizar o status dessa solicitação.

O que ENTRA no escopo do MVP:

Catálogo de Serviços (RF01): Visualização das categorias e serviços disponíveis pelo hóspede.

Solicitação de Serviços (RF02 e RF03): Criação do pedido diretamente pelo aplicativo, com a possibilidade de adicionar observações.

Acompanhamento de Status (RF04): Visualização do andamento atual do pedido pelo hóspede.

Painel Administrativo Básico (RF06): Visualização das solicitações em andamento para a gestora e equipe do hotel.

Atualização de Status: Ação do funcionário de alterar o status do pedido (ex: pendente, em andamento, concluído) através das regras de negócio do PedidoService.

O que NÃO ENTRA no escopo do MVP:

Relatórios e Métricas (RF08): A geração de dados operacionais e de tempo médio (RelatorioService) será implementada em iterações futuras.

Notificações Push (RF09): O envio automatizado de notificações (NotificacaoService) não estará nesta versão inicial. A atualização dependerá da recarga da tela.

Aba de Informações do Hotel (RF10): A exibição de regras e horários estáticos (InformacaoHotel) será postergada.

Distribuição Automática de Tarefas (RF07): A atribuição formal e complexa de funcionários (AtribuicaoPedido) será simplificada. Os funcionários visualizarão uma fila geral de pedidos no painel.

2. Descrição do Fluxo Principal do Sistema
O caminho percorrido pela funcionalidade principal, desde a interface até a persistência no banco de dados, seguirá estritamente a Arquitetura em Camadas definida no projeto. O fluxo ocorre da seguinte forma:

Entrada de Dados (Frontend): O hóspede acessa o aplicativo e visualiza os serviços organizados por Categoria. Ao escolher um Servico, preenche as observações e confirma a solicitação, disparando uma requisição HTTP POST /pedidos com os dados em JSON.

Recepção e Validação (Controller): O PedidoController recebe a requisição, realiza as validações básicas de estrutura e aciona a camada inferior.

Processamento (Service): O PedidoService recebe a requisição e aplica as regras de negócio através do método criarPedido(). A classe central Pedido é instanciada e vinculada corretamente ao Hospede e ao Servico correspondentes.

Persistência (Repository): O PedidoService repassa o objeto finalizado para o PedidoRepository, que abstrai a infraestrutura e salva o registro no Banco de Dados com o status inicial.

Confirmação: A resposta de sucesso (HTTP) percorre o caminho inverso até o Frontend, confirmando a criação para o hóspede.

Atualização pela Equipe: O funcionário acessa o painel (via GET), visualiza a nova tarefa e, ao iniciá-la ou concluí-la, envia uma requisição PUT / PATCH. O PedidoService utiliza o método atualizarStatus() para refletir a mudança no banco de dados, permitindo que o hóspede acompanhe a evolução.

3. Planejamento Técnico da Implementação
A implementação técnica conectará as classes do modelo UML diretamente à Arquitetura em Camadas, isolando responsabilidades para garantir manutenibilidade.

3.1. Infraestrutura e Persistência (Banco de Dados e Repository)

Serão criadas as tabelas relacionais para persistir as entidades vitais do MVP: Hospede, Pedido, Servico, Categoria e Funcionario.

Os repositórios (PedidoRepository e ServicoRepository) atuarão como a única ponte de acesso ao banco, garantindo que o Service não lide com consultas SQL diretas.

3.2. Lógica de Negócio (Service)

A classe PedidoService será desenvolvida para centralizar a lógica. Ela será responsável por garantir que a multiplicidade do modelo seja respeitada, como confirmar que um Pedido pertence a um único Hospede e está associado a um único Servico ativo.

3.3. Controladores e API REST (Controller)

Serão implementados o PedidoController e o ServicoController.

Os endpoints essenciais serão disponibilizados: GET (para listar o catálogo no Frontend), POST (para criação de pedidos pelo hóspede) e PUT/PATCH (para a equipe atualizar status).

3.4. Interfaces de Usuário (Frontend)

Construção de duas interfaces visuais seguindo o requisito de usabilidade (RNF02): a visão do hóspede (focada em solicitação e acompanhamento) e a visão da equipe (focada em listagem e gestão de tarefas).

A interface não conterá regras de negócio, limitando-se a exibir dados e capturar ações para enviá-las ao Controller via JSON.
