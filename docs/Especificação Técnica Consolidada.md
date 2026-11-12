# Especificação Técnica Consolidada  
**Portfólio de Desenvolvimento + Diretório Inteligente de Empresas de Barretos-SP**  
_Data da pesquisa técnica: 21/10/2026_

---

## 1. Resumo executivo

### Visão do produto

- **Camada 1 — Portfólio público**  
  Site pessoal em `portfolio.israelreispereira.com.br` com:
  - apresentação profissional,
  - lista de projetos (incluindo o diretório de empresas),
  - documentação das decisões técnicas e aprendizados.

- **Camada 2 — Diretório público de empresas (Barretos-SP)**  
  Aplicação web acessível via caminho:
  - `portfolio.israelreispereira.com.br/projetos/mapa-empresas-barretos`
  que permite:
  - buscar e filtrar estabelecimentos por nome, categoria e outros campos,
  - visualizar em **cards** e **tabela**,
  - opcionalmente exibir **mapa** com Leaflet quando houver coordenadas confiáveis.

- **Camada 3 — Prospecção privada (futura, fora do MVP)**  
  Área separada (outro app ou ao menos outra base) para:
  - registrar hipóteses comerciais, prioridades e notas privadas,
  - nunca expor esses dados no front-end público nem em arquivos estáticos.

### Recomendação arquitetural (fase MVP)

**Stack recomendada para o MVP:**

- **Astro** como gerador de site estático + ilhas de interatividade.  
  - Arquitetura “islands” com hidratação seletiva reduz JS enviado ao cliente em relação a SPAs, pois apenas componentes interativos são hidratados. 
- **TypeScript** para tipagem estática das entidades e funções de negócio. 
- **CSS próprio** (sem Tailwind inicialmente) para manter controle e aprendizado explícito.
- **Papa Parse** para parsing de CSV no navegador em um módulo de importação/preview. 
- **Zod** para validação de dados conforme esquema.
- **Leaflet** para mapa interativo quando houver dados geográficos confiáveis. 
- **Vitest** para testes unitários de regras de negócio (integra-se bem com projetos baseados em Vite, o que inclui Astro). 
- **Playwright** para testes E2E em múltiplos navegadores. 
- **Hospedagem estática principal: Cloudflare Pages + DNS Cloudflare**  
  - Pages oferece deploy automático via Git e requests para *assets estáticos* livres e ilimitados no plano gratuito; funções (Pages Functions) são tarifadas como Workers, mas não serão usadas no MVP. 
  - DNS autoritativo na Cloudflare permite gerenciar subdomínios como `portfolio.israelreispereira.com.br` apontando para o projeto Pages. 

**Cloudflare Workers no plano evolutivo (não no MVP):**

- **Cloudflare Workers** (e eventualmente D1) são reservados para:
  - futura autenticação,
  - prospecção privada,
  - importações persistentes e APIs.
- Workers Free: ~100k requisições/dia e 10 ms de CPU por requisição gratuitos; depois, US$ 0,30/milhão de requisições no plano pago. 

### Justificativa resumida

- Para o MVP:
  - **quase todo conteúdo é estático**, com um módulo de filtros e importação rodando 100% no cliente.
  - Astro resolve rotas, layout, SEO, conteúdo estático e permite JS apenas onde necessário, o que atende o foco em desempenho para mobile.
  - Cloudflare Pages oferece CI/CD simples, domínio customizado e custo zero para estático.
- **Cloudflare Workers** e back-end só entram quando aparecer necessidade real de:
  - escrita persistente multiusuário,
  - prospecção privada online,
  - APIs ou integrações que não possam rodar apenas no navegador.

---

## 2. Requisitos

### 2.1 Funcionais

**Portfólio (Camada 1)**

- RF1. Exibir página inicial com apresentação profissional, tecnologias e objetivos.
- RF2. Listar projetos com:
  - nome, descrição curta,
  - tecnologias usadas,
  - link para página do projeto.
- RF3. Página do projeto “Mapa de empresas de Barretos” com:
  - resumo do problema,
  - decisões arquiteturais,
  - link para a aplicação em si.

**Diretório público (Camada 2)**

- RF4. Listar estabelecimentos em Barretos-SP, obtidos de um conjunto de dados controlado.
- RF5. Buscar por texto (nome + termos relevantes).
- RF6. Filtrar combinando:
  - categoria(s),
  - bairro ou área básica (quando disponível),
  - estado de verificação.
- RF7. Apresentar resultados:
  - em **cards**,
  - em **tabela**, garantindo que ambas as visões mostrem o mesmo subconjunto e contagens.
- RF8. Indicar para cada estabelecimento:
  - quais informações são **desconhecidas** vs **não se aplicam**,
  - estado de verificação (`unverified`, `verified`, `needs_review`, `inactive`).
- RF9. Exibir procedência básica dos dados (fonte principal, data de coleta).
- RF10. Exibir mapa (Leaflet) opcionalmente, apenas para registros com coordenadas válidas.
- RF11. Continuar funcional sem mapa (lista/tabela funcionando mesmo que mapa falhe).
- RF12. Módulo de importação (uso técnico, não necessariamente exposto para público geral) que:
  - carregue CSV local via upload,
  - valide, normalize e classifique registros,
  - apresente **relatório detalhado** (aceitos, rejeitados, duplicatas, pendentes),
  - permita baixar um JSON normalizado para ser versionado no Git.

**Prospecção privada (Camada 3 – futura)**

- RF13. Manter registros de prospecção (hipóteses comerciais, prioridades, notas) **separados** dos dados públicos, em outro armazenamento; não implementar no MVP.

### 2.2 Não funcionais

- RNF1. **Desempenho**:
  - HTML inicial leve, JS apenas para filtros/importação.
  - Otimizar para redes móveis (3G/4G) e dispositivos modestos.
- RNF2. **Acessibilidade**:
  - Alinhar-se às diretrizes **WCAG 2.2 nível AA** para conteúdo web: teclado, contraste, hierarquia, estados, etc. 
- RNF3. **Segurança**:
  - Nenhuma credencial ou dado privado em código cliente.
  - Nenhuma anotação de prospecção ou dado pessoal sensível em JSON público.
- RNF4. **Privacidade (LGPD)**:
  - Aplicar princípios da Lei 13.709/2018 para qualquer dado pessoal (ex.: nome de pessoa física, telefone pessoal) 
  - Reduzir ao mínimo a coleta de dados pessoais.
- RNF5. **Manutenibilidade**:
  - Código organizado por responsabilidades (UI vs regras de negócio vs dados).
  - Testes automatizados para as funções-chave.
- RNF6. **Evolução incremental**:
  - Permitir migração futura para Workers, outro framework ou back-end, sem reescrever tudo.

---

## 3. Escopo do MVP

### 3.1 Incluído

- Portfólio estático com pelo menos:
  - home,
  - página “projetos”,
  - página detalhada do diretório de empresas.
- Diretório público com:
  - dataset controlado (20–50 registros, misto fictício/real, claramente sinalizado),
  - busca textual,
  - filtros combinados,
  - cards e tabela sincronizados,
  - indicação de procedência e estado de verificação,
  - estado de erro, vazio, carregamento,
  - módulo de importação CSV **cliente-side** com relatório completo e opção de baixar JSON.
- Layout minimalista responsivo + primeiros testes de acessibilidade.

### 3.2 Pós-MVP

- Importação a partir de fontes externas oficiais (RFB CNPJ, SEADE) com:
  - limpeza pesada,
  - deduplicação em escala,
  - enriquecimento incremental.
- Mapa com coordenadas reais para um subconjunto significativo de estabelecimentos.
- Ferramentas internas para marcar `needs_review` / `inactive` com fluxo definido.
- Testes de acessibilidade com ferramentas automatizadas + revisão manual mais ampla.

### 3.3 Explicitamente fora do MVP

- Cadastro público de empresas por autoatendimento.
- Múltiplos usuários autenticados.
- Banco de dados compartilhado (Postgres, D1 etc.) para escrita multiusuário.
- Prospecção privada persistente online.
- Scraping em massa de diretórios.
- Pontuação automática de “quem precisa de software”.
- Aplicativo nativo móvel.

**Motivo**: todos ampliam escopo, complexidade de segurança e exigências de LGPD sem benefício proporcional na primeira fase.

---

## 4. Pesquisa técnica (fontes e fatos principais)

**Data da pesquisa:** 21/10/2026.  
**Alguns fatos importantes (fontes oficiais):**

- **Astro**
  - Usa **file-based routing** em `src/pages` para gerar URLs. 
  - Trate arquivos `.astro`, `.md` etc. em `src/pages` como páginas completas. 
  - Adota arquitetura de **ilhas** (partial/selective hydration) para interatividade local sem transformar tudo em SPA pesada. 
  - **Content collections** permitem organizar dados JSON/Markdown com tipagem e validação de esquema em build. 

- **Cloudflare**
  - **DNS**: Cloudflare atua como DNS autoritativo após troca de nameservers no registrador; seus registros DNS para subdomínios (como `portfolio.israelreispereira.com.br`) são geridos na Cloudflare. 
  - **Pages**:
    - Deploy por GitHub/GitLab com builds automáticos. 
    - Requests a **assets estáticos** são “free and unlimited” no plano gratuito; funções (Pages Functions) contam como Workers requests. 
    - Limites de projetos/pages no Free são documentados (mas muito acima das necessidades do MVP). 
  - **Workers**:
    - 100k requisições/dia e 10 ms de CPU por requisição no plano Free; tarifação de US$0,30/milhão de requisições no plano Standard. 
    - Requests a assets estáticos servidos via Workers Sites/Pages Functions são gratuitos; apenas execuções de função contam para o limite. 

- **Astro + Cloudflare**
  - O adapter `@astrojs/cloudflare` é voltado ao runtime do Workers (SSR/on-demand), não é necessário (nem hoje suportado) para deploy estático em Pages. 
  - Guia recente de Astro + Cloudflare recomenda Workers para novos projetos full-stack; para SSG puro, usar build estático tradicional. 

- **Papa Parse**: parsing de CSV strings, arquivos locais e remotos, fornecendo dados + erros + metadados. 

- **Leaflet**: biblioteca JS open-source para mapas interativos, com API clara para criar mapas e adicionar camadas/atribuições. 

- **OpenStreetMap e Nominatim**:
  - Tile server `tile.openstreetmap.org`:
    - capacidade limitada, sem SLA; exige attribution visível e caching; proíbe scraping e prefetch em massa. 
  - Nominatim:
    - taxa pública limitada (máx. 1 requisição/segundo),
    - uso principal é o search bar do openstreetmap.org, rodando em infraestrutura doada. 

- **TypeScript**: checker estático para JS, rodando antes da execução e reduzindo erros de tipos; handbook oficial orienta uso incremental. 

- **Vitest**: framework de testes unitários/integrados baseado em Vite para projetos modernos. 

- **Playwright**: framework E2E que suporta múltiplos browsers, headless/headed, com tooling para relatórios e debug. 

- **WCAG 2.2 / W3C WAI**: 13 diretrizes sob os princípios Perceptível, Operável, Compreensível, Robusto, com critérios de sucesso em níveis A/AA/AAA. 

- **LGPD / ANPD**:
  - Lei 13.709/2018 define dado pessoal como “informação relacionada a pessoa natural identificada ou identificável” e aplica-se amplamente a qualquer tratamento de dados pessoais. 
  - Guias da ANPD reforçam princípios de minimização, finalidade, transparência, segurança e direitos do titular, inclusive para agentes de pequeno porte. 

- **Fontes de dados oficiais**:
  - **Receita Federal / CNPJ**: base cadastral de pessoas jurídicas; dados abertos disponibilizados em formatos estruturados (.csv, .json etc.), porém focados em dados cadastrais, não em telefones, sites ou coordenadas detalhadas atualizadas. 
  - **SEADE – Empresas no Estado de SP**: dataset com atividade econômica, porte e natureza jurídica das empresas/MEIs por município, derivado do CNPJ; cobertura estatística por município, atualizado anualmente, com licença CC BY 4.0.   
    → Útil para entender o universo de empresas de Barretos, mas **não** é um diretório pronto com telefones ou coordenadas.

---

## 5. Comparação de tecnologias de front-end (sem favoritismo)

### 5.1 Tabela comparativa

**Contexto de comparação:** portfólio estático + diretório com filtros, cards, tabela e mapa, sem back-end no MVP, implantado em Cloudflare.

| Critério | HTML/CSS/TS puro | Astro + TS | React + Vite + TS | Vue 3 + Vite + TS | SvelteKit + TS |
|---------|------------------|-----------|--------------------|-------------------|----------------|
| **Modelo principal** | Páginas estáticas manuais + scripts soltos | SSG + islands / server islands | SPA/flexível via framework | SPA/flexível via framework | Full-stack framework |
| **Roteamento** | Manual (links + organização própria) | File-based em `src/pages`  | Exige router (ex. React Router)  | Roteamento manual ou eco-sistema | File-based em `src/routes` (Kit)  |
| **JS enviado ao cliente** | Mínimo, só o que você escreve | Zero por padrão; apenas ilhas interativas recebem JS (partial hydration)  | Runtime React + app inteiro (SPA) por padrão  | Runtime Vue + app (SPA) por padrão  | Depende do modo (SSR/SSG/SPA); tende a enviar app completo |
| **Adequação a conteúdo estático** | Ótima, mas tudo manual | Excelente: SSG, Markdown, collections  | Boa, mas exige tooling adicional de SSG/SSR | Boa, com tooling adicional | Muito boa, mas mais infra (SSR/SSG) do que o MVP precisa |
| **Adequação a filtros/UX ricos** | Possível, porém com mais “cola” manual | Ilhas reativas (pode usar React/Vue/Svelte dentro de Astro) | Forte: SPA com estado rico | Forte | Muito forte (framework full-stack) |
| **Complexidade p/ iniciante** | Baixa no começo, cresce rápido sem estrutura | Baixa–média: conceitos de páginas/layouts, mas sem SPA completa | Média–alta: hooks, estado global, roteamento, build | Média: reatividade mais simples, mas ainda eco-sistema grande | Alta: SSR, rotas + server/client boundary |
| **Integração com Cloudflare Pages** | Build estático com qualquer bundler ou nenhum | Build estático direto (sem adapter) para Pages; adapter Cloudflare para Workers SSR  | Vite build → Pages estático  | Vite build → Pages estático | Adapter estático ou adapter Cloudflare para Workers / Pages+Workers  |
| **Teste unitário com Vitest** | Integração manual com Vite ou TS | Suporte natural (Astro usa ecossistema Vite)  | Nativo (base Vite) | Nativo (base Vite) | Nativo (base Vite) |
| **Aprendizado de arquitetura** | Obliga a entender bem fundamentos, mas sem guias | Ensina SSG, layouts, conteúdo, ilhas; boa base incremental | Ensina SPA moderna, mas com muito conceito simultâneo | Similar a React | Ensina full-stack moderno, mas com bastante sobrecarga |

### 5.2 Análise crítica para este projeto

- **HTML/CSS/TS puro**
  - **Prós**: controle total, dependências mínimas, perfeito para protótipos.
  - **Contras**: organização de rotas, layouts, build, testes e deploy crescem caoticamente; reuso de componentes e SEO exigem mais esforço.
  - **Conclusão**: bom para o *protótipo HTML autocontido* (Etapa 2), mas não ideal como base final.

- **Astro + TS**
  - **Prós**:
    - File-based routing + páginas estáticas (portfólio + diretório) sem esforço extra. 
    - Islands/partial hydration: envia **apenas** JS necessário para filtros/importação. 
    - Collections de conteúdo para armazenar dados de empresas em JSON com esquema tipado. 
    - Integração natural com ecossistema Vite (Vitest, etc.).
  - **Contras**:
    - É mais uma ferramenta para aprender (arquivos `.astro`, layouts, collections).
    - Se o projeto migrar para um app ultra interativo único, frameworks de app podem ficar mais práticos.
  - **Conclusão**: melhor equilíbrio entre **conteúdo estático**, interatividade moderada e curva de aprendizado para iniciante.

- **React + Vite + TS**
  - **Prós**:
    - Excelente para interfaces complexas e SPAs ricas. 
    - Ecossistema maduro de bibliotecas.
  - **Contras**:
    - Overkill para páginas principalmente estáticas.
    - Tende a enviar mais JS, exigindo otimizações sofisticadas para igualar desempenho inicial de um SSG como Astro.
  - **Conclusão**: reservar para quando (e se) a aplicação se tornar um painel altamente dinâmico em uma única tela.

- **Vue 3 + Vite + TS**
  - **Prós**:
    - API declarativa acessível, bom equilíbrio entre simplicidade e poder. 
  - **Contras**:
    - Problema similar a React: para conteúdo estático + algumas interações, frameworks de app completam mais do que o necessário.
  - **Conclusão**: opção viável, mas não superior a Astro para o formato atual do projeto.

- **SvelteKit + TS**
  - **Prós**:
    - Framework full-stack moderno com SSR, SSG, rotas, formulários e adapters (incluindo Cloudflare). 
  - **Contras**:
    - Introduz desde já conceitos de SSR, endpoints server-side, layouts compartilhados, que não são estritamente necessários para o MVP estático.
  - **Conclusão**: forte candidato se o projeto evoluir para autenticação, APIs, back-end em D1/SQL etc., mas não é o ponto de partida mais simples.

### 5.3 Decisão

- **Decisão inicial:** usar **Astro + TS** como base do portfólio e do diretório, com build 100% estático implantado em **Cloudflare Pages**.
- **Critérios para revisar decisão (mudar de stack ou de modo de renderização):**
  - Número de telas com interatividade complexa cresce a ponto de exigir uma SPA consistente (ex.: dashboards, edição inline complexa).
  - Necessidade de SSR por motivos de SEO em conteúdo altamente dinâmico.
  - Necessidade de APIs e autenticação integradas que se beneficiem de um framework full-stack (SvelteKit, por exemplo).

---

## 6. Decisão arquitetural (MVP) e alternativas

### 6.1 Arquitetura recomendada (MVP)

- **Tipo:** Aplicação **estática** gerada por Astro (SSG) + módulos interativos no cliente.
- **Hospedagem:** Cloudflare Pages (build via Git) + DNS Cloudflare.
- **Persistência de dados públicos:**
  - Arquivos **JSON** versionados no Git, possivelmente organizados como content collections.
  - Esses arquivos representam **apenas dados revisados e aprovados para publicação**.
- **Ferramenta de importação/normalização:**
  - Rodando no **navegador**:
    - Upload de CSV → PapaParse → normalização + validação Zod → relatório → download de JSON limpo.
  - O JSON gerado deve ser **revisado manualmente** e, então, commitado no repositório para se tornar parte dos dados públicos.

**Problema que resolve:**  
Permite publicar rapidamente portfólio + diretório com boa performance e sem custo fixo de infra, mantendo controle manual sobre dados.

**Custo de adoção:**  
Aprendizado de Astro + TS + pipeline de build + testes.

**Custo de não adoção:**  
Reinventar roteamento, SEO, estrutura de páginas e build apenas com HTML/TS.

### 6.2 Alternativa 1 — Astro + Cloudflare Workers (SSR/Full-stack)

- **Descrição:** Mesmo Astro, mas com adapter `@astrojs/cloudflare` para rodar em Workers (SSR, server islands, ações, sessões). 
- **Vantagens:**
  - Permite autenticação, ações de formulário server-side, acesso a D1/KV etc.
- **Desvantagens:**
  - Introduz complexidade de código entre server/client.
  - Usa quota de Workers (100k req/dia no free), ainda suficiente, mas agora cada requisição dinâmico conta. 
- **Quando considerar:**  
  Quando o projeto precisar de:
  - prospecção privada online,
  - contas de usuário,
  - APIs ou sincronização em tempo real.

### 6.3 Alternativa 2 — SvelteKit + Cloudflare adapter

- **Descrição:** Reescrever front-end em SvelteKit com `@sveltejs/adapter-cloudflare` para Workers/Pages+Workers. 
- **Prós:**
  - Framework full-stack coeso, com rotas, formulários e endpoints.
- **Contras:**
  - Curva de aprendizado maior para iniciante.
  - Exige separar desde cedo código server/client.
- **Uso recomendado:**  
  Futuro cenário de produto mais complexo, não para MVP.

### 6.4 Alternativa 3 — SPA pura (React/Vue + Vite) em Cloudflare Pages

- **Descrição:** SPA única que consome JSON estático.
- **Prós:**
  - Simples do ponto de vista de modelo mental: “uma app JS controlando tudo”.
  - Integração natural com Vitest e Playwright.
- **Contras:**
  - Mais JS entregue, pior first load sem otimizações fortes.
  - Reimplementa layout e conteúdo estático que Astro resolve melhor.
- **Conclusão:**  
  Não recomendada para a primeira versão deste projeto específico.

---

## 7. Domínio, DNS e implantação

### 7.1 Registro.br + Cloudflare DNS

- Domínio registrado no **Registro.br** e DNS apontando para nameservers Cloudflare (já existente).
- Cloudflare atua como DNS autoritativo; criação de registros para subdomínios como `portfolio.israelreispereira.com.br` é feita no painel da Cloudflare. 

### 7.2 Subdomínio vs caminho

- **Cenário A – Dentro do portfólio (recomendado no início)**  
  - `portfolio.israelreispereira.com.br/` — home do portfólio  
  - `/projetos/mapa-empresas-barretos` — diretório
- **Cenário B – Subdomínio separado (futuro)**  
  - `empresas.israelreispereira.com.br` apontando para outro projeto (Pages ou Workers).

Começar com **Cenário A** reduz overhead de DNS e implantação. Migrar depois, se necessário, é apenas criar um novo projeto Cloudflare e ajustar rotas.

### 7.3 Cloudflare Pages x Cloudflare Workers

| Aspecto | Cloudflare Pages | Cloudflare Workers |
|--------|------------------|--------------------|
| Modelo | Hosting de sites estáticos + Functions opcionais | Funções serverless no edge (SSR, APIs, etc.) |
| Git integration | Deploy automático por commit (GitHub/GitLab)  | Workers Builds também suporta Git, mas com foco em scripts Workers.  |
| Custo estático | Requests de assets estáticos: gratuitos e ilimitados no Free  | Não é plataforma de hosting estático puro, mas pode servir assets via Workers Sites |
| Custo de função | Pages Functions tarifadas como Workers requests, com cota de 100k req/dia no Free  | 100k req/dia Free; US$0,30/milhão no plano Standard; 10 ms CPU/request no Free  |
| Adaptação Astro | SSG: sem adapter, build estático e deploy em Pages  | SSR: usar `@astrojs/cloudflare` para Workers; adapter não suporta mais Pages diretamente  |

**MVP:**  
- Astro em modo SSG → build gerado → implantado em Cloudflare Pages via Git.  
- Nenhuma Pages Function / Worker necessário.

---

## 8. Arquitetura do repositório

Estrutura proposta (adaptável):

```text
portfolio-barretos/
├── public/                  # Assets estáticos públicos (favicon, imagens genéricas)
│   ├── favicon.svg
│   └── images/
├── src/
│   ├── components/          # Componentes de UI (sem lógica de negócio complexa)
│   │   ├── SiteHeader.astro
│   │   ├── SiteFooter.astro
│   │   ├── BusinessCard.astro
│   │   ├── BusinessFilters.astro
│   │   ├── BusinessTable.astro
│   │   └── ImportStatus.astro
│   ├── content/             # Conteúdo do portfólio (Markdown/collections)
│   │   └── projects/
│   ├── data/                # JSONs públicos de empresas (após importação)
│   │   ├── businesses.sample.json
│   │   └── categories.json
│   ├── layouts/             # Layouts compartilhados
│   │   └── BaseLayout.astro
│   ├── lib/                 # Regras de negócio / utilitários sem UI
│   │   ├── business-schema.ts
│   │   ├── normalize-business.ts
│   │   ├── filter-businesses.ts
│   │   ├── csv-import.ts
│   │   └── errors.ts
│   ├── pages/               # Rotas públicas
│   │   ├── index.astro
│   │   └── projetos/
│   │       ├── index.astro
│   │       └── mapa-empresas-barretos.astro
│   └── styles/
│       └── global.css
├── tests/
│   ├── unit/                # Vitest (regras de negócio, validação, filtros)
│   └── e2e/                 # Playwright (fluxos reais no navegador)
├── docs/                    # Documentação do projeto
│   ├── ARCHITECTURE.md
│   ├── DATA-DICTIONARY.md
│   └── DEPLOYMENT.md
├── astro.config.mjs
├── package.json
├── tsconfig.json
└── README.md
```

**Principais regras:**

- **`src/lib` não deve importar componentes de UI.**
  - Aqui ficam: esquemas Zod, funções de normalização/validação, lógica de deduplicação, filtros.
- **Componentes de UI (`src/components`)** recebem dados já validados e normalizados; não sabem de parsing CSV.
- **`src/data`** contém apenas dados aprovados para publicação (sem notas privadas).
- **`tests`**:
  - `unit`: funções de `src/lib`.
  - `e2e`: cenários reais no browser (build dev/preview).
- **`docs`** registra decisões e contratos de dados (necessário para portfólio).

---

## 9. Modelo de dados

### 9.1 Entidade `Business` (estabelecimento público)

Campos (contrato lógico):

| Campo | Tipo (conceitual) | Obrigatório | Significado |
|-------|-------------------|------------|-------------|
| `id` | string | Sim | Identificador interno estável (não depende de posição na planilha) |
| `name` | string | Sim | Nome público do estabelecimento |
| `categoryIds` | string[] | Sim | Uma ou mais categorias (referem-se a `Category.id`) |
| `description` | string \| null | Não | Descrição pública revisada |
| `address` | objeto \| null | Não | Endereço estruturado (rua, número, bairro, CEP opcional) |
| `phone` | string \| null | Não | Telefone de contato verificado (com DDD) |
| `websiteUrl` | string (URL) \| null | Não | Site oficial confirmado (ou `null` se **desconhecido**) |
| `socialLinks` | objeto/lista \| null | Não | URLs de redes sociais (Facebook, Instagram, etc.) |
| `coordinates` | { lat: number; lng: number } \| null | Não | Coordenadas válidas (lat ∈ [-90,90], lng ∈ [-180,180]) |
| `sourceIds` | string[] | Sim | IDs de `Source` que contribuíram com dados |
| `verificationStatus` | enum | Sim | `unverified` \| `verified` \| `needs_review` \| `inactive` |
| `lastVerifiedAt` | ISO date string \| null | Não | Última data de verificação ativa |
| `createdAt` | ISO date string | Sim | Data de inclusão no diretório |
| `updatedAt` | ISO date string | Sim | Última atualização de qualquer campo |

**Regra importante:**  
- `websiteUrl: null` = **“não informado/desconhecido”**, **não** “não possui site”.

### 9.2 `Category`

- `id: string`
- `name: string` (ex.: “Alimentação”)
- `slug: string` (ex.: `alimentacao`)
- `description: string | null`
- `parentId: string | null` (para categorias agregadas, se necessário)

Evitar taxonomia complexa antes de entender a distribuição de negócios em Barretos.

### 9.3 `Source` (procedência)

- `id: string`
- `name: string` (ex. “Planilha de teste”, “SEADE 2025”)
- `sourceUrl: string | null`
- `sourceType: enum` (ex.: `manual`, `csv_oficial`, `site_oficial`, `dados_abertos`)
- `license: string | null` (ex.: “CC BY 4.0” para SEADE) 
- `collectedAt: ISO date string`
- `notes: string | null`

Futuro: para granularidade maior, permitir procedência por campo, se necessário.

### 9.4 `ImportJob` (histórico técnico – futuro)

No MVP, histórico pode ser apenas em memória/console. Conceitualmente:

- `id: string`
- `filename: string`
- `startedAt / completedAt: ISO date`
- `status: enum` (`pending`, `analyzed`, `applied`, `failed`, `canceled`)
- `totalRows: number`
- `acceptedRows: number`
- `rejectedRows: number`
- `duplicateRows: number`
- `warningsCount: number`
- `errors: { line: number | null; code: string; message: string }[]`

### 9.5 `ProspectingRecord` (APENAS camada privada futura)

- `businessId: string`
- `reviewStatus: enum` (`todo`, `in_progress`, `contacted`, `closed`)
- `opportunityTypes: string[]` (ex.: `["site", "agendamento_online"]`)
- `priority: enum` (`low`, `medium`, `high`)
- `notes: string`
- `lastReviewedAt: ISO date string`

**Nunca** deve ser salvo em JSON público ou enviado para o front-end público.  
Quando (e se) for implementado, exigirá:

- back-end (Workers/D1 ou outro),
- autenticação/autorização,
- avaliação LGPD formal.

---

## 10. Importação, validação e normalização

### 10.1 Ordem de prioridade (MVP)

1. **CSV local → preview no navegador → download JSON normalizado** (já no MVP).
2. Importação manual de JSON (carregar dados de teste direto de `src/data/*.json`).
3. APIs externas / dados oficiais (após consolidar modelo e fluxo).

### 10.2 Fluxo detalhado (MVP, no cliente)

1. Usuário (você, como mantenedor, ou visitante avançado) seleciona um CSV.
2. **Papa Parse** faz parsing do arquivo:
   - lida com separadores, aspas, quebras de linha; retorna dados + lista de erros sintáticos. 
3. Conversão linha a linha em objetos brutos.
4. **Normalização**:
   - trim de espaços,
   - padronização de maiúsculas/minúsculas onde fizer sentido,
   - conversão de valores vazios em `null`.
5. **Validação (Zod)**:
   - campos obrigatórios (`name`, pelo menos uma categoria, etc.),
   - formatos (URLs, telefones, coordenadas).
6. **Classificação**:
   - `accepted` (dados válidos),
   - `rejected` (erros graves),
   - `needs_review` (avisos de qualidade),
   - `duplicate_candidates` (potenciais duplicatas).
7. **Relatório de importação** (na interface):
   - total analisado,
   - contagens por status,
   - exemplos de mensagens de erro/aviso.
8. **Ação final**:
   - opção de baixar JSON apenas com registros aceitos (e, opcionalmente, os pendentes marcados).
   - cabe a você revisar e commitar esse JSON em `src/data/`.

### 10.3 Regras obrigatórias

- Não ignorar erros silenciosamente.
- Não descartar registros inválidos sem explicar o motivo.
- Não sobrescrever JSON de produção diretamente via importação em produção (processo é offline: gerar JSON → revisar → commit).
- Diferenciar:
  - erro de parsing (CSV corrompido),
  - erro de validação (campo obrigatório ausente, coordenadas inválidas),
  - aviso de qualidade (campo suspeito, mas não bloqueante),
  - possível duplicata.

### 10.4 Mensagens de erro sugeridas

- “Não conseguimos interpretar o arquivo. Confira o separador, o cabeçalho e as aspas.”
- “Linha 12: o campo ‘nome’ está vazio.”
- “Linha 27: coordenadas fora do intervalo permitido; o registro não aparecerá no mapa.”
- “Encontramos 8 possíveis duplicatas. Revise os registros antes de confirmar a importação.”
- “Importação analisada: 42 registros aceitos, 5 para revisão e 3 rejeitados.”

---

## 11. Fontes de dados de Barretos-SP

### 11.1 Fase A — Conjunto de teste controlado (MVP)

- Criar **20–50 registros**:
  - Alguns fictícios,
  - Alguns reais, verificados manualmente (site oficial, contato).
- Marcar no dataset:
  - se o registro é fictício ou real,
  - nível de verificação (`unverified`, `verified` etc.).

### 11.2 Fase B — Fontes estruturadas (RFB / SEADE)

- **SEADE – “Empresas no Estado de SP”**:
  - Dados derivados do CNPJ, com atividade, porte, natureza jurídica, por município. 
  - Licença CC BY 4.0 → uso permitido com atribuição.
  - Focado em estatística; não garante telefone ou site atualizado.
- **CNPJ (Receita Federal)**:
  - Base cadastral, com layout público para dados não protegidos por sigilo fiscal. 
  - Pensado para consumo governamental; exige muito tratamento de dados.
- **Estratégia**:
  - Usar inicialmente para entender **ordem de grandeza** de empresas de Barretos (tipos, portes), não para encher diretório automaticamente.
  - Qualquer uso de CNPJ para listagem pública exige:
    - verificar se dados são de fato “não protegidos por sigilo”,
    - respeitar licenças e orientações da Receita/ANPD.

### 11.3 Fase C — Complementação (sites e dados públicos específicos)

- Usar sites oficiais de estabelecimentos:
  - para confirmar telefone, site, tipo de serviço.
- Manter `Source` adequado indicando origem de cada dado.

### 11.4 Fase D — Verificação

- Definir claramente:
  - `unverified`: importado de fonte bruta, não revisado manualmente.
  - `verified`: conferido manualmente (data máxima, ex. 12 meses).
  - `needs_review`: suspeita de desatualização.
  - `inactive`: empresa aparentemente encerrada/mudou.

---

## 12. Geolocalização e mapa

### 12.1 Critérios para introduzir o mapa

- Pelo menos **algumas dezenas** de registros com coordenadas **confiáveis**.
- Documentação da procedência das coordenadas (Nominatim, dados oficiais, coleta manual, etc.).
- Implementação de fallback (lista/tabela) funcionando bem.

### 12.2 Uso do Leaflet + OpenStreetMap

- Leaflet é apenas a **lib de visualização** (mapa, camadas, eventos). 
- Servidor de tiles padrão `tile.openstreetmap.org`:
  - uso limitado, sem SLA,
  - exige atribuição “© OpenStreetMap contributors” visível, caching e identificação de User-Agent. 
  - é proibido scraping/prefetch massivo.

### 12.3 Nominatim (geocodificação) – se usado

- API pública de Nominatim é limitada a usos leves (máx. 1 req/s), sem SLA. 
- Não deve ser usada para geocodificar toda a cidade de uma vez nem a cada visita.
- Se usada:
  - cachear resultados em dataset local (JSON) respeitando licenças,
  - usar off-line na ferramenta de importação, não durante navegação normal dos usuários.

### 12.4 Requisitos mínimos do mapa

- Coordenadas válidas, com origem conhecida.
- Sincronização com filtros: o mapa mostra apenas o subconjunto filtrado.
- Indicação clara quando:
  - um registro não tiver coordenadas,
  - o mapa não puder ser carregado (mensagem + fallback de lista).

---

## 13. Privacidade, segurança e separação de dados

### 13.1 Separação de camadas de dados

- **Dados públicos**:
  - `Business`, `Category`, `Source`, sem anotações internas.
  - Versionados em Git, servidos via JSON estático.
- **Dados técnicos internos**:
  - `ImportJob`, logs de erro, etc. — usados apenas em desenvolvimento; podem não ser persistidos no MVP.
- **Dados de prospecção privada**:
  - `ProspectingRecord` e similares — **NÃO** vão para arquivos JSON estáticos nem para front-end público.

### 13.2 Por que JSON no front-end não é “privado”

- Qualquer arquivo JSON publicado em `src/data` e servido em Pages é baixável por qualquer usuário.
- “Ocultar coluna” na UI ou “senha em JS” não protegem dados — entram em conflito direto com as exigências da LGPD e com boas práticas de segurança. 

### 13.3 LGPD (linha geral)

- Não coletar dados pessoais desnecessários.
  - Nome de pessoa física, telefones pessoais, e-mail pessoal → só se houver motivo legal e se isso for parte de uma relação com o titular.
- Documentar:
  - finalidade do tratamento,
  - base legal (legítimo interesse, consentimento, etc.),
  - canal para contato do titular (mesmo que simples).
- Como o MVP se restringe em grande parte a dados de CNPJ/estabelecimento comercial, risco é moderado, mas:
  - ainda assim há titulares (ex.: MEI com nome da pessoa).

---

## 14. Design, acessibilidade e UX

### 14.1 Direção visual

- Fundo branco ou cinza muito claro.
- Texto em cinza escuro (grafite) com **uma cor de destaque** (links, botões).
- Tipografia sem serifa, tamanhos e espaçamentos constantes.
- Componentes:
  - Header simples com navegação clara.
  - Cards com:
    - nome,
    - categoria(s),
    - bairro,
    - estado de verificação,
    - links de contato.
  - Tabela legível com cabeçalhos claros, sem overflow horizontal em mobile (usar flex/responsivo ou colunas prioritárias).

### 14.2 Acessibilidade (WCAG 2.2 AA – critérios principais)

- Teclado:
  - toda funcionalidade acionável por teclado; foco visível sempre.
- Hierarquia:
  - `<h1>` único por página, seguido por `<h2>`, `<h3>` lógicos.
- Formularios:
  - `label` associado a campos,
  - mensagens de erro claras, não só cor.
- Contraste:
  - cumprir contraste mínimo recomendado (4.5:1 na maioria dos casos). 
- Conteúdo dinâmico:
  - mudanças significativas (ex.: “nenhum resultado”) devem ser perceptíveis a leitores de tela (por exemplo, área com `aria-live`).
- Mapa:
  - não ser a **única** forma de obter informação; lista/tabela devem conter os mesmos dados relevantes.

---

## 15. Testes, desempenho e depuração

### 15.1 Testes unitários (Vitest)

Cobrir, no mínimo:

- Normalização de campos (`normalize-business`).
- Validação de:
  - categorias existentes,
  - URLs,
  - coordenadas,
  - campos obrigatórios.
- Deduplicação (regras de similaridade).
- Filtros combinados (busca + categoria + status).
- Consistência de contagens (aceitos, rejeitados, pendentes).

### 15.2 Testes de integração

- Importar CSV de exemplo:
  - verificar conversão para o modelo `Business`,
  - conferir relatório de importação (contagens batendo com dados brutos),
  - garantir que falhas em linhas individuais **não quebram todo arquivo**.

### 15.3 Testes E2E (Playwright)

Fluxos:

- Abrir diretório.
- Fazer busca por nome.
- Aplicar filtros combinados.
- Limpar filtros.
- Alternar cards ↔ tabela.
- Importar CSV válido (em ambiente de desenvolvimento).
- Tentar importar CSV inválido (cabeçalho ou tipos errados) e verificar mensagens.
- Usar aplicação quando o mapa não carrega (simular falha de rede para tiles).

### 15.4 Desempenho

- Medições:
  - tamanho total de HTML, CSS, JS na primeira carga,
  - tempo até conteúdo principal visível em mobile,
  - tempo para aplicar filtros em listas maiores (ex.: 1000 registros, em ambiente de teste).
- Ferramentas:
  - DevTools dos navegadores (Network, Performance),
  - Lighthouse ou similares (sem necessidade de citar doc específico).

### 15.5 Regras de depuração

- Nenhum `catch` vazio.
- Não substituir dados válidos sem confirmação.
- Logs de desenvolvimento com contexto (operação, linha de CSV, etc.), removidos/minimizados em produção.
- Stack traces nunca exibidos para o visitante; mensagens de erro amigáveis.

---

## 16. Plano de execução incremental (para desenvolvedor iniciante)

### Etapa 1 — Planejamento e requisitos

- **Objetivo:** consolidar escopo, modelo de dados e critérios.
- **Tarefas:**
  - Criar `docs/ARCHITECTURE.md` e `docs/DATA-DICTIONARY.md` com resumo desta especificação.
  - Definir campos mínimos de `Business`, `Category`, `Source`.
  - Listar estados de verificação.
- **Entrega:** documentos no repositório.
- **Critério de aceite:** nenhuma dúvida crítica sobre o que cada campo significa.

### Etapa 2 — Protótipo HTML autocontido

- **Objetivo:** validar UX/fluxos sem Astro.
- **Tarefas:**
  - Criar `preview.html` com:
    - barra de busca,
    - filtros básicos,
    - cards + tabela sincronizadas (pelo menos com dados estáticos embutidos),
    - mensagens de “nenhum resultado”.
- **Entrega:** arquivo HTML estático testável localmente.
- **Critério de aceite:** alguém consegue usar o protótipo em mobile para encontrar um estabelecimento fictício.

### Etapa 3 — Projeto Astro básico

- **Objetivo:** migrar protótipo para arquitetura final.
- **Tarefas:**
  - Iniciar projeto Astro + TS.
  - Implementar páginas:
    - `/` (portfólio),
    - `/projetos`,
    - `/projetos/mapa-empresas-barretos`.
  - Migrar layout e componentes.
  - Carregar JSON de `src/data` e exibir lista + filtros.
- **Entrega:** app rodando em `npm run dev`.
- **Critério de aceite:** funcionalidade mínima de busca + filtros espelha o protótipo.

### Etapa 4 — Importador CSV

- **Objetivo:** demonstrar pipeline de dados.
- **Tarefas:**
  - Implementar função `csv-import.ts` com Papa Parse + Zod.
  - Criar UI simples de upload + relatório (pode ser página separada).
  - Implementar download de JSON normalizado.
- **Entrega:** ferramenta interna de importação com relatório.
- **Critério de aceite:** CSV de exemplo resulta em JSON conforme modelo e relatório coerente.

### Etapa 5 — Geolocalização (opcional no MVP inicial, mas previsto)

- **Objetivo:** integrar mapa com subset de dados.
- **Tarefas:**
  - Adicionar Leaflet e camada de tiles OSM com atribuição correta. 
  - Plotar apenas registros com `coordinates` válidas.
  - Sincronizar com filtros.
  - Tratar falhas de carregamento.
- **Entrega:** visualização de mapa funcional.
- **Critério de aceite:** mapa não quebra app; lista continua utilizável quando há erro.

### Etapa 6 — Testes, acessibilidade e publicação

- **Objetivo:** consolidar qualidade e publicar.
- **Tarefas:**
  - Configurar Vitest e criar testes unitários básicos.
  - Configurar Playwright com 2–3 cenários críticos.
  - Revisar contraste, foco e navegação por teclado.
  - Conectar projeto ao Cloudflare Pages, configurar subdomínio.
- **Entrega:** site público em `portfolio.israelreispereira.com.br` com diretório acessível.
- **Critério de aceite:** checklist de publicação (seção 17) atendido para itens bloqueantes.

---

## 17. Checklist de publicação (resumido, com bloqueadores)

### A. Requisitos e arquitetura

- [ ] Escopo do MVP documentado e separado de funcionalidades futuras. **(Bloqueador)**
- [ ] Dicionário de dados com tipos e validações. **(Bloqueador)**
- [ ] Principais decisões arquiteturais registradas.

### B. Importação e qualidade dos dados

- [ ] CSV com acentos/aspas/quebras testado e tratado.
- [ ] Arquivos vazios/corrompidos/cabeçalhos inválidos tratados com mensagem clara.
- [ ] Campos obrigatórios e tipos validados. **(Bloqueador)**
- [ ] Duplicatas identificadas sem exclusão automática.
- [ ] Prévia de importação com contagens consistentes.
- [ ] Importação inválida não destrói dados já publicados. **(Bloqueador)**

### C. Interface e acessibilidade

- [ ] Busca e filtros combináveis e “limpáveis”.
- [ ] Cards e tabela exibem o mesmo conjunto.
- [ ] Layout funciona em celular, tablet e desktop.
- [ ] Estados de carregamento/vazio/erro claros.
- [ ] Navegação por teclado com foco visível. **(Bloqueador)**
- [ ] Mapa não é único meio de acessar informações.

### D. Segurança, privacidade e conteúdo

- [ ] Nenhuma chave secreta/credencial no código público. **(Bloqueador)**
- [ ] Nenhuma nota de prospecção privada em JSON público. **(Bloqueador)**
- [ ] Fontes e licenças dos dados documentadas.
- [ ] Avaliação mínima de LGPD para dados pessoais.

### E. Testes e desempenho

- [ ] Testes unitários das funções críticas passam.
- [ ] Pelo menos 2 cenários E2E passam sem erro.
- [ ] Sem erros JavaScript inesperados em fluxo comum.
- [ ] Tamanho de JS inicial revisado e aceitável (ordem de poucos dezenas de KB, não MB).

### F. Publicação e operação

- [ ] Build de produção sem erros. **(Bloqueador)**
- [ ] Deploy de teste validado antes de apontar subdomínio. **(Bloqueador)**
- [ ] Subdomínio configurado no Cloudflare Pages e DNS. **(Bloqueador)**
- [ ] HTTPS verificado.
- [ ] Página 404 funcional.
- [ ] Procedimento simples de rollback documentado (voltar para commit anterior).

---

## 18. Matriz de riscos (exemplos principais)

| Risco | Prob. | Impacto | Sinais de alerta | Medida preventiva | Plano de resposta |
|-------|-------|---------|------------------|-------------------|-------------------|
| Escopo grande demais para iniciante | Alta | Alto | backlog cresce sem entregas | Limitar MVP; etapas pequenas | Congelar escopo, focar em publicação da primeira versão |
| Stack inadequada (migração precoce) | Média | Médio | tentativa de reescrever em outro framework antes de publicar | Documentar critérios de revisão de stack | Adiar migração até uso real evidenciar necessidade |
| Dados empresariais desatualizados | Alta | Médio | muitos registros `unverified` antigos | Estados de verificação claros, datas de coleta | Marcar registros como `needs_review` e comunicar limitação |
| Uso indevido de tiles OSM/Nominatim | Baixa–Média | Médio–Alto | chamadas frequentes, sem caching | Seguir políticas oficiais; cache; mapa opcional  | Desligar mapa temporariamente ou mudar provedor |
| Exposição de dados privados (prospecção) | Média | Alto | campos internos em JSON público | Não implementar prospecção no MVP; revisão manual de dados | Remover imediatamente dados expostos; comunicar, se necessário |
| Importação corromper dados válidos | Baixa (no modelo atual) | Alto | pipeline de importação escreve direto em produção | Manter fluxo offline (JSON via download + commit) | Reverter para commit anterior; corrigir script |
| Desempenho ruim em mobile | Média | Médio | cargas de JS muito grandes, travamentos | Usar Astro com islands, medição contínua | Otimizar, dividir bundles, simplificar UI |

---

## 19. Decisões pendentes

- Lista inicial de categorias (`Category`) para Barretos (começar com poucas genéricas).
- Critérios quantitativos para “introduzir o mapa” (por ex.: “≥ 30 empresas com coordenadas verificadas”).
- Política de atualização de registros (quanto tempo até um registro `verified` virar `needs_review`).
- Se o módulo de importação ficará acessível publicamente ou apenas em rota/documentação para demonstração técnica.

---

## 20. Próxima ação recomendada (para você agora)

1. **Criar o repositório Git local** e adicionar esta especificação em `docs/ARCHITECTURE.md`.
2. **Implementar o protótipo HTML simples (`preview.html`)** com:
   - alguns cards estáticos,
   - busca e filtro de categoria funcionando,
   - estados de “nenhum resultado”.
3. Só depois de estar satisfeito com a navegação:
   - inicializar o projeto Astro,
   - migrar o protótipo para as páginas Astro,
   - e então começar a implementar o módulo de importação CSV conforme o modelo.

Esse caminho minimiza risco, permite aprendizado incremental e produz rapidamente algo demonstrável no portfólio sem comprometer segurança, privacidade e evolução futura.