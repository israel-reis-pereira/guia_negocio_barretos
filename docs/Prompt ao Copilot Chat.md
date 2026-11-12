Pela sua especificação, você já fez uma parte importante do trabalho: definiu a visão do produto, a arquitetura recomendada, os requisitos, os riscos, o modelo de dados e os critérios de publicação.

O que falta agora é transformar essa especificação em um plano executável, com decisões suas, tarefas para o Copilot, critérios de aceite e pontos de aprovação antes de publicar.

Minha recomendação é usar o GitHub Copilot como parceiro de planejamento e implementação, mas não pedir que ele desenvolva tudo de uma vez. É melhor trabalhar por fases, com entregas verificáveis e autorização explícita para operações que afetem o repositório, as contas ou o domínio.

## 1. Quais fatores dependem de você?

Separei os fatores em três grupos: decisões de negócio, responsabilidades operacionais e trabalho que você pode delegar ao Copilot.

### 1. Decisões que só você pode tomar

Sua responsabilidade- Objetivo profissional: o que você quer demonstrar no portfólio e quais competências deseja destacar.
- Identidade visual: cores, estilo, tom dos textos, foto, apresentação e links profissionais.
- Conteúdo público: biografia, tecnologias que realmente conhece, projetos e informações de contato.
- Escopo do MVP: confirmar que o mapa geográfico é opcional e que prospecção privada, login e banco de dados ficam para o futuro.
- Dados empresariais: decidir quais registros reais podem ser publicados, quais fontes são confiáveis e quais precisam de revisão.

### 2. Acessos e operações que dependem de você

Aprovação necessária- Criar ou confirmar o repositório no GitHub.
- Autorizar o Copilot a acessar o repositório e editar os arquivos, conforme as permissões disponíveis.
- Conectar o GitHub à Cloudflare e selecionar a conta e o projeto corretos.
- Configurar o subdomínio `portfolio.israelreispereira.com.br`, caso ele ainda não esteja configurado.
- Aprovar commits, publicação, mudanças de DNS e eventuais custos ou alterações de plano.
- Testar o site publicado e autorizar a divulgação definitiva.

### 3. Trabalho que pode ser delegado ao Copilot

Automatizável em grande parte- Analisar a especificação e montar o cronograma e o backlog.
- Criar a estrutura Astro + TypeScript e implementar componentes.
- Desenvolver validação de dados, importador CSV, filtros e visualizações.
- Escrever documentação, testes unitários e testes E2E.
- Verificar acessibilidade, responsividade, segurança básica e desempenho.
- Preparar configuração de build e deploy, diagnosticar falhas e produzir um checklist final.

Uma distinção importante: o Copilot pode preparar a publicação, mas não deve decidir sozinho o que é verdadeiro, legalmente publicável ou profissionalmente adequado, nem receber credenciais secretas em prompts. A capacidade de executar deploys depende das ferramentas, permissões e integrações habilitadas no seu ambiente.

## 2. As decisões que recomendo você fechar antes de começar

Para não deixar o planejamento travado por detalhes secundários, sugiro partir das seguintes decisões iniciais:

| Fator | Decisão inicial recomendada |
| --- | --- |
| Framework | Astro + TypeScript |
| Estilo | CSS próprio, visual minimalista e responsivo |
| Hospedagem | Cloudflare Pages, site estático |
| Repositório | GitHub, com histórico de alterações |
| Dados de demonstração | 20–50 registros, fictícios claramente identificados e reais com procedência |
| Mapa | Adiar até haver coordenadas confiáveis suficientes |
| Importador CSV | Incluído no MVP, com processamento local e download do JSON |
| Prospecção privada | Fora do MVP, sem dados privados no front-end |
| Qualidade | Vitest, Playwright e revisão de acessibilidade |
| Publicação | Primeiro preview de homologação; depois domínio definitivo |

Essas decisões já são coerentes com sua especificação. O ponto que você precisa decidir pessoalmente com mais atenção é a qualidade e a natureza dos dados reais, além do conteúdo da sua apresentação profissional.

Há também uma decisão de segurança: se o importador for apenas uma demonstração técnica, ele pode ser uma página de acesso claramente documentado, mas não deve ser confundido com uma área administrativa protegida. Tudo que é enviado ao navegador pode ser inspecionado pelo visitante.

## 3. O prompt principal para o GitHub Copilot

Use o prompt abaixo no Copilot Chat, no modo Agent, com o repositório do projeto aberto. O modo Agent é adequado quando você quer que o Copilot analise arquivos, proponha alterações e execute tarefas usando as ferramentas disponíveis no ambiente.

O objetivo deste primeiro prompt é fazê-lo planejar o projeto inteiro até a publicação, sem começar a criar arquivos antes de entender o estado atual do repositório.

Escrita

# PROMPT MESTRE — Planejamento completo até a publicação

## 1\. Seu papel

Atue como arquiteto de software, analista de requisitos, desenvolvedor sênior, especialista em qualidade, acessibilidade, segurança web, DevOps e mentor de um desenvolvedor iniciante.

Seu objetivo é transformar a especificação técnica fornecida neste repositório em um plano de execução completo, incremental, verificável e adequado para publicação em produção.

O projeto é o **Portfólio de Desenvolvimento + Diretório Inteligente de Empresas de Barretos-SP**.

O resultado final desejado é um site público em:

- Portfólio: https://portfolio.israelreispereira.com.br/
- Projetos: https://portfolio.israelreispereira.com.br/projetos/
- Diretório: https://portfolio.israelreispereira.com.br/projetos/mapa-empresas-barretos/

Não presuma que esses endereços já estejam funcionando. Verifique o estado real da infraestrutura antes de afirmar que estão configurados.

## 2\. Fonte de verdade

Antes de propor ou executar alterações:

1. Examine o repositório, os arquivos existentes, o Git, o README e as configurações de projeto.
2. Localize e leia a especificação técnica consolidada fornecida pelo proprietário.
3. Identifique o que já existe, o que está incompleto e o que ainda precisa ser criado.
4. Não sobrescreva arquivos, descarte alterações locais ou substitua configurações existentes sem autorização.
5. Se a especificação não estiver no repositório, solicite sua localização ou peça que seja adicionada. Não invente seu conteúdo.
6. Identifique conflitos entre a especificação, o estado atual do código e as práticas técnicas atuais.
7. Verifique versões, compatibilidade e documentação oficial das dependências e serviços antes de fixar versões ou afirmar limites e preços atuais.

Em caso de conflito, registre a divergência e proponha uma decisão fundamentada, sem alterar silenciosamente requisitos importantes.

## 3\. Arquitetura de referência

Considere como arquitetura inicial:

- Astro com geração estática de páginas.
- TypeScript com tipagem estrita.
- CSS próprio, responsivo e organizado.
- Git e GitHub para versionamento.
- Cloudflare Pages para hospedagem estática.
- Cloudflare DNS para o subdomínio, se necessário.
- JSON versionado para dados públicos aprovados.
- Papa Parse para leitura de CSV local.
- Zod para validação e normalização.
- Vitest para testes unitários.
- Playwright para testes de ponta a ponta.
- Leaflet somente quando houver coordenadas confiáveis e benefício real.

Não adicione banco de dados, autenticação, Workers, SSR ou infraestrutura paga sem uma necessidade justificada e aprovação do proprietário.

## 4\. Escopo obrigatório do MVP

Planeje a entrega de:

1. Página inicial do portfólio.
2. Página de projetos.
3. Página de apresentação do projeto Diretório de Empresas de Barretos.
4. Diretório com busca textual e filtros combinados.
5. Visualização em cards e tabela com resultados sincronizados.
6. Estados de verificação e tratamento explícito de informações desconhecidas.
7. Identificação da procedência e da data de coleta dos dados.
8. Conjunto de demonstração com 20–50 registros, distinguindo claramente dados fictícios e reais.
9. Importador CSV executado localmente no navegador, com validação, normalização, identificação de duplicatas e relatório de erros.
10. Download de JSON normalizado, sem publicação automática dos dados importados.
11. Layout responsivo e requisitos de acessibilidade WCAG 2.2 AA como objetivo de conformidade.
12. Testes unitários, testes E2E e documentação técnica.
13. Página 404, tratamento de erros e checklist de produção.
14. Build de produção e preparação do deploy em Cloudflare Pages.
15. Configuração e validação do domínio, quando os acessos necessários estiverem disponíveis.

O mapa pode ser adiado sem bloquear o lançamento inicial.

## 5\. Segurança, privacidade e dados

Considere obrigatórias as seguintes regras:

- Nunca inclua tokens, senhas, chaves privadas ou credenciais no código público, nos prompts ou nos arquivos versionados.
- Nunca inclua anotações comerciais privadas, hipóteses de prospecção ou dados internos nos arquivos públicos.
- Não invente empresas, contatos, fontes, licenças ou coordenadas apresentados como reais.
- Identifique explicitamente todos os registros fictícios.
- Registre a origem dos dados e os direitos de uso conhecidos.
- Diferencie dados desconhecidos de informações que não se aplicam.
- Não descarte duplicatas automaticamente sem produzir relatório.
- Não permita que uma importação inválida substitua os dados publicados.
- Minimize dados pessoais e sinalize dúvidas de privacidade para revisão humana.
- Não considere uma rota escondida ou uma interface sem link como mecanismo de autenticação.
- Não publique o importador como ferramenta administrativa segura se ele não tiver autenticação e autorização adequadas.
- Não prometa conformidade legal ou certificação de acessibilidade sem avaliação suficiente.

## 6\. Fase inicial: diagnóstico e planejamento

Nesta primeira execução, NÃO implemente o projeto inteiro e NÃO publique nada.

Produza um diagnóstico contendo:

A. Estado atual do repositório.

B. Requisitos funcionais e não funcionais, com rastreabilidade entre requisitos, tarefas e testes.

C. Backlog priorizado por dependências e criticidade, separado em:

- Bloqueadores.
- MVP obrigatório.
- Melhorias recomendadas.
- Pós-MVP.
- Itens que dependem de decisão humana.

D. Plano de execução com fases, tarefas pequenas, dependências, estimativa de esforço em faixas, riscos e entregáveis verificáveis.

E. Matriz RACI simplificada ou equivalente, identificando o que cabe ao proprietário, ao Copilot e aos serviços externos.

F. Plano de testes unitários, integração, E2E, acessibilidade, segurança básica, desempenho e validação de dados.

G. Plano de publicação com desenvolvimento local, integração com Git, preview de homologação, deploy de produção, domínio, HTTPS, monitoramento básico e rollback.

H. Lista de acessos e configurações que o proprietário precisa providenciar, sem solicitar ou expor segredos no chat.

I. Lista das decisões pendentes, cada uma acompanhada de:

- impacto;
- recomendação padrão;
- consequência de não decidir;
- momento limite para decidir.

J. Critérios objetivos de conclusão de cada fase.

K. Checklist completo de publicação derivado da especificação, incluindo todos os bloqueadores.

L. Plano de manutenção posterior, incluindo atualização dos dados, correções e revisão de dependências.

Apresente o plano de maneira compreensível para um desenvolvedor iniciante, explicando brevemente decisões técnicas relevantes.

## 7\. Arquivos de planejamento a preparar

Depois de analisar o repositório, proponha o conteúdo e a finalidade de:

- docs/PROJECT-PLAN.md
- docs/REQUIREMENTS.md
- docs/ARCHITECTURE.md
- docs/DATA-DICTIONARY.md
- docs/TEST-PLAN.md
- docs/SECURITY-AND-PRIVACY.md
- docs/DEPLOYMENT.md
- docs/RELEASE-CHECKLIST.md
- README.md

Evite duplicação desnecessária. Se já houver arquivos equivalentes, prefira atualizá-los com cuidado em vez de criar documentos concorrentes.

Não altere nem crie esses arquivos nesta primeira fase sem antes apresentar o diagnóstico e obter minha aprovação.

## 8\. Método de execução depois da aprovação

Após eu aprovar o plano:

1. Execute uma fase por vez.
2. Antes de cada fase, informe objetivo, arquivos que pretende alterar, dependências e critério de aceite.
3. Implemente em mudanças pequenas e coerentes.
4. Execute os testes e verificações aplicáveis.
5. Revise os resultados e corrija as falhas encontradas.
6. Informe os arquivos modificados, comandos executados, resultados reais e limitações restantes.
7. Atualize a documentação e o checklist conforme o trabalho realmente concluído.
8. Não marque uma tarefa como concluída apenas porque o código foi gerado.
9. Não ignore erros, testes falhos, avisos de segurança ou regressões.
10. Se faltar acesso, informação ou ferramenta, registre o bloqueio e forneça o procedimento necessário para eu resolver.
11. Se descobrir uma necessidade fora do escopo, explique o impacto e solicite autorização antes de ampliar o MVP.

## 9\. Portões de aprovação obrigatórios

Exija minha aprovação antes de:

- alterar significativamente a arquitetura ou ampliar o escopo;
- remover ou sobrescrever dados existentes;
- publicar dados reais cuja procedência ou autorização esteja incerta;
- adicionar serviços pagos ou gerar custos;
- executar operações destrutivas no Git ou alterar o histórico;
- modificar DNS ou configurações de domínio;
- realizar deploy de produção;
- divulgar o endereço como lançamento definitivo.

Você pode executar tarefas locais, reversíveis e dentro do escopo aprovado quando o ambiente permitir, respeitando as permissões configuradas.

## 10\. Definição de pronto

O projeto só poderá ser considerado pronto para lançamento quando:

- os requisitos obrigatórios estiverem implementados ou suas exceções tiverem sido formalmente aprovadas;
- o build de produção terminar sem erros;
- os testes críticos passarem;
- busca, filtros, cards e tabela funcionarem de maneira consistente;
- importações inválidas não comprometerem os dados aprovados;
- não houver segredos ou dados privados nos artefatos públicos;
- a navegação por teclado e os principais critérios de acessibilidade tiverem sido verificados;
- as fontes e os dados estiverem documentados;
- o preview tiver sido validado;
- o domínio e o HTTPS tiverem sido verificados, quando aplicáveis;
- o rollback estiver documentado;
- as limitações conhecidas estiverem registradas.

Diferencie sempre:

- implementado;
- testado;
- validado manualmente;
- publicado;
- ainda não verificado.

## 11\. Formato da primeira resposta

Responda inicialmente com:

1. Resumo executivo do estado encontrado.
2. Principais lacunas e riscos.
3. Plano de execução por fases.
4. Backlog priorizado.
5. Decisões que dependem de mim.
6. Acessos e preparações necessários.
7. Critérios de aceite e checklist de publicação.
8. Próxima ação recomendada.

Não comece a implementar ou publicar nesta primeira resposta. Termine solicitando minha aprovação do plano ou indicando a única informação realmente indispensável que estiver faltando.

Seja criterioso, incremental, transparente e orientado a entregas verificáveis. O objetivo é chegar à publicação real, e não apenas produzir código ou documentação.

## 4. Como usar o prompt sem perder o controle do projeto

O prompt mestre cria o plano. Depois, conduza a implementação por etapas, evitando que o agente tente resolver arquitetura, interface, dados, testes e infraestrutura em uma única execução.

## 1

Planejamento e diagnóstico

Peça o backlog, os riscos, as dependências e os critérios de aceite. Aprove o plano antes de começar a implementação.

Saída esperada: plano documentado e tarefas ordenadas.

## 2

Fundação do projeto

Solicite a estrutura Astro, TypeScript, CSS, rotas, documentação e configuração de qualidade.

Saída esperada: projeto executando localmente, com build funcional.

## 3

Interface e funcionalidades

Implemente portfólio, diretório, filtros, cards, tabela, estados de interface e dados de demonstração.

Saída esperada: fluxos principais utilizáveis em desktop e celular.

## 4

Importação e confiabilidade

Implemente Papa Parse, Zod, normalização, detecção de duplicatas, relatórios e download do JSON, com testes.

Saída esperada: importação segura e reproduzível, sem publicação automática.

## 5

Qualidade e homologação

Execute Vitest, Playwright, revisão de acessibilidade, testes responsivos, verificação de dados e build de produção.

Saída esperada: relatório de testes e lista de pendências reais.

## 6

Publicação

Configure a integração GitHub–Cloudflare Pages, valide o preview e prepare o domínio e o HTTPS. Faça o deploy definitivo apenas com sua aprovação.

Saída esperada: URL pública verificada, documentação e procedimento de rollback.

## 5. Prompt para executar cada fase com qualidade

Depois que o Copilot apresentar o planejamento e você o aprovar, utilize este prompt no início de cada fase.

Escrita

Execute a próxima fase aprovada do projeto, seguindo o plano documentado no repositório.

Antes de alterar arquivos:

1. Consulte o plano, os requisitos e os critérios de aceite da fase.
2. Confira o estado do Git e preserve minhas alterações existentes.
3. Informe o objetivo, os arquivos que pretende modificar e os riscos relevantes.

Durante a implementação:

- Trabalhe em pequenas entregas.
- Respeite a arquitetura e o escopo aprovados.
- Escreva código tipado, legível, modular e documentado quando necessário.
- Crie ou atualize testes para as regras implementadas.
- Não introduza dependências ou serviços desnecessários.
- Não invente dados reais nem inclua informações privadas nos arquivos públicos.
- Execute os testes e o build aplicáveis, verificando os resultados reais.
- Corrija as falhas que forem causadas pelas suas alterações.
- Se houver uma decisão que altere significativamente o escopo, pare e me consulte.

Ao terminar, apresente:

1. O que foi implementado.
2. Os arquivos criados e modificados.
3. Os testes executados e seus resultados.
4. Os critérios de aceite atendidos e não atendidos.
5. Os problemas conhecidos e as decisões pendentes.
6. O próximo passo recomendado.

Atualize a documentação e o checklist somente com informações verificadas. Não declare a fase concluída se houver critérios obrigatórios sem atendimento ou evidência.

Não faça deploy de produção nem altere DNS sem minha aprovação explícita.

## 6. O que você precisa preparar pessoalmente

Use este checklist para acompanhar sua parte. Você pode marcar os itens à medida que avançar.

## Checklist do proprietário

### 0/12

Projeto e desenvolvimento

[ ]Tenho o repositório Git criado ou sei onde o projeto existente está.

[ ]Tenho o VS Code e o ambiente Node.js funcionando.

[ ]Consigo executar os comandos de desenvolvimento e verificar os resultados.

Conteúdo e dados

[ ]Revisei a apresentação profissional e os links que serão públicos.

[ ]Defini as categorias iniciais do diretório.

[ ]Separei os dados fictícios dos reais e identifiquei as fontes dos dados reais.

Publicação

[ ]Tenho acesso ao GitHub e à conta Cloudflare correta.

[ ]Confirmei o estado atual do subdomínio e do DNS.

[ ]Consigo validar o site de homologação antes de autorizar o lançamento.

Aprovação final

[ ]Revisei o conteúdo, a privacidade e os resultados dos testes.

[ ]Confirmei o HTTPS, o funcionamento em dispositivos móveis e o procedimento de rollback.

[ ]Autorizei a publicação definitiva.

Copiar checklist  Limpar marcações

As marcações servem para acompanhar seu progresso nesta conversa; copie o checklist para mantê-lo no repositório ou em outro documento.

## 7. Como saber se o planejamento do Copilot está realmente bom?

Não avalie a resposta apenas pelo tamanho ou pela quantidade de tarefas. Verifique se ela responde a estas cinco perguntas:

- O que será feito primeiro? As dependências estão claras, sem começar pela infraestrutura antes de validar o projeto.
- Como saberei que funcionou? Cada tarefa tem um critério de aceite objetivo.
- O que depende de mim? Acessos, decisões, revisão de dados e autorizações estão identificados.
- Como evitaremos problemas? Existem testes, controles de privacidade, revisão de dados e rollback.
- Como chegaremos à publicação real? O plano inclui homologação, configuração de domínio, HTTPS e verificação do endereço público, não apenas o comando de build.

Minha sugestão é começar sem implementar o mapa e sem integrar fontes externas de dados em massa. Primeiro publique uma versão pequena, confiável e demonstrável do portfólio e do diretório; depois amplie os recursos.

Sua próxima ação: abra o repositório no VS Code, localize a especificação técnica consolidada e envie o Prompt Mestre ao Copilot Chat. Revise o plano que ele produzir e aprove a primeira fase antes de autorizar a implementação.

Assim, você não apenas terá um site publicado: terá também um projeto documentado, testável e com decisões técnicas que poderá explicar em entrevistas e apresentar no seu portfólio.