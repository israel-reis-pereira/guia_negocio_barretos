Especificação Arquitetural e Planejamento Integrado: Portfólio de Desenvolvimento e Diretório Inteligente de Barretos-SP

A concepção do projeto de mapeamento e diretório comercial de Barretos-SP nasce da convergência entre a consolidação de um portfólio profissional de desenvolvimento web e a resolução de um problema real de inteligência comercial local. A análise detalhada de todos os documentos de planejamento, pesquisas técnicas e propostas de arquitetura revela um consenso de engenharia: a construção de uma solução altamente eficiente, minimalista e escalável não exige a introdução prematura de bancos de dados relacionais complexos ou infraestruturas de servidor dispendiosas na fase inicial. Em vez disso, adota-se uma abordagem enxuta baseada em geração estática de sites (SSG), ilhas de interatividade reativa, validação rigorosa no cliente e implantação em redes de distribuição globais de custo zero.

1. Visão Geral do Produto e Arquitetura em Três Camadas

Conforme documentado nas especificações técnicas e no planejamento do projeto, a solução é concebida como um ecossistema modular dividido em três camadas distintas de funcionalidade, acesso e responsabilidade. Essa divisão garante a separação estrita de escopos, impedindo que informações privadas de prospecção comercial vazem para o público ou comprometam a privacidade de dados.

1.1 Detalhamento das Camadas do Sistema

A arquitetura estabelece limites claros entre o conteúdo estático do portfólio, a aplicação de consulta pública e as ferramentas comerciais internas:

* Camada 1 — Portfólio Público (Apresentação Profissional): Disponibilizada no subdomínio principal, apresenta a trajetória do desenvolvedor, competências técnicas, documentação arquitetural e o catálogo de projetos desenvolvidos. Atua como o ponto de entrada institucional e vitrine de aprendizado.
* Camada 2 — Diretório Público de Empresas de Barretos-SP (Aplicação de Descoberta): Aplicação web leve acessível via subcaminho ou subdomínio dedicado. Permite à população e aos comerciantes pesquisar estabelecimentos por nome, filtrar por categorias, bairros e faixas de preço, além de visualizar os resultados em formato de cards, tabela sincronizada e mapa interativo opcional.
* Camada 3 — Prospecção Privada e Inteligência Comercial (Área Interna Futura): Camada reservada exclusivamente ao uso do desenvolvedor para registro de hipóteses comerciais, avaliação de maturidade digital das empresas e priorização de abordagens de serviços. Esta camada é mantida totalmente desconectada do repositório estático público.

1.2 Delimitação do Escopo do Mapeamento (MVP vs. Evolução)

Para garantir que o projeto saia do papel e mantenha uma entrega incremental sustentável, os documentos de planejamento definem rigorosamente o que integra a versão inicial funcional (MVP) e o que deve ser postergado para fases futuras.

Dimensão de Escopo	Funcionalidades Incluídas no MVP	Funcionalidades Posteradas (Pós-MVP)	Fora de Escopo (Excluídas)
Portfólio	Página inicial, listagem de projetos, documentação de decisões e estudos de caso.	Painel dinâmico de métricas de leitura e comentários.	Sistema de blog multiautor com CMS pesado.
Diretório Público	Busca textual, filtros combinados, visualização em cards e tabela, dataset controlado (20–50 registros), indicação de procedência e status de verificação.	Integração automática com APIs de órgãos governamentais (RFB/SEADE) e mapa com alta densidade de coordenadas validadas.	Cadastro público por autoatendimento, avaliações de usuários, anúncios patrocinados e planos comerciais.
Ingestão de Dados	Upload e parsing de CSV no navegador, validação com Zod, relatório de importação e download de JSON normalizado.	Pipeline de limpeza automatizado em nuvem e sincronização em tempo real.	Scraping em massa não autorizado e robôs de varredura irrestrita.
Infraestrutura	Compilação estática com Astro, hospedagem no Cloudflare Pages e gerenciamento DNS no Registro.br/Cloudflare.	Execução de rotas dinâmicas em Cloudflare Workers, banco SQL Cloudflare D1 e autenticação com Cloudflare Access.	Servidores dedicados, máquinas virtuais ou bancos de dados relacionais gerenciados de alto custo.

2. Avaliação Crítica da Stack Tecnológica e Decisões de Engenharia

A seleção das tecnologias não responde a tendências de mercado ou preferências pessoais, mas a critérios objetivos de desempenho, facilidade de manutenção para um desenvolvedor iniciante e custo operacional nulo. As pesquisas técnicas compararam rigorosamente cinco alternativas de implementação para a camada de apresentação e componentes interativos.

2.1 Análise Comparativa de Tecnologias Front-End

A tabela abaixo sintetiza a avaliação de arquitetura e viabilidade das opções consideradas nas pesquisas do projeto:

Critério de Avaliação	HTML/CSS/TS Puro	Astro + TypeScript	React + Vite + TS	Vue 3 + Vite + TS	SvelteKit + TS
Modelo de Renderização	Páginas estáticas manuais com scripts soltos.	Gerador de Site Estático (SSG) com Ilhas de Reatividade.	Aplicação de Página Única (SPA) por padrão.	Aplicação de Página Única (SPA) por padrão.	Framework Full-Stack (SSR/SSG).
JavaScript Enviado ao Cliente	Mínimo (apenas scripts manuais).	Zero por padrão; JS enviado apenas para componentes interativos.	Bundle completo do runtime do React + aplicação.	Bundle completo do runtime do Vue + aplicação.	Depende do modo; tende a enviar o runtime do framework.
Curva de Aprendizado para Iniciantes	Baixa no início, mas cresce rapidamente sem estrutura.	Baixa a Média (conceitos claros de páginas e layouts).	Média a Alta (gerenciamento de estado, hooks, roteamento).	Média (reatividade simples, mas ecossistema amplo).	Alta (fronteiras entre servidor e cliente, SSR).
Adequação a Conteúdo Estático e SEO	Excelente, porém totalmente manual.	Excelente (SSG nativo, SEO otimizado, Content Collections).	Boa, mas exige ferramentas adicionais para pré-renderização.	Boa, exigindo plugins de SSG adicionais.	Muito boa, porém introduz complexidade excessiva de infraestrutura.
Integração com Cloudflare Pages	Build estático simples sem dependências.	Build estático direto em Pages sem necessidade de adaptadores.	Build estático gerado via Vite para Pages.	Build estático gerado via Vite para Pages.	Exige adaptador específico (@sveltejs/adapter-cloudflare).

2.2 Justificativa da Escolha do Astro e Critérios de Revisão

Como demonstrado pela análise de engenharia, o Astro oferece o melhor equilíbrio para o projeto. Ele entrega HTML puro para o portfólio e para as páginas informativas, permitindo utilizar partial hydration (ilhas) somente onde os filtros do diretório exigem interatividade. Isso elimina a sobrecarga de carregar um runtime pesado de SPA para exibir conteúdos estáticos.

Os documentos técnicos estabelecem critérios claros para revisar essa decisão no futuro: caso o diretório evolua para um painel com edição em tempo real, estado altamente complexo e encadeado em uma única tela, ou exija controle multiusuário dinâmico, o projeto poderá migrar módulos específicos para React ou Vue, que são perfeitamente suportados como ilhas dentro do ecossistema Astro.

2.3 Ferramentas Complementares da Stack

O ecossistema é complementado por bibliotecas especializadas que resolvem tarefas específicas sem inchar o código:

* TypeScript: Garante tipagem estática rigorosa para todas as entidades de negócio, esquemas de dados e funções de filtro, prevenindo erros em tempo de compilação.
* Papa Parse: Biblioteca leve e rápida escolhida para realizar o parsing de arquivos CSV no navegador, tratando delimitadores, aspas e quebras de linha com eficiência.
* Zod: Responsável pela validação de esquema e sanitização dos dados importados, garantindo que nenhum registro fora da especificação seja processado.
* Leaflet.js: Biblioteca open-source de mapeamento interativo, utilizada para plotar estabelecimentos com coordenadas confirmadas sobre camada de dados do OpenStreetMap.
* Vitest: Framework de testes unitários integrado nativamente ao ecossistema Vite/Astro, utilizado para validar regras de negócio, normalização e filtros.
* Playwright: Ferramenta de automação E2E responsável por simular jornadas completas de usuários em múltiplos navegadores reais.

3. Infraestrutura, Domínios e Topologia de Hospedagem na Cloudflare

A infraestrutura de publicação foi projetada para oferecer resiliência de nível empresarial com custo fixo de operação equivalente a zero, aproveitando as integrações nativas da Cloudflare.

3.1 Configuração de Domínio e Gerenciamento DNS

O domínio principal israelreispereira.com.br é registrado junto ao Registro.br. Os servidores de nome (nameservers) são apontados para a infraestrutura da Cloudflare, que atua como DNS autoritativo e camada de segurança. A publicação do portfólio e do diretório ocorre sob a estrutura de subdomínio portfolio.israelreispereira.com.br, com o diretório acessível pelo caminho /projetos/mapa-empresas-barretos. Essa abordagem centraliza o certificado SSL/TLS e simplifica a gestão de rotas sem exigir registros DNS adicionais para cada projeto.

3.2 Comparação entre Cloudflare Pages e Cloudflare Workers

As pesquisas técnicas esclarecem as diferenças fundamentais entre os dois serviços de hospedagem da Cloudflare, fundamentando a escolha para cada etapa do projeto:

[ Registro.br (Domínio) ] ──> [ Cloudflare DNS Autoritativo ]
                                            │
                                            ▼
                              [ Cloudflare Pages (MVP Estático) ]
                                 ├── Astro SSG (Build via Git)
                                 ├── Assets Estáticos Gratuitos/Ilimitados
                                 └── Módulo de Filtros/CSV no Cliente
                                            │
                                            ▼ (Evolução Pós-MVP)
                              [ Cloudflare Workers & D1 (APIs / SQL) ]
                                 ├── Autenticação via Cloudflare Access
                                 └── Banco de Dados Relacional Serverless


Em sua fase MVP, a aplicação utiliza exclusivamente o Cloudflare Pages, pois a requisição de assets estáticos é totalmente gratuita e ilimitada. O deploy é automatizado via integração contínua (CI/CD) conectada ao repositório GitHub. A introdução de Cloudflare Workers (funções serverless), Cloudflare D1 (banco SQL) e Cloudflare Access fica reservada para a evolução pós-MVP, quando houver necessidade de autenticar o desenvolvedor e persistir registros de prospecção comercial online.

4. Estratégia de Fontes de Dados e Auditoria Cadastral

Um dos achados mais críticos das especificações técnicas é a distinção entre obter dados cadastrais de empresas e obter dados comerciais verificados e geolocalizados. Nenhuma fonte pública isolada oferece um catálogo completo e pronto para consumo em um guia comercial.

4.1 Avaliação das Fontes Governamentais e Privadas

Os documentos auditam três principais origens de dados para o município de Barretos-SP:

* Dados Abertos da Receita Federal (CNPJ): Fonte oficial gratuita que fornece razão social, nome fantasia, CNPJ, situação cadastral, CNAE, endereço e CEP. No entanto, não garante que a empresa esteja ativamente atendendo no local, nem disponibiliza telefones comerciais atualizados, WhatsApp, sites ou coordenadas de mapa.
* SEADE (Empresas no Estado de SP): Dataset sob licença Creative Commons Attribution (CC BY 4.0) com recortes estatísticos de atividade econômica e porte por município. Útil para compreender a distribuição do mercado local, mas ineficiente para contatos comerciais diretos.
* Google Places API / Google Business Profile API: Oferece dados ricos como horários, avaliações e fotos. Contudo, as pesquisas técnicas desaconselham seu uso para montar o catálogo do D1 ou arquivos estáticos devido às restrições rígidas das políticas do Google, que proíbem o armazenamento permanente e a redistribuição de dados extraídos da plataforma fora de instâncias autorizadas de visualização.

4.2 Modelo Convergente: Cadastro Próprio com Validação Oficial

A estratégia adotada combina a confiabilidade dos registros oficiais com a curadoria comercial humana. A Receita Federal é utilizada para validar a existência legal e o CNPJ do estabelecimento, enquanto as informações comerciais (WhatsApp, atendimento presencial, horários de funcionamento, tabela de preços e links) são verificadas e inseridas manualmente via planilha-mestre.

5. Modelo de Dados Conceitual e Contratos de Entidades

Para garantir que o sistema seja escalável e permita adicionar novos campos sem reescrever a aplicação, o modelo de dados é estruturado em contratos lógicos rígidos em TypeScript.

5.1 Especificação da Entidade Principal (Business)

A entidade Business representa o estabelecimento comercial exibido no diretório público. O contrato diferencia rigorosamente a ausência de informação de uma resposta negativa, utilizando null para indicar valores explicitamente desconhecidos (por exemplo, websiteUrl: null significa que o site é desconhecido, não que a empresa não possui site).

Campo	Tipo Conceitual	Regra de Validação	Significado e Uso no Sistema
id	string	Obrigatório; UUID ou slug único.	Identificador interno estável e independente da posição na planilha.
name	string	Obrigatório; mínimo 2 caracteres.	Nome comercial de exibição pública da empresa.
categoryIds	string[]	Obrigatório; mínimo 1 elemento.	Lista de IDs que associam a empresa às categorias cadastradas.
description	string | null	Opcional; texto limpo.	Resumo sobre serviços, diferenciais ou história do negócio.
address	Object | null	Opcional; objeto estruturado.	Contém logradouro, número, bairro, cidade, estado e CEP.
phone	string | null	Opcional; formato DDD + número.	Telefone fixo comercial verificado.
websiteUrl	string (URL) | null	Opcional; formato URL válido.	Link oficial do site do estabelecimento.
socialLinks	Object | null	Opcional; mapa de URLs.	Links para perfis em redes sociais (Instagram, Facebook).
coordinates	{lat: number, lng: number} | null	Opcional; intervalos lat [-90,90], lng [-180,180].	Latitude e longitude precisas para plotagem no mapa.
sourceIds	string[]	Obrigatório; mínimo 1 fonte.	IDs das fontes de informação que fundamentam os dados publicados.
verificationStatus	Enum	Obrigatório; valores restritos.	Status de verificação: unverified, verified, needs_review, inactive.
lastVerifiedAt	ISO Date String | null	Opcional; data válida.	Data da última confirmação humana das informações comerciais.
createdAt	ISO Date String	Obrigatório; data de inclusão.	Registro de quando a empresa foi cadastrada no sistema.
updatedAt	ISO Date String	Obrigatório; data de alteração.	Registro de quando ocorreu a última modificação no cadastro.

5.2 Entidades Complementares de Apoio

O modelo é sustentado por quatro entidades adicionais que garantem a rastreabilidade e a expansão do sistema:

// Exemplo de representação das entidades de apoio no sistema
interface Category {
  id: string;
  name: string;
  slug: string;
  description: string | null;
  parentId: string | null; // Suporte a subcategorias
}

interface Source {
  id: string;
  name: string;
  sourceUrl: string | null;
  sourceType: 'manual' | 'csv_oficial' | 'site_oficial' | 'dados_abertos';
  license: string | null;
  collectedAt: string;
  notes: string | null;
}

interface ImportJob {
  id: string;
  filename: string;
  startedAt: string;
  completedAt: string;
  status: 'pending' | 'analyzed' | 'applied' | 'failed';
  totalRows: number;
  acceptedRows: number;
  rejectedRows: number;
  duplicateRows: number;
  errors: Array<{ line: number | null; code: string; message: string }>;
}

// Entidade estritamente isolada na camada privada (Pós-MVP)
interface ProspectingRecord {
  businessId: string;
  reviewStatus: 'todo' | 'in_progress' | 'contacted' | 'closed';
  opportunityTypes: string[]; // ex: ['site', 'agendamento_online', 'cardapio']
  priority: 'low' | 'medium' | 'high';
  notes: string;
  lastReviewedAt: string;
}


6. Pipeline de Importação, Normalização e Resolução de Duplicidades

A ingestão de dados representa o módulo técnico central da aplicação. Para evitar que erros em arquivos CSV comprometam a estabilidade do site ou insiram registros corrompidos, o fluxo é processado em etapas bem definidas.

6.1 Fluxo Operacional de Importação no Cliente

O módulo de importação executa integralmente no navegador do mantenedor, seguindo uma sequência transacional e auditável:

1. Seleção do Arquivo: O mantenedor faz o upload do arquivo CSV com codificação UTF-8.
2. Parsing com Papa Parse: A biblioteca converte a string do arquivo em objetos JavaScript brutos, capturando erros sintáticos de delimitadores ou aspas.
3. Sanitização e Normalização: O sistema aplica regras de limpeza, como remoção de espaços nas extremidades (trim), padronização de maiúsculas/minúsculas e conversão de valores vazios em null.
4. Validação de Esquema com Zod: Cada linha é submetida ao esquema tipado do Zod. Registros com erros em campos obrigatórios são marcados para rejeição.
5. Deduplicação e Classificação: O sistema compara o CNPJ de 14 dígitos (identificador primário) e a combinação de nome normalizado + endereço (chave secundária) para identificar duplicatas.
6. Geração do Relatório de Auditoria: Uma prévia exibe o total de registros analisados, divididos em aceitos, rejeitados, pendentes de revisão e duplicados.
7. Exportação do JSON Limpo: Após a confirmação humana, o sistema gera o arquivo businesses.json normalizado para download, que é revisado e commitado no repositório Git.

6.2 Regras de Tratamento de Erros de Importação

O pipeline garante resiliência na ingestão, tratando falhas sem interromper o processamento global:

Comportamento diante de Inconsistências: O sistema não descarta erros silenciosamente nem sobrescreve a base de produção automaticamente. Erros de linha (por exemplo, um e-mail malformado ou coordenada inválida) resultam na rejeição daquela linha específica com mensagem explicativa detalhada, mantendo as demais linhas válidas no lote de importação. Se o cabeçalho do CSV estiver corrompido ou faltarem colunas obrigatórias, a importação inteira é abortada com um alerta de erro crítico.

7. Diretrizes de Geolocalização, Leaflet e Resiliência da Interface

A inclusão de um mapa interativo enriquece a experiência visual, mas introduz dependências de serviços externos que devem ser gerenciadas com cautela.

7.1 Requisitos para Integração do Leaflet e OpenStreetMap

O mapa utiliza a biblioteca Leaflet.js consumindo tiles do OpenStreetMap (OSM). A utilização desses serviços exige conformidade estrita com as políticas oficiais da OpenStreetMap Foundation:

* Exibição de Atribuição: Todos os mapas devem apresentar de forma visível os créditos "© OpenStreetMap contributors".
* Respeito aos Limites de Tiles: É proibido realizar prefetching em massa ou scraping de imagens de tiles. O caching local no navegador deve ser ativado.
* Geocodificação via Nominatim: A API pública do Nominatim é restrita a 1 requisição por segundo. O projeto proíbe chamadas de geocodificação em tempo real durante a navegação dos usuários. Toda coordenada deve ser pré-calculada e armazenada no dataset.

7.2 Princípio da Resiliência e Fallback de Interface

O mapa é tratado como um recurso complementar, nunca como a única forma de acessar as informações. Caso a conexão com os servidores de tiles falhe ou determinado estabelecimento não possua coordenadas válidas, a interface mantém 100% de sua funcionalidade através das visualizaciones sincronizadas em cards e tabela.

8. Segurança da Informação, LGPD e Isolamento de Dados Sensíveis

A conformidade legal e a proteção de dados são tratadas como requisitos arquiteturais obrigatórios desde o primeiro dia de planejamento.

8.1 Separação Rígida entre Dados Públicos e Privados

Um dos alertas mais enfáticos da pesquisa técnica estabelece que ocultar colunas na interface ou utilizar senhas simples em código JavaScript no cliente não protege os dados. Qualquer arquivo JSON publicado na pasta src/data/ ou enviado ao navegador pode ser inspecionado por qualquer visitante.

Por esse motivo, as anotações comerciais da ProspectingRecord e hipóteses de abordagens de vendas ficam estritamente isoladas em ambiente offline ou em bancos de dados futuros protegidos por autenticação server-side.

8.2 Conformidade com a Lei Geral de Proteção de Dados (LGPD - Lei 13.709/2018)

Mesmo tratando predominantemente de dados cadastrais de pessoas jurídicas (CNPJ), a aplicação observa as diretrizes da Autoridade Nacional de Proteção de Dados (ANPD):

* Minimização da Coleta: Apenas dados estritamente necessários para a identificação do estabelecimento comercial são publicados.
* Tratamento de Dados de Pessoas Físicas: Microempreendedores Individuais (MEIs) cujo nome empresarial contenha nome civil ou telefone pessoal têm seus direitos resguardados, garantindo canal de atendimento para solicitação de remoção ou atualização de dados.
* Ausência de Credenciais: O repositório público não armazena nenhuma chave de API privada, token de acesso ou segredo de servidor.

9. Arquitetura do Repositório, UX, Acessibilidade (WCAG 2.2 AA) e Testes

A organização do código-fonte e o padrão de design foram projetados para manter o repositório limpo, testável e fácil de navegar.

9.1 Estrutura de Diretórios do Projeto

A estrutura proposta separa claramente os componentes visuais, utilitários de negócio e dados:

portfolio-barretos/
├── public/                  # Assets estáticos (favicons, imagens estáticas)
├── src/
│   ├── components/          # Componentes visuais desacoplados da lógica complexa
│   │   ├── SiteHeader.astro
│   │   ├── SiteFooter.astro
│   │   ├── BusinessCard.astro
│   │   ├── BusinessFilters.astro
│   │   └── BusinessTable.astro
│   ├── content/             # Collections de conteúdo do portfólio em Markdown
│   ├── data/                # JSONs públicos aprovados para produção
│   │   ├── businesses.json
│   │   └── categories.json
│   ├── layouts/             # Layouts base da aplicação
│   │   └── BaseLayout.astro
│   ├── lib/                 # Regras de negócio puras (sem dependências de UI)
│   │   ├── business-schema.ts
│   │   ├── normalize-business.ts
│   │   ├── filter-businesses.ts
│   │   └── csv-import.ts
│   └── pages/               # Roteamento baseado em arquivos
│       ├── index.astro
│       └── projetos/
│           └── mapa-empresas-barretos.astro
├── tests/
│   ├── unit/                # Suíte Vitest para validação de regras de negócio
│   └── e2e/                 # Suíte Playwright para testes de navegação real
├── docs/                    # Documentação técnica do projeto
│   ├── ARCHITECTURE.md
│   ├── DATA-DICTIONARY.md
│   └── DEPLOYMENT.md
├── astro.config.mjs
└── package.json


9.2 Direção Visual e Diretrizes de Acessibilidade (WCAG 2.2 Nível AA)

A interface adota um estilo minimalista com fundo claro (#f6f7f4), texto em grafite de alto contraste (#202923) e uma única cor de destaque para elementos de ação. A acessibilidade é garantida por critérios verificáveis:

* Navegação Integral por Teclado: Todos os controles (busca, filtros, alternância de visualização) são acessíveis via tecla Tab, com estado de foco claramente visível.
* Semântica Rígida: Utilização de um único elemento <h1> por página, seguido por hierarquia lógica de <h2> e <h3>, além de rótulos <label> associados a todos os formulários.
* Leitores de Tela: Regiões de atualização dinâmica (como a contagem de resultados filtrados) utilizam atributos aria-live="polite" para anunciar alterações aos usuários.

9.3 Estratégia de Testes Automatizados

A qualidade do código é assegurada por duas camadas de testes:

[ Regras de Negócio (src/lib/) ] ──> [ Vitest (Testes Unitários Rápidos) ]
                                          ├── Validação de Esquemas Zod
                                          ├── Normalização de Strings/CNPJ
                                          └── Lógica de Filtros Combinados

[ Aplicação em Execução ] ─────────> [ Playwright (Testes E2E em Browsers) ]
                                          ├── Fluxo de Busca e Filtro de Cards
                                          ├── Sincronização com Tabela
                                          └── Resiliência a Falhas de Rede


10. Plano de Execução Incremental, Matriz de Riscos e Checklist de Publicação

A implementação do projeto segue um cronograma dividido em seis etapas bem delimitadas, prevenindo o crescimento descontrolado do escopo.

10.1 Cronograma de Execução Incremental em 6 Etapas

1. Etapa 1 — Especificação e Requisitos: Consolidação da documentação arquitetural, esquema de dados e regras de negócio em arquivos .md no repositório.
2. Etapa 2 — Protótipo HTML Autocontido: Criação do arquivo preview.html com estilos e filtros estáticos para validar a navegação e a UX em dispositivos móveis.
3. Etapa 3 — Estrutura Astro e Roteamento: Inicialização do projeto Astro com TypeScript, criação das páginas do portfólio e integração do dataset JSON inicial.
4. Etapa 4 — Pipeline de Importação CSV: Desenvolvimento do módulo de leitura com Papa Parse e validação com Zod, com geração do relatório de auditoria e download do JSON.
5. Etapa 5 — Mapeamento e Geolocalização: Adição opcional da camada Leaflet e tiles OSM, garantindo a sincronização dos filtros e o fallback para modo lista.
6. Etapa 6 — Qualidade, Testes e Deploy: Execução das suítes de teste (Vitest/Playwright), revisão de acessibilidade, conexão ao Cloudflare Pages e apontamento do subdomínio.

10.2 Matriz de Gestão de Riscos Priorizados

A tabela a seguir apresenta os principais riscos mapeados e suas respectivas estratégias de prevenção:

Risco Mapeado	Probabilidade	Impacto	Medida Preventiva Mapeada	Plano de Resposta em Crise
Escopo excessivo para iniciante	Alta	Alto	Congelar o MVP em visualização estática e dataset de 20–50 registros.	Postergar banco de dados, autenticação e mapas para versões futuras.
Exposição acidental de dados privados	Média	Alto	Isolar a entidade ProspectingRecord fora de arquivos estáticos.	Remover o repositório imediatamente, limpar o histórico Git e reemitir chaves.
Inconsistência de coordenadas geográficas	Alta	Médio	Condicionar a exibição do mapa à verificação prévia das coordenadas.	Desativar o componente de mapa e manter a aplicação em modo cards/tabela.
Bloqueio por uso excessivo de tiles OSM	Média	Médio	Ativar caching local no navegador e proibir chamadas em massa.	Alternar para outro provedor de tiles gratuito ou exibir aviso de indisponibilidade.

10.3 Checklist Bloqueador de Lançamento em Produção

Antes de autorizar a publicação definitiva no subdomínio de produção, a seguinte lista de verificação deve ser 100% cumprida:

* [ ] Build de produção gerado via npm run build sem nenhum erro ou aviso de compilação.
* [ ] Auditoria efetuada confirmando ausência total de chaves secretas ou dados de prospecção em src/data/.
* [ ] Navegação por teclado e teste de contraste aprovados conforme diretrizes WCAG 2.2 AA.
* [ ] Suíte de testes unitários (Vitest) e testes E2E (Playwright) executados com 100% de aprovação.
* [ ] Subdomínio portfolio.israelreispereira.com.br vinculado corretamente ao projeto no Cloudflare Pages com HTTPS ativo.
