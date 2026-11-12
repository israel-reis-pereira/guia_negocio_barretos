# Prompt Mestre — Análise de 15 MVPs, Seleção Tecnológica, Custos e Validação Comercial

## 1. Papel e objetivo

Atue como:

- Product Manager Sênior;
- Arquiteto de Software;
- Analista de Negócios;
- Engenheiro de Software Full Stack;
- Consultor de viabilidade financeira para Micro-SaaS e MVPs destinados a pequenos negócios brasileiros.

Seu objetivo é elaborar uma análise funcional, técnica, financeira e comercial de **15 ideias de produtos digitais para pequenos negócios de Barretos-SP**, identificando quais realmente merecem ser desenvolvidas e qual oferece a melhor oportunidade de validação inicial.

### Estratégia de desenvolvimento

A estratégia consiste em:

1. Desenvolver aplicações úteis e confiáveis.
2. Demonstrá-las com dados fictícios quando apropriado.
3. Permitir que clientes reais avaliem sua utilidade durante aproximadamente 15 dias.
4. Identificar oportunidades comercialmente viáveis.
5. Reduzir riscos de desenvolvimento e evitar gastos sem justificativa comercial.

O objetivo não é construir o maior número possível de aplicações, mas encontrar oportunidades viáveis e comprovar sua utilidade antes de ampliar o investimento.

### Princípios obrigatórios

- Qualidade acima de quantidade.
- Escolha tecnológica orientada pelas necessidades do produto.
- Custo total de desenvolvimento e operação próximo de zero durante a validação, sempre que realisticamente possível.
- Transparência sobre todos os custos que possam surgir depois do teste.
- Funcionalidades essenciais antes de recursos sofisticados.
- Aplicações funcionais, seguras, testáveis e adequadas ao uso real.
- Ausência de integrações fictícias ou promessas sobre recursos não implementados.
- Arquitetura simples, sustentável e adequada a um desenvolvedor independente.
- Separação entre protótipo visual, demonstração com dados fictícios e MVP operacional.
- Validação da necessidade comercial antes de ampliar o escopo.
- Não recomendar o desenvolvimento simultâneo dos 15 projetos.

Considere que o desenvolvedor trabalha sozinho e deseja reduzir retrabalho, custos, complexidade de suporte e dependência de serviços externos.

---

## 2. Princípio central: a stack deve ser escolhida para cada MVP

Não existe uma stack obrigatória.

Não priorize tecnologias por preferência pessoal, incluindo:

- Astro;
- PHP;
- MySQL;
- React;
- Node.js;
- Python;
- Supabase;
- Firebase;
- Cloudflare;
- Outras tecnologias ou serviços.

Avalie as alternativas adequadas para cada projeto e recomende a combinação que ofereça o melhor equilíbrio entre:

- Custo total.
- Qualidade.
- Segurança.
- Facilidade de desenvolvimento.
- Facilidade de manutenção.
- Velocidade de implantação.
- Confiabilidade.
- Compatibilidade com as funcionalidades necessárias.
- Disponibilidade de serviços gratuitos.
- Limites dos planos gratuitos.
- Facilidade de migração.
- Risco de dependência de fornecedores.
- Previsibilidade dos custos futuros.

### 2.1. Avaliação da complexidade necessária

Antes de recomendar uma arquitetura, considere alternativas mais simples:

- Site estático.
- Aplicação frontend simples.
- Ferramenta sem banco de dados.
- Planilha estruturada.
- Backend mínimo.

Quando houver necessidade de persistência, autenticação, dados privados, processamento em segundo plano, envio de mensagens ou armazenamento de arquivos, avalie a arquitetura necessária para atender esses requisitos com segurança.

### 2.2. Comparação tecnológica dos finalistas

Para cada projeto finalista, compare pelo menos duas alternativas tecnológicas viáveis quando isso puder alterar significativamente o custo, a complexidade ou a qualidade.

Apresente:

1. Stack recomendada.
2. Alternativa viável.
3. Justificativa técnica da escolha.
4. Custo de cada alternativa.
5. Complexidade de implantação e manutenção.
6. Limitações e riscos.
7. Possibilidade de migração futura.

Não escolha a alternativa mais barata isoladamente se ela comprometer a confiabilidade ou exigir manutenção excessiva.

Não escolha uma arquitetura robusta demais para um produto que ainda precisa provar que alguém pagaria por ele.

Verifique a compatibilidade real entre frontend, backend, banco de dados, armazenamento e hospedagem.

---

## 3. Política de custos e orçamento

Cada projeto deverá ter um orçamento separado para quatro etapas.

### 3.1. Custo de desenvolvimento

Estimar:

- Horas de análise.
- Horas de implementação.
- Horas de testes.
- Horas de publicação.
- Ferramentas pagas, se necessárias.
- Serviços externos necessários durante o desenvolvimento.

Separar esforço de trabalho e desembolso financeiro.

Não considerar o trabalho do desenvolvedor como gratuito apenas porque não há pagamento de uma ferramenta.

### 3.2. Custo do teste de 15 dias

Planejar a menor infraestrutura capaz de sustentar o fluxo principal do MVP durante aproximadamente 15 dias.

Discriminar:

- Hospedagem.
- Banco de dados.
- Armazenamento.
- Domínio.
- Certificado HTTPS, quando aplicável.
- APIs externas.
- Mensagens.
- Processamento em segundo plano.
- Backups.
- Monitoramento.
- Limites de utilização.
- Risco de cobranças excedentes.

Sempre que possível, utilizar serviços gratuitos com condições adequadas ou desenvolver uma alternativa que elimine a dependência de integrações pagas.

Não assumir que uma ferramenta é gratuita por oferecer uma conta de entrada, créditos temporários ou período promocional.

Não assumir que todo o período de teste terá custo zero. Se houver qualquer custo inevitável, informar o valor ou a necessidade de cotação.

### 3.3. Custo mensal após a validação

Apresentar três cenários por projeto:

| Cenário | Descrição |
|---|---|
| Econômico | Operação de pequeno porte, com utilização baixa. |
| Esperado | Operação compatível com um cliente real usando o produto regularmente. |
| Crescimento | Aumento de usuários, dados, arquivos ou integrações. |

Para cada cenário, informar:

- Custo fixo mensal.
- Custo variável.
- Custo por utilização, quando aplicável.
- Limites incluídos.
- Custos que podem surgir por excedentes.
- Manutenção técnica.
- Suporte.
- Melhorias evolutivas, quando contratadas.

Separar o custo da infraestrutura do preço do serviço prestado pelo desenvolvedor.

Não apresentar um valor mensal sem explicar o que está incluído e quais hipóteses foram utilizadas.

### 3.4. Transparência financeira para o cliente

Para cada projeto recomendado, elaborar um resumo financeiro que possa ser apresentado ao cliente antes do início do teste.

O resumo deverá informar:

- Funcionalidades incluídas.
- Duração do teste.
- Limites de utilização.
- Custos cobertos durante a validação.
- Possíveis despesas externas.
- Custo mensal estimado após o teste.
- Custos de manutenção e suporte.
- Custos de integrações opcionais.
- Situações que podem aumentar o orçamento.

A proposta deve ajudar a verificar desde o início se o cliente terá condições de manter a aplicação.

Não prometer gratuidade permanente.

Diferenciar claramente:

- Teste subsidiado pelo desenvolvedor.
- Operação gratuita em produção.
- Operação paga após a validação.

---

## 4. Pesquisa e confiabilidade das informações

Quando houver acesso à internet, pesquisar informações atuais sobre:

- Preços.
- Limites dos planos.
- Políticas de APIs.
- Condições de hospedagem.
- Documentação técnica.
- Termos de uso.
- Mercado local.

### 4.1. Fontes prioritárias

Priorizar:

1. Documentação oficial.
2. Páginas oficiais de preços.
3. Documentação técnica dos provedores.
4. Termos de uso relevantes.
5. Fontes confiáveis sobre o mercado local.

Registrar a data da consulta quando apresentar preços ou limites que possam mudar.

### 4.2. Informações que não podem ser inventadas

Não inventar:

- Preços.
- Limites gratuitos.
- Disponibilidade de integrações.
- Dados de demanda local.
- Número de clientes potenciais.
- Receita esperada.
- Probabilidade de sucesso comercial.

Se uma informação não puder ser confirmada, identificá-la como:

- Hipótese.
- Estimativa.
- Pendência de validação.

Distinguir fatos verificados de suposições comerciais.

---

## 5. Os 15 projetos a serem analisados

Analise individualmente os projetos abaixo, preservando suas características, segmentos e restrições.

### Projeto 1 — Sem Vergonha de Cobrar

**Segmento:** beleza, manicure, cílios, barbearias e profissionais autônomos.

**Problema:** dificuldade para acompanhar dívidas de clientes e realizar cobranças recorrentes.

**Ideia:** painel para cadastrar clientes, registrar valores devidos, controlar pagamentos e preparar lembretes amigáveis com instruções de pagamento via Pix.

### Projeto 2 — Confirmador de Agendamentos Anti-Falta

**Segmento:** salões, barbearias, clínicas e prestadores de serviços.

**Problema:** clientes que não comparecem aos horários agendados.

**Ideia:** cadastro ou importação de agendamentos, acompanhamento de confirmações, visualização de horários pendentes e preparação de lembretes.

### Projeto 3 — Capturador de Avaliações

**Segmento:** clínicas, consultórios, odontologia e serviços veterinários.

**Problema:** dificuldade para solicitar feedback e avaliações após o atendimento.

**Ideia:** registro de solicitações, acompanhamento de respostas e encaminhamento neutro para canais apropriados de avaliação pública.

**Restrições:**

- Não criar avaliações falsas.
- Não condicionar recompensas a avaliações positivas.
- Não direcionar seletivamente avaliações públicas com base na nota atribuída pelo cliente.

### Projeto 4 — Gerador de Recibos de Consulta

**Segmento:** médicos, fisioterapeutas e consultórios.

**Problema:** demora na emissão de recibos e documentos administrativos.

**Ideia:** preenchimento dos dados necessários, geração de PDF, histórico e download ou compartilhamento do documento.

**Restrição:** considerar privacidade, controle de acesso e proteção dos dados pessoais.

### Projeto 5 — Catálogo Digital com Sacola no WhatsApp

**Segmento:** lojas de roupas, moda country, acessórios e comércio varejista.

**Problema:** necessidade de vender e apresentar produtos online sem manter uma plataforma complexa de comércio eletrônico.

**Ideia:** catálogo com fotos, preços, variantes, montagem de sacola e encaminhamento do pedido para o WhatsApp da loja.

### Projeto 6 — Notificador de Novidades para Clientes VIP

**Segmento:** lojas de roupas e varejistas com clientes recorrentes.

**Problema:** trabalho manual para comunicar lançamentos e novidades.

**Ideia:** cadastro de clientes com consentimento ou outra base legal aplicável, organização de preferências e preparação de campanhas segmentadas.

**Restrições:**

- A automação por WhatsApp deve ser tratada como dependência específica.
- Analisar custos, políticas, credenciais e limitações.
- Prever alternativas de envio manual, links de compartilhamento ou e-mail.

### Projeto 7 — Rastreador de Ordem de Serviço

**Segmento:** oficinas, revendas de peças e prestadores de serviços para o agronegócio.

**Problema:** clientes precisam entrar em contato repetidamente para acompanhar serviços.

**Ideia:** cadastro de ordens de serviço, atualização de status e consulta pelo cliente mediante um código seguro de acompanhamento.

**Restrição:** não expor CPF, telefone ou outros dados pessoais em consultas públicas.

### Projeto 8 — Quadro de Avisos e Cotações

**Segmento:** produtores rurais, escritórios agrícolas, cooperativas e revendas de insumos.

**Problema:** dificuldade de centralizar informações e distribuir cotações aos parceiros.

**Ideia:** painel de publicações, registro da fonte e da data das cotações, histórico e preparação de comunicados.

**Restrições:**

- Não inventar cotações.
- Não presumir acesso gratuito a fontes de mercado.

### Projeto 9 — Organizador de Pedidos para Cozinha

**Segmento:** marmitarias, restaurantes, lanchonetes e delivery.

**Problema:** dificuldade para organizar pedidos recebidos por mensagens e encaminhá-los para cozinha e entrega.

**Ideia:** painel de pedidos, itens, observações, endereço quando necessário, status e impressão.

**Restrições:**

- A integração automática com WhatsApp deverá ser analisada separadamente.
- O MVP poderá começar com cadastro manual ou importação.

### Projeto 10 — Caderneta Digital de Fiado

**Segmento:** padarias, mercadinhos e pequenos comércios.

**Problema:** erros, perda de registros e dificuldade para acompanhar dívidas recorrentes.

**Ideia:** cadastro de clientes, registro de compras a prazo, pagamentos parciais, cálculo de saldo e demonstrativos de movimentação.

**Restrições:**

- Considerar permissões.
- Manter histórico de alterações.
- Proteger a privacidade.
- Prevenir exclusões acidentais.

### Projeto 11 — Calculadora de Tintas e Orçamento Rápido de Parede

**Segmento:** pintores residenciais e comerciais.

**Problema:** demora para medir superfícies, estimar materiais, calcular mão de obra e apresentar orçamentos.

**Ideia:** aplicação mobile-first para registrar dimensões, calcular áreas, estimar consumo de tinta, considerar demãos, estimar quantidades comerciais de embalagens e calcular mão de obra conforme os valores configurados pelo profissional.

**Funcionalidades a avaliar:**

- Cadastro de preços de mão de obra.
- Cálculo de áreas de paredes e outras superfícies.
- Desconto de portas e janelas.
- Configuração de demãos e rendimento.
- Margem de perda.
- Cadastro de preços de materiais.
- Separação entre materiais e mão de obra.
- Observações e validade do orçamento.
- Geração de PDF ou documento para impressão.
- Compartilhamento pelo WhatsApp.
- Histórico de orçamentos.

**Restrições:**

- Não apresentar estimativas de consumo como quantidades exatas.
- Considerar o rendimento informado pelo usuário ou fabricante.
- Considerar o estado da superfície, a preparação e o método de aplicação.
- Avaliar se a primeira versão pode funcionar sem conta de usuário, backend ou integração externa.

### Projeto 12 — Catálogo Digital de Cores, Texturas e Portfólio de Obras

**Segmento:** pintores profissionais.

**Problema:** dificuldade para localizar fotografias de trabalhos anteriores e demonstrar técnicas a potenciais clientes.

**Ideia:** portfólio digital com fotografias organizadas por categoria, descrição dos serviços e contato.

**Funcionalidades a avaliar:**

- Página pública.
- Galeria de fotos.
- Categorias de técnicas e acabamentos.
- Descrições dos trabalhos.
- Link compartilhável.
- Contato pelo WhatsApp.
- Painel de administração, se necessário.
- Otimização de imagens.
- Limites de armazenamento.

**Restrições:**

- Avaliar se o portfólio pode ser mantido com conteúdo estático ou se precisa de um sistema de gerenciamento.
- Considerar autorização para publicação de imagens de imóveis e ambientes de clientes.

### Projeto 13 — Diário de Obra e Acompanhamento do Cliente

**Segmento:** pintores residenciais e comerciais.

**Problema:** clientes querem acompanhar o progresso da obra sem precisar perguntar repetidamente ao profissional.

**Ideia:** painel para registrar etapas, atualizações diárias e fotografias, disponibilizando acompanhamento ao cliente por um mecanismo de acesso seguro.

**Funcionalidades a avaliar:**

- Cadastro de obras.
- Identificação do cliente.
- Etapas do serviço.
- Atualização de status.
- Registro de data e descrição.
- Fotografias opcionais.
- Linha do tempo.
- Página de acompanhamento.
- Registro de conclusão.
- Controle de acesso e encerramento.

**Restrições:**

- Não depender apenas de identificadores previsíveis ou dados pessoais para proteger o acesso.
- Considerar armazenamento, privacidade e exclusão de imagens.

### Projeto 14 — Controle de Recebimentos e Parcelamento de Obras

**Segmento:** pintores profissionais.

**Problema:** dificuldade para acompanhar entradas, parcelas, pagamentos pendentes e saldos de obras.

**Ideia:** painel financeiro simples para registrar contratos, parcelas, vencimentos, recebimentos e valores pendentes.

**Funcionalidades a avaliar:**

- Cadastro de obras e clientes.
- Valor contratado.
- Entrada e parcelas.
- Registro manual de pagamentos.
- Saldo devedor.
- Parcelas vencidas e futuras.
- Histórico de recebimentos.
- Resumo financeiro por obra.
- Demonstrativo para o cliente.
- Preparação de lembretes.
- Integração opcional com provedor de pagamentos.

**Comparar duas alternativas:**

1. Controle financeiro com registros manuais.
2. Controle financeiro integrado a um provedor de pagamentos.

**Restrições:**

- Verificar tarifas, condições, credenciais e custos vigentes antes de recomendar uma integração.
- Não afirmar que pagamentos foram confirmados automaticamente sem integração efetivamente implementada.

### Projeto 15 — Central de Parcerias entre Pintores e Lojas de Tintas

**Segmento:** pintores profissionais e lojas de tintas.

**Problema:** dificuldade para comprovar indicações, registrar compras originadas de recomendações e acompanhar possíveis benefícios comerciais.

**Ideia:** ferramenta para criar listas de materiais identificadas com o pintor responsável e permitir que a loja registre indicações e compras confirmadas.

**Funcionalidades a avaliar:**

- Cadastro de pintores.
- Cadastro de lojas.
- Listas de materiais.
- Quantidades e observações.
- Código identificador ou QR Code.
- Link para consulta da lista.
- Registro de indicação.
- Registro de atendimento.
- Confirmação manual de compra.
- Histórico de operações.
- Relatórios de benefícios ou comissões.
- Controle de acesso dos parceiros.

**Restrições:**

- Não presumir que lojas participarão ou pagarão comissões.
- Diferenciar lista criada, indicação, atendimento, compra confirmada e benefício validado conforme acordo entre as partes.
- Considerar uma validação manual com poucas lojas antes de construir uma plataforma completa.

---

## 6. Estrutura obrigatória para analisar cada projeto

Analise os 15 projetos individualmente, mantendo uma seção independente para cada um.

### 6.1. Visão geral do produto

Informar:

- Nome.
- Segmento.
- Perfil do cliente ideal.
- Problema principal.
- Proposta de valor.
- Benefício demonstrável em 15 dias.
- Hipóteses comerciais.
- Principais riscos de adoção.

### 6.2. Escopo funcional do MVP

Para cada funcionalidade, informar:

| Campo | Descrição |
|---|---|
| Identificador | Código da funcionalidade, como F01. |
| Nome | Nome da funcionalidade. |
| Descrição | O que a funcionalidade realiza. |
| Usuário responsável | Quem executa a ação. |
| Dados de entrada | Informações necessárias. |
| Processamento | Regras e operações executadas. |
| Resultado esperado | Resultado apresentado ao usuário. |
| Critério de aceitação | Condição objetiva para considerar a funcionalidade concluída. |
| Prioridade | Classificação P0, P1 ou P2. |

**Classificação de prioridades:**

- **P0:** indispensável para o fluxo principal.
- **P1:** importante, mas pode ser adiada.
- **P2:** melhoria futura, fora do MVP.

Evitar funcionalidades que não contribuam para resolver a dor principal.

### 6.3. Fluxos de usuário

Descrever:

1. Primeiro acesso.
2. Configuração inicial.
3. Fluxo principal completo.
4. Fluxo alternativo.
5. Tratamento de erros.
6. Conclusão da tarefa.

### 6.4. Telas e navegação

Para cada tela, definir:

- Objetivo.
- Componentes.
- Campos e botões.
- Ações disponíveis.
- Validações.
- Estados vazios.
- Carregamento e erros.
- Comportamento em celular e computador.

Não criar telas sem função prática.

### 6.5. Modelo de dados

Quando houver persistência, especificar:

- Entidades ou tabelas.
- Campos e tipos.
- Chaves primárias e estrangeiras.
- Campos obrigatórios.
- Restrições e índices.
- Relações.
- Regras de integridade.
- Exemplos de registros fictícios.

Não introduzir um banco de dados se a solução não precisar dele.

### 6.6. Regras de negócio

Documentar:

- Cálculos.
- Estados.
- Validações.
- Duplicidades.
- Limites.
- Permissões.
- Tratamento de operações inválidas.
- Histórico de alterações, quando necessário.

### 6.7. Arquitetura e implementação

Definir:

- Stack recomendada.
- Alternativa tecnológica.
- Frontend.
- Backend, se necessário.
- Banco de dados, se necessário.
- Armazenamento.
- Autenticação.
- Autorização.
- APIs e endpoints.
- Métodos HTTP, quando aplicáveis.
- Estrutura de respostas.
- Validação.
- Tratamento de erros.
- Hospedagem.
- Processo de publicação.

Fornecer exemplos dos endpoints essenciais quando houver API.

Justificar por que a stack escolhida é adequada ao produto e por que alternativas mais complexas ou caras foram descartadas.

### 6.8. Integrações externas

Para cada integração, informar:

- Objetivo.
- Necessidade no MVP.
- Credenciais necessárias.
- Custos.
- Limites.
- Riscos.
- Dependências.
- Alternativa manual ou sem integração.
- Critério de validação.

Diferenciar claramente:

- Integração real.
- Fluxo manual.
- Demonstração simulada.

### 6.9. Segurança e LGPD

Identificar:

- Dados pessoais.
- Riscos de exposição.
- Controle de acesso.
- Proteção de credenciais.
- Validação no servidor, quando aplicável.
- Separação de dados entre empresas.
- Backup.
- Retenção e exclusão.
- Registro de ações relevantes.
- Base legal ou consentimento, quando aplicável.

Utilizar dados sintéticos nas demonstrações e evitar a coleta de dados sensíveis desnecessários.

### 6.10. Critérios de aceite e testes

Incluir:

- Cenários positivos.
- Cenários negativos.
- Campos inválidos.
- Duplicidades.
- Erros de integração.
- Persistência.
- Uso em celulares.
- Autorização.
- Fluxo principal de ponta a ponta.

Os critérios devem permitir verificar objetivamente se o MVP está pronto.

### 6.11. Plano de desenvolvimento

Dividir em:

1. Preparação.
2. Estrutura da aplicação.
3. Implementação do fluxo principal.
4. Banco de dados e backend, se necessários.
5. Integrações.
6. Testes.
7. Publicação.
8. Demonstração comercial.

Para cada etapa, apresentar:

- Entregáveis.
- Dependências.
- Horas estimadas.
- Riscos.
- Condição de conclusão.

### 6.12. Validação comercial

Definir:

- Demonstração com dados fictícios.
- Problema apresentado.
- Fluxo demonstrado.
- Perguntas ao cliente.
- Métricas para os 15 dias.
- Critérios para continuar.
- Critérios para encerrar ou reformular.
- Evidências de disposição para pagar.

Não prometer resultados financeiros sem evidências.

### 6.13. Custos e operação

Apresentar uma tabela com:

| Campo | Informação necessária |
|---|---|
| Componente | Parte da solução ou serviço utilizado. |
| Serviço recomendado | Tecnologia ou provedor escolhido. |
| Alternativa | Outra opção viável. |
| Custo inicial | Desembolso inicial. |
| Custo no período de 15 dias | Desembolso durante a validação. |
| Custo mensal após validação | Estimativa de operação mensal. |
| Cenário econômico | Operação de baixa utilização. |
| Cenário esperado | Operação regular. |
| Cenário de crescimento | Aumento de utilização. |
| Limites do plano | Restrições de uso. |
| Custos variáveis | Despesas dependentes de utilização. |
| Manutenção | Esforço e custo técnico. |
| Situação da informação | Confirmada, estimada ou pendente. |

Separar:

- Infraestrutura.
- Domínio.
- APIs.
- Mensagens.
- Armazenamento.
- Desenvolvimento.
- Manutenção.
- Suporte.

### 6.14. Fora do escopo

Listar explicitamente o que ficará de fora da primeira versão.

Considerar, quando aplicável:

- Aplicativo nativo.
- Multiunidades.
- Integrações complexas.
- Automações pagas.
- Inteligência artificial não essencial.
- Relatórios avançados.
- Pagamentos online.
- Gestão empresarial completa.
- Funcionalidades sem relação direta com a dor principal.

### 6.15. Definição de pronto

Exigir:

- Fluxo principal funcional.
- Persistência, quando necessária.
- Validações.
- Testes críticos aprovados.
- Interface utilizável em dispositivos móveis.
- Credenciais protegidas.
- Tratamento dos erros essenciais.
- Publicação acessível.
- Demonstração executável.
- Instruções básicas de uso.

---

## 7. Comparação entre os 15 projetos

Produza uma matriz comparativa que inclua todos os projetos, do 1 ao 15.

### 7.1. Colunas obrigatórias

| Critério | Descrição |
|---|---|
| Número e nome | Identificação do projeto. |
| Segmento | Mercado atendido. |
| Dor principal | Problema que pretende resolver. |
| Público-alvo | Perfil do cliente. |
| Funcionalidade central | Principal solução oferecida. |
| Quantidade de funcionalidades P0 | Número de funcionalidades indispensáveis. |
| Complexidade técnica | Nota de 1 a 5. |
| Estimativa de desenvolvimento | Horas necessárias. |
| Custo estimado de desenvolvimento | Desembolso financeiro e esforço. |
| Custo estimado do teste de 15 dias | Infraestrutura e serviços. |
| Custo mensal após validação | Estimativa operacional. |
| Dependência de integrações | Nível de dependência de terceiros. |
| Viabilidade de operação gratuita | Possibilidade de operação sem custos. |
| Risco técnico | Probabilidade e impacto de problemas técnicos. |
| Risco de manutenção | Complexidade de suporte e evolução. |
| Facilidade de conseguir os primeiros usuários | Acesso ao público-alvo. |
| Facilidade de demonstrar valor | Clareza do benefício durante a apresentação. |
| Potencial de receita recorrente | Possibilidade de cobrança contínua. |
| Recomendação de prioridade | Posição na ordem de desenvolvimento. |

Justificar as notas e apresentar as hipóteses utilizadas.

Não tratar estimativas de receita ou demanda como fatos comprovados.

---

## 8. Análise especial dos cinco projetos de pintura

Investigue se os projetos 11 a 15 podem compartilhar funcionalidades, dados ou infraestrutura.

### 8.1. Projetos envolvidos

- Projeto 11 — Calculadora de Tintas e Orçamento Rápido de Parede.
- Projeto 12 — Catálogo Digital de Cores, Texturas e Portfólio de Obras.
- Projeto 13 — Diário de Obra e Acompanhamento do Cliente.
- Projeto 14 — Controle de Recebimentos e Parcelamento de Obras.
- Projeto 15 — Central de Parcerias entre Pintores e Lojas de Tintas.

### 8.2. Possibilidades de integração a investigar

Avaliar:

- Se a calculadora de orçamento pode alimentar o diário de obra.
- Se o orçamento pode gerar uma lista de materiais.
- Se o controle financeiro pode utilizar os dados do orçamento.
- Se o portfólio pode funcionar como canal de aquisição.
- Se uma base comum de clientes e obras traria benefícios reais.

### 8.3. Estratégias a comparar

Comparar três estratégias:

1. Desenvolver apenas um produto independente.
2. Desenvolver um produto principal com módulos opcionais.
3. Desenvolver produtos independentes e integrá-los apenas quando houver demanda.

Para cada alternativa, apresentar:

- Custo.
- Complexidade.
- Manutenção.
- Benefícios.
- Riscos.

Não recomendar integração apenas porque os produtos atendem ao mesmo segmento.

---

## 9. Priorização e decisão final

Classifique os 15 projetos conforme os seguintes critérios:

- Velocidade de desenvolvimento.
- Facilidade de demonstrar valor.
- Custo de operação.
- Independência de integrações externas.
- Segurança.
- Simplicidade de suporte.
- Acesso aos primeiros clientes.
- Potencial de receita recorrente.
- Facilidade de validação em 15 dias.
- Capacidade de o cliente manter o produto financeiramente.

### 9.1. Decisões obrigatórias

Selecione e justifique:

1. Melhor projeto geral para começar.
2. Segundo melhor projeto.
3. Melhor projeto para validar com meu pai e profissionais de pintura.
4. Projeto mais fácil de demonstrar sem integrações externas.
5. Projeto com maior risco técnico.
6. Projeto mais dependente de terceiros.
7. Projeto com melhor equilíbrio entre simplicidade e potencial comercial.
8. Projeto com maior risco de custo operacional.
9. Projeto que não deveria ser desenvolvido antes de validar a demanda.
10. Melhor oportunidade para um produto modular, se houver evidências que justifiquem essa escolha.

Apresente critérios e notas que expliquem as decisões.

Não force uma recomendação positiva para todos os projetos.

Se algum deles tiver baixa viabilidade, recomende:

- Adiar.
- Reformular.
- Descartar.

---

## 10. Plano de execução

Depois da análise, proponha um plano realista para desenvolver um MVP por vez.

O plano deve incluir:

- Projeto selecionado.
- Justificativa.
- Escopo P0.
- Stack recomendada.
- Estimativa de horas.
- Orçamento de desenvolvimento.
- Orçamento do teste de 15 dias.
- Custos mensais após validação.
- Riscos.
- Critérios de aceite.
- Plano de demonstração.
- Métricas de validação.
- Condições para continuar ou interromper.

**Não gere o código-fonte nesta etapa.**

---

## 11. Formato obrigatório da resposta

A análise deverá seguir estas orientações:

- Escrever em português brasileiro.
- Analisar todos os 15 projetos.
- Não misturar os requisitos de projetos diferentes.
- Utilizar tabelas comparativas e listas para organizar informações.
- Ser específico e técnico sem introduzir complexidade desnecessária.
- Diferenciar fatos, estimativas e hipóteses.
- Consultar fontes oficiais para preços e limites atuais quando houver acesso à internet.
- Não inventar funcionalidades, custos, integrações ou dados de mercado.
- Quando faltar informação, explicitar a hipótese adotada e continuar.
- Não fazer perguntas antes de entregar a primeira versão da análise.
- Não gerar o código-fonte completo.
- Não recomendar construir todos os projetos simultaneamente.

---

## 12. Resultado esperado

Entregar um documento que permita decidir:

1. Quais projetos merecem ser desenvolvidos.
2. Qual stack utilizar em cada caso.
3. Quanto custará construir cada solução.
4. Quanto custará operar cada solução.
5. Quais despesas deverão ser apresentadas ao cliente antes do início do teste.
6. Qual projeto oferece a melhor oportunidade de validação inicial.
7. Qual deve ser a sequência realista de desenvolvimento.

O resultado deve servir de base para:

- Backlog.
- Arquitetura.
- Planejamento.
- Testes.
- Publicação.
- Demonstração.
- Validação comercial.

---

## 13. Regra final

**Escolher a tecnologia depois de entender o problema, construir a menor solução confiável que gere valor real, manter os custos transparentes e ampliar o produto somente quando houver evidências que justifiquem o investimento.**