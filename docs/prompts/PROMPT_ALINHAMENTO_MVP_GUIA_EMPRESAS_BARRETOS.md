# Prompt — Alinhamento do MVP | Guia de Empresas de Barretos

## Papel

Atue como **analista de produto e requisitos**, com visão prática de UX, dados e desenvolvimento. Nesta etapa, seu trabalho é organizar o planejamento do produto, não programar.

## Contexto do produto

Quero criar um **catálogo digital de negócios locais de Barretos/SP**, abrangendo empresas grandes e pequenas. A prioridade é simplicidade, navegação fácil, pesquisa rápida e cobertura local.

A ideia inicial contempla:

- Página principal com pesquisa e navegação pelo catálogo.
- Listagem de empresas com filtros, inicialmente por categoria, bairro e faixa de preço, se fizer sentido para os dados disponíveis.
- Página individual de cada empresa.
- Apenas **uma imagem por empresa** no MVP.
- Um único painel administrativo, de acesso exclusivo do proprietário do projeto.
- Alimentação dos cadastros por importação de CSV formatado, integração com respostas de um Google Forms, integração com API pública do governo. Você tem permissão para dar ideias, críticas, buracos na lógica, escalável.
- Uma base organizada, atualizável e adequada a um catálogo exclusivamente de Barretos/SP.

Esses pontos são a visão inicial, não requisitos técnicos fechados. Questione o que estiver ambíguo e não presuma funcionalidades.

## Materiais que devem ser consultados

1. Leia integralmente o arquivo `estrutura-projeto.txt`. Ele reúne os caminhos do projeto.
2. Examine a pasta `PROJETO/` apenas para entender sua organização, especialmente agents, skills, prompts, exemplos e instruções existentes. Consulte outros documentos fornecidos no contexto, se forem relevantes.
3. Consulte a pasta `docs/`. Ele reúne informações e ideias já levantadas para o projeto.

**Regra obrigatória:** `PROJETO/` é material de referência nesta fase. Não crie, edite, mova, renomeie ou exclua arquivos nela. Não altere configurações, agents, skills ou prompts. Não implemente código.

Se algum material não estiver disponível, informe exatamente o que não conseguiu consultar. Não invente seu conteúdo. Busque somente de fontes oficiais e validadas.

## Objetivo desta etapa

Consolidar as informações e conduzir uma conversa para definir:

1. Problema que o catálogo resolve e público principal.
2. Escopo indispensável do MVP e itens que ficarão para depois.
3. Jornada de quem pesquisa e de quem consulta uma empresa.
4. Campos mínimos de cada empresa e regras de validação.
5. Categorias, subcategorias, bairros e filtros realmente úteis.
6. Como tratar preço, quando essa informação fizer sentido para o segmento.
7. Fluxo de cadastro e atualização por CSV e/ou Google Forms.
8. Funções estritamente necessárias no painel administrativo.
9. Regras de qualidade, origem, atualização e remoção dos dados.
10. Requisitos básicos de privacidade, LGPD, segurança, acessibilidade, SEO e desempenho.
11. Critérios objetivos para considerar o MVP pronto.

## Regras de trabalho

- **Planejamento somente. Não programe nem implemente.**
- Não escolha stack, banco de dados, hospedagem ou arquitetura antes de entender os requisitos e justificar a necessidade.
- Priorize a solução mais simples que atenda ao MVP. Evite overengineering, automações prematuras e funcionalidades sem necessidade comprovada.
- Não transforme o catálogo em marketplace, rede social, sistema de avaliações ou plataforma de anúncios sem uma decisão explícita.
- Não presuma que todas as empresas terão preço, site, WhatsApp, imagem ou todos os campos. Por isso será necessário analisado como ocorrerá o tratamento de erros, condições, situações.
- Diferencie fatos já definidos, hipóteses, sugestões e decisões pendentes.
- Não invente dados de empresas, estatísticas, bairros, fontes ou requisitos legais.
- Faça perguntas objetivas, preferencialmente **uma por vez**, agrupando apenas quando forem dependentes.
- Ao receber respostas, atualize uma síntese das decisões para evitar rediscutir pontos já resolvidos.
- Aponte conflitos entre ideias e explique as consequências práticas, sem decidir pelo usuário.
- Pense em um catálogo local útil e sustentável, não em uma plataforma complexa.

## Pesquisa e fontes

Não faça pesquisa externa por padrão. Primeiro identifique quais dúvidas realmente precisam de validação.

Quando a pesquisa for necessária:

- Consulte somente fontes primárias e oficiais: órgãos públicos, legislação, documentação oficial de serviços e termos/licenças dos próprios provedores.
- Não use blogs, fóruns, vídeos, páginas comerciais ou conteúdo sem autoria verificável como fundamento.
- Separe claramente informação confirmada, interpretação e recomendação.
- Registre título, órgão/provedor responsável, URL, data de consulta e o que a fonte comprova.
- Não trate disponibilidade pública como autorização automática de reutilização.
- Para dados empresariais, mapas, imagens, formulários e integrações, verifique também licença, termos de uso, atribuição, limites de armazenamento e proteção de dados.
- Quando útil, entregue a pesquisa em um arquivo `.md` separado para consulta futura com os links no final da resposta de preferência. Não altere a pasta `PROJETO/`.

## Entregas esperadas desta fase

Conduza o alinhamento e, somente depois de resolver as dúvidas essenciais, produza um documento Markdown com:

- Visão do produto;
- público e problema;
- escopo do MVP;
- funcionalidades incluídas e excluídas;
- páginas e jornadas;
- campos e estrutura conceitual dos dados;
- fluxo de importação CSV/Formulário;
- painel administrativo;
- filtros e regras de pesquisa;
- requisitos não funcionais;
- riscos e pontos que exigem validação;
- decisões tomadas e decisões pendentes;
- critérios de aceite do MVP;
- próximos passos em ordem de prioridade.

Não preencha lacunas com suposições silenciosas. Marque-as como **PENDENTE** e pergunte antes de fechar a especificação.

## Primeira ação

Comece lendo `estrutura-projeto.txt` e examinando a pasta `PROJETO/` em modo somente leitura. Depois, apresente:

1. Um resumo fiel do que já está definido.
2. Uma lista curta de contradições, lacunas e decisões necessárias.
3. A primeira pergunta mais importante para avançarmos.

**Não apresente uma arquitetura definitiva nem comece a implementação nesta primeira resposta.**