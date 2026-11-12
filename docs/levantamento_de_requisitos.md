Para estruturar completamente o conteúdo da pasta **`PROJETO/`** e garantir a execução segura e incremental do primeiro MVP do **Guia Comercial de Barretos**, aqui está o levantamento detalhado das **informações que faltam ser preenchidas** nos documentos/arquivos e **o que você deve pesquisar** para supri-las.

---

### 1. Informações que faltam preencher na pasta `PROJETO/`

* **Dataset de Demonstração e Curadoria Local (`src/data/` e arquivos de dados)**:
  * **Lista Inicial de Estabelecimentos (20 a 50 registros)**: Falta definir a relação inicial de empresas para testes e validação, distinguindo claramente quais registros são fictícios e quais são reais verificados.
  * **Taxonomia de Categorias e Subcategorias**: Definição da lista inicial de categorias adaptada à realidade de Barretos (ex.: *Alimentação, Saúde, Beleza, Serviços Profissionais, Comércio, Agro/Serviços Rurais*).
* **Mapeamento Geográfico de Barretos-SP (`docs/DATA-DICTIONARY.md` e filtros)**:
  * **Regiões e Bairros**: Faltam as regras de agrupamento dos bairros em regiões editoriais do portal (ex.: agrupar bairros sob *Centro*, *Zona Norte*, *Zona Sul*, etc.) para alimentar os filtros combinados.
* **Contratos de Dados e Esquemas Zod/TypeScript (`docs/ARCHITECTURE.md` e `.agents/skills/`)**:
  * **Regras de Nulos e Opcionais**: Especificação rigorosa de distinção entre valores desconhecidos e valores negativos (ex.: `websiteUrl: null` significa *"não informado/desconhecido"*, e não *"não possui site"*).
  * **Estados de Verificação**: Mapeamento dos estados dos registros (`unverified`, `verified`, `needs_review`, `inactive`) e definição das datas de validade da verificação.
* **Variáveis de Ambiente e Arquivos de Infraestrutura (`.env.example` e `docs/INFRASTRUCTURE.md`)**:
  * Definição das chaves/variáveis para o build estático do Astro no **Cloudflare Pages** e regras de rotas protegidas (como o Cloudflare Access para o upload privado de CSV, caso aplicado).
* **Documentação de Privacidade e Conformidade Legal (`docs/SECURITY.md`)**:
  * **Avaliação de LGPD (Lei 13.709/2018)**: Mapeamento de quais dados cadastrais de pessoas físicas (ex.: MEI com nome civil no CNPJ ou telefones pessoais) exigem atenção, canal de contato para titulares e termos de procedência das fontes públicos.

---

### 2. O que pesquisar para suprir essa falta de informações (para o MVP)

#### A. Obtenção e Validação dos Dados das Empresas
* **Dados Abertos do CNPJ (Receita Federal)**:
  * **O que pesquisar**: Baixar os arquivos de dados abertos do cadastro de pessoas jurídicas da Receita Federal e filtrar pelo **código oficial do município de Barretos-SP** e situação cadastral **ativa**.
  * **O que extrair**: CNPJ, Razão Social, Nome Fantasia, CNAE principal/secundário, Endereço cadastral e CEP.
* **SEADE (Empresas no Estado de São Paulo)**:
  * **O que pesquisar**: O repositório de dados abertos do SEADE (licença CC BY 4.0) para mapear a distribuição econômica e porte das empresas em Barretos-SP para validar as categorias do catálogo.
* **Verificação Comercial Direta (Complementação Manual)**:
  * **O que pesquisar**: Canais oficiais públicos das empresas (sites, telefones comerciais e WhatsApp de atendimento) para confirmar que o estabelecimento está efetivamente em operação.

#### B. Definição Geográfica e Cartográfica
* **Divisão de Bairros de Barretos**:
  * **O que pesquisar**: A lista oficial ou mapeamento público dos bairros da cidade para padronizar a grafia e criar os agrupamentos por região.
* **Geolocalização (OpenStreetMap / Nominatim)**:
  * **O que pesquisar**: Obter coordenadas (latitude e longitude) confiáveis apenas para o subconjunto de estabelecimentos que aparecerão no mapa.
  * **Políticas de uso**: Pesquisar as políticas de limites do servidor de tiles do OpenStreetMap e regras do Nominatim (máx. 1 req/s, exigência de cache e User-Agent) para garantir consumo offline/pré-processado na etapa de importação.

#### C. Políticas de Licenças e Privacidade
* **Licenças das Fontes**: Conferir os termos e atribuições exigidas pelas bases governamentais (Receita Federal e SEADE).
* **Diretrizes da ANPD (LGPD)**: Revisar os guias de minimização de dados e transparência para garantir que nenhuma anotação privada ou dado pessoal desnecessário seja incluído no JSON estático do projeto.

---
