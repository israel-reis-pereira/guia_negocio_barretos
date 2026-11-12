# Guia Comercial de Barretos — Levantamento para o MVP

Este documento consolida os pontos pendentes do projeto e as fontes oficiais necessárias para preenchê-los. A recomendação central é iniciar com um catálogo **somente leitura**, alimentado por dados autorizados ou verificados, com painel administrativo restrito a você.

## 1. Dataset inicial e curadoria

Falta definir uma base inicial de **20 a 50 estabelecimentos**, separando registros de demonstração dos registros reais já validados. Para o MVP, recomendo começar com 30 empresas reais e 10 fictícias de teste, todas marcadas com um campo `origin` e `verificationStatus`.

| Campo | Finalidade |
|---|---|
| `id` | Identificador interno único |
| `slug` | URL amigável, como `padaria-exemplo-barretos` |
| `name` | Nome comercial |
| `legalName` | Razão social, opcional |
| `cnpj` | Apenas se for público e necessário |
| `category` | Categoria principal |
| `subcategory` | Subcategoria principal |
| `neighborhood` | Bairro |
| `address` | Endereço público |
| `phone` | Telefone comercial |
| `whatsapp` | WhatsApp comercial |
| `website` | Site oficial |
| `instagram` | Perfil público |
| `priceRange` | Faixa de preço |
| `imageUrl` | Uma imagem principal |
| `description` | Descrição curta |
| `status` | Estado editorial |
| `verifiedAt` | Data da última verificação |
| `source` | Origem do dado |
| `placeId` | Identificador do Google, se usado |

### Regras de dados

- `null`: campo ainda não informado ou desconhecido.
- `""`: campo existe, mas está vazio.
- `false`: confirmação negativa, por exemplo, “não possui site”.
- `unverified`: registro importado, mas não conferido.
- `verified`: dados conferidos manualmente ou autorizados pelo estabelecimento.
- `needs_review`: dado incompleto, conflitante ou suspeito.
- `inactive`: empresa encerrada, fora de operação ou removida a pedido.

A Receita Federal disponibiliza dados abertos do CNPJ em arquivos estruturados, com layout documentado e separador ponto e vírgula, adequados para importação e filtragem por município. [gov](https://www.gov.br/receitafederal/dados/cnpj-metadados.pdf/@@download/file)

## 2. Taxonomia de categorias

Use uma taxonomia de dois níveis, com **uma categoria principal** e **uma subcategoria** por empresa. Categorias secundárias podem existir apenas como tags, para não fragmentar a busca.

### Categorias iniciais

| Categoria | Subcategorias |
|---|---|
| **Alimentação e Bebidas** | Restaurantes; Lanchonetes; Pizzarias; Churrascarias; Cafeterias; Padarias; Sorveterias; Açaí; Delivery; Comércio de alimentos |
| **Saúde** | Clínicas médicas; Odontologia; Farmácias; Óticas; Laboratórios; Fisioterapia; Psicologia; Nutrição; Veterinários |
| **Beleza e Bem-estar** | Cabeleireiros; Barbearias; Manicure; Estética; Depilação; Maquiagem; Spa; Academias; Pilates; Dança |
| **Comércio** | Supermercados; Hortifrúti; Açougues; Bebidas; Moda; Calçados; Eletrônicos; Móveis; Pet shops; Presentes |
| **Automotivo** | Concessionárias; Oficinas; Funilaria; Pneus; Autopeças; Estética automotiva; Guincho; Despachante |
| **Construção e Reformas** | Construtoras; Alvenaria; Pintura; Elétrica; Hidráulica; Marcenaria; Serralheria; Vidraçaria; Ar-condicionado |
| **Serviços Profissionais** | Advocacia; Contabilidade; Consultoria; Engenharia; Marketing; TI; Design; RH; Gráfica |
| **Finanças e Seguros** | Bancos; Cooperativas; Correspondentes; Seguros; Crédito; Investimentos; Lotéricas |
| **Imóveis** | Imobiliárias; Corretores; Administração de locações; Loteadoras; Mudanças; Manutenção predial |
| **Educação** | Escolas; Cursos técnicos; Idiomas; Reforço escolar; Música; Informática; Capacitação |
| **Eventos e Lazer** | Buffets; Salões; Fotografia; Decoração; Som; DJs; Cinema; Turismo; Bares |
| **Agro e Rural** | Pecuária; Agricultura; Cana-de-açúcar; Insumos; Máquinas; Veterinária rural; Consultoria agronômica |
| **Indústria e Produção** | Alimentos; Carnes; Metalurgia; Plásticos; Embalagens; Móveis; Têxtil; Reciclagem |
| **Logística e Transporte** | Cargas; Mudanças; Entregas; Motoboy; Passageiros; Armazenagem; Distribuidoras |
| **Tecnologia** | Software; Suporte; Redes; Segurança eletrônica; Câmeras; Informática; Marketing digital |
| **Serviços Domésticos** | Limpeza; Jardinagem; Dedetização; Manutenção; Costura; Lavanderia; Pets; Funerárias |
| **Instituições** | Órgãos públicos; ONGs; Associações; Sindicatos; Igrejas; Fundações |

## 3. Bairros e regiões

Falta padronizar a lista de bairros e criar agrupamentos editoriais. Como não há uma contagem oficial consolidada de bairros de Barretos publicada pelo IBGE ou pela Prefeitura, o catálogo deve tratar bairro como **campo editorial**, não como dado geográfico oficial.

### Estrutura recomendada

```text
region
└── neighborhood
    └── business
```

| Região editorial | Critério provisório |
|---|---|
| Centro | Área central e entorno comercial |
| Zona Norte | Bairros ao norte do centro |
| Zona Sul | Bairros ao sul do centro |
| Zona Leste | Bairros a leste do centro |
| Zona Oeste | Bairros a oeste do centro |
| Distritos e área rural | Localidades rurais e distritos |

Não use “Zona Norte”, “Zona Sul” etc. como divisão oficial sem confirmação municipal. Trate-os como **agrupamentos editoriais**, criados para facilitar filtros, e documente a regra no dicionário de dados.

## 4. Modelo de dados

### Tabela `business`

```sql
CREATE TABLE businesses (
  id TEXT PRIMARY KEY,
  slug TEXT UNIQUE NOT NULL,
  name TEXT NOT NULL,
  legal_name TEXT,
  cnpj TEXT,
  category_id TEXT NOT NULL,
  subcategory_id TEXT,
  neighborhood_id TEXT,
  address TEXT,
  postal_code TEXT,
  phone TEXT,
  whatsapp TEXT,
  website_url TEXT,
  instagram_url TEXT,
  price_range TEXT,
  description TEXT,
  image_url TEXT,
  place_id TEXT,
  status TEXT NOT NULL DEFAULT 'unverified',
  source TEXT NOT NULL DEFAULT 'manual',
  verified_at TEXT,
  created_at TEXT NOT NULL,
  updated_at TEXT NOT NULL
);
```

### Tabela `categories`

```sql
CREATE TABLE categories (
  id TEXT PRIMARY KEY,
  slug TEXT UNIQUE NOT NULL,
  name TEXT NOT NULL,
  parent_id TEXT,
  sort_order INTEGER DEFAULT 0,
  is_active INTEGER DEFAULT 1
);
```

### Tabela `neighborhoods`

```sql
CREATE TABLE neighborhoods (
  id TEXT PRIMARY KEY,
  slug TEXT UNIQUE NOT NULL,
  name TEXT NOT NULL,
  region_id TEXT,
  is_active INTEGER DEFAULT 1
);
```

### Tabela `regions`

```sql
CREATE TABLE regions (
  id TEXT PRIMARY KEY,
  slug TEXT UNIQUE NOT NULL,
  name TEXT NOT NULL,
  sort_order INTEGER DEFAULT 0
);
```

## 5. Filtros combinados

A página inicial deve permitir combinar filtros sem recarregar a página inteira.

| Filtro | Tipo | Comportamento |
|---|---|---|
| Busca livre | Texto | Nome, descrição, tags e categoria |
| Categoria | Seleção única | Filtra pela categoria principal |
| Subcategoria | Seleção única | Depende da categoria escolhida |
| Bairro | Múltipla seleção | Aceita mais de um bairro |
| Região | Múltipla seleção | Expande para os bairros vinculados |
| Faixa de preço | Múltipla seleção | `$`, `$$`, `$$$`, `$$$$` |
| Status | Interno | Exibe apenas `published` ao público |
| Ordenação | Seleção única | Relevância, nome A-Z, mais recentes |

### Faixas de preço

| Valor | Significado |
|---|---|
| `$` | Econômico |
| `$$` | Moderado |
| `$$$` | Elevado |
| `$$$$` | Premium |
| `null` | Não informado |

Não use preço como dado obrigatório. Muitos serviços, clínicas, indústrias e escritórios não possuem preço público comparável.

## 6. Página inicial

A home deve priorizar descoberta rápida:

- Busca por nome, serviço ou categoria.
- Filtros de categoria, bairro, região e preço.
- Cards com uma imagem, nome, categoria, bairro e botão “Ver empresa”.
- Destaques editoriais opcionais.
- Link para “Cadastrar minha empresa” ou “Sugerir correção”.
- Rodapé com política de privacidade, fontes e contato.

Cada card deve conter apenas uma imagem para manter performance e simplicidade visual.

## 7. Página individual

A página da empresa deve conter:

- Nome comercial.
- Imagem principal.
- Categoria e subcategoria.
- Bairro e região.
- Endereço, se público.
- Telefone e WhatsApp comercial.
- Site, Instagram e redes sociais.
- Horário de funcionamento.
- Descrição.
- Faixa de preço, quando aplicável.
- Botão de rota no Google Maps.
- Aviso de última atualização.
- Botão “Sugerir correção”.

Não publique dados pessoais de sócios, CPF, documentos, endereço residencial ou telefone pessoal.

## 8. Painel administrativo

O painel deve ser privado, com acesso exclusivamente seu. A forma mais simples e gratuita é usar **Cloudflare Access** na rota `/admin`, exigindo autenticação por e-mail ou provedor de identidade.

### Funcionalidades mínimas

- Login restrito.
- Listagem de empresas com busca e filtros.
- Criação, edição, publicação, despublicação e exclusão lógica.
- Importação de CSV.
- Validação de campos obrigatórios.
- Pré-visualização antes da publicação.
- Histórico simples de alterações.
- Upload de imagem para R2.
- Geração automática de `slug`.
- Marcação de `verified`, `needs_review` e `inactive`.

### Importação de CSV

O CSV deve ter colunas padronizadas:

```csv
name,legal_name,cnpj,category,subcategory,neighborhood,address,phone,whatsapp,website,instagram,price_range,description,image_url,source,status
```

O painel deve validar:

- Nome obrigatório.
- Categoria obrigatória.
- Bairro obrigatório ou marcado como “não informado”.
- CNPJ com máscara e duplicidade.
- URL válida.
- Telefone e WhatsApp válidos.
- Slug único.
- Imagem opcional.

## 9. Formulário Google

O Google Forms é uma boa opção gratuita para coletar sugestões e cadastros iniciais. Ele pode alimentar uma planilha Google Sheets, que pode ser exportada como CSV e importada ao painel.

### Fluxo recomendado

1. Empresário preenche o formulário.
2. Você recebe os dados na planilha.
3. Você valida as informações.
4. Você exporta ou conecta a planilha ao painel.
5. O registro entra como `needs_review`.
6. Após conferência, você publica.

Não exponha a planilha publicamente. Use o Google Forms apenas como canal de entrada e mantenha o painel como fonte única de publicação.

## 10. Arquitetura gratuita

| Camada | Solução | Papel |
|---|---|---|
| Front-end | Astro | Geração de páginas estáticas e conteúdo SEO-friendly |
| Hospedagem | Cloudflare Workers/Pages | Deploy do site e APIs |
| Banco de dados | Cloudflare D1 | Cadastro de empresas, categorias, bairros e regiões |
| Arquivos | Cloudflare R2 | Imagens, CSVs e assets |
| Domínio | registro.br | Domínio `.com.br` ou `.com.br` regional |
| Painel | Astro + Workers + Cloudflare Access | CRUD restrito |
| Formulário | Google Forms | Captação inicial de cadastros |
| Mapa | OpenStreetMap/Nominatim | Geocodificação pontual e mapa |

O plano gratuito do Cloudflare Workers permite 100 mil requisições por dia, 10 ms de CPU por requisição, 50 subrequests por invocação e 64 variáveis por Worker. [developers.cloudflare](https://developers.cloudflare.com/workers/platform/limits/)

O D1 gratuito permite até 10 bancos, 5 milhões de linhas lidas por dia, 100 mil linhas escritas por dia e 5 GB de armazenamento total. [developers.cloudflare](https://developers.cloudflare.com/workers/platform/pricing/)

## 11. Variáveis de ambiente

Crie um `.env.example` com:

```env
PUBLIC_SITE_URL=https://guiacomercialbarretos.com.br
PUBLIC_SITE_NAME=Guia Comercial de Barretos
PUBLIC_CONTACT_EMAIL=contato@seudominio.com.br

CLOUDFLARE_ACCOUNT_ID=
CLOUDFLARE_API_TOKEN=
D1_DATABASE_ID=
R2_BUCKET_NAME=
R2_PUBLIC_BASE_URL=

ADMIN_EMAIL=
ADMIN_ALLOWED_EMAIL=

GOOGLE_FORM_URL=
GOOGLE_SHEETS_CSV_URL=

NOMINATIM_USER_AGENT=GuiaComercialBarretos/1.0 (contato@seudominio.com.br)
```

No Cloudflare, variáveis de texto e JSON podem ser definidas via `wrangler` ou pelo painel, e ficam disponíveis no objeto `env` do Worker. [developers.cloudflare](https://developers.cloudflare.com/workers/configuration/environment-variables/)

Segredos não devem ficar no repositório. Use `.dev.vars` localmente e o painel do Cloudflare para produção. [developers.cloudflare](https://developers.cloudflare.com/workers/static-assets/migration-guides/migrate-from-pages/)

## 12. LGPD e privacidade

O catálogo deve priorizar dados empresariais públicos e necessários. Dados de pessoas jurídicas, como razão social, CNPJ e endereço comercial, não são, por si sós, dados pessoais; já nome, CPF, telefone pessoal e e-mail pessoal de responsáveis exigem atenção. [brasilparticipativo.presidencia.gov](https://brasilparticipativo.presidencia.gov.br/processes/guiadadospessoais/f/4670/?locale=pt-BR)

### Regras práticas

- Publique apenas dados comerciais públicos e necessários.
- Não publique CPF, documento, endereço residencial ou telefone pessoal.
- Não publique nome civil de MEI se não for necessário para a finalidade do catálogo.
- Use telefone comercial ou WhatsApp empresarial.
- Mantenha um canal de contato para correção, atualização e exclusão.
- Documente a origem de cada dado.
- Permita que a empresa solicite remoção ou correção.
- Faça backup antes de exclusões definitivas.
- Restrinja o acesso administrativo ao mínimo necessário.

As orientações oficiais reforçam minimização, finalidade específica, transparência, qualidade dos dados, segurança e direitos de acesso, correção e eliminação. [gov](https://www.gov.br/gestao/pt-br/acesso-a-informacao/privacidade-e-protecao-de-dados/lgpd-no-mgi-1/OrientacoesparaPrivacidade_v3_web.pdf)

## 13. Fontes de dados

### Receita Federal

Use os dados abertos do CNPJ para criar a base inicial de empresas ativas em Barretos. Os arquivos incluem dados cadastrais, CNAEs, endereço e situação cadastral. [gov](https://www.gov.br/receitafederal/dados/cnpj-metadados.pdf/@@download/file)

### SEADE

Use o repositório do SEADE para validar a distribuição setorial, emprego, PIB municipal e dados por município. O repositório oferece bases em CSV e API, além de informações municipais para os 645 municípios paulistas. [repositorio.seade.gov](https://repositorio.seade.gov.br/group/seade-municipios?groups=seade-municipios&res_format=CSV)

### Verificação direta

Após importar a base, confirme os dados por:

- Site oficial da empresa.
- Telefone comercial.
- WhatsApp comercial.
- Instagram ou Facebook oficial.
- Google Maps, apenas para consulta e validação manual.
- Ligação ou mensagem ao estabelecimento.

## 14. Geolocalização

Use OpenStreetMap e Nominatim apenas para geocodificar endereços durante a importação. Armazene latitude e longitude no banco, evitando chamadas repetidas em tempo real.

Regras recomendadas:

- Uma requisição por segundo.
- User-Agent identificável.
- Cache permanente dos resultados.
- Geocodificação apenas para empresas que serão exibidas no mapa.
- Respeito às políticas de uso do serviço.

## 15. Roadmap do MVP

| Etapa | Entrega |
|---|---|
| 1 | Estrutura do projeto Astro + Cloudflare |
| 2 | Banco D1 e tabelas iniciais |
| 3 | Taxonomia de categorias e bairros |
| 4 | Importação de 30 empresas reais |
| 5 | Página inicial com busca e filtros |
| 6 | Página individual da empresa |
| 7 | Painel administrativo protegido |
| 8 | Upload de CSV e CRUD |
| 9 | Formulário Google de sugestão/cadastro |
| 10 | Domínio registro.br e publicação |
| 11 | Política de privacidade e canal de correção |

## Links oficiais

- Receita Federal — Dados Abertos do CNPJ: [https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/dados](https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/dados) [gov](https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/dados)
- Receita Federal — Novo layout dos dados abertos do CNPJ: [https://www.gov.br/receitafederal/dados/cnpj-metadados.pdf/@@download/file](https://www.gov.br/receitafederal/dados/cnpj-metadados.pdf/@@download/file) [gov](https://www.gov.br/receitafederal/dados/cnpj-metadados.pdf/@@download/file)
- Receita Federal — Repositório de arquivos dos dados abertos do CNPJ: [https://arquivos.receitafederal.gov.br/dados/cnpj/dados_abertos_cnpj/](https://arquivos.receitafederal.gov.br/dados/cnpj/dados_abertos_cnpj/) [arquivos.receitafederal.gov](https://arquivos.receitafederal.gov.br/dados/cnpj/dados_abertos_cnpj/)
- SEADE — Repositório de dados abertos: [https://repositorio.seade.gov.br/dataset/](https://repositorio.seade.gov.br/dataset/) [repositorio.seade.gov](https://repositorio.seade.gov.br/dataset/)
- SEADE — Conjuntos municipais em CSV: [https://repositorio.seade.gov.br/group/seade-municipios?groups=seade-municipios&res_format=CSV](https://repositorio.seade.gov.br/group/seade-municipios?groups=seade-municipios&res_format=CSV) [repositorio.seade.gov](https://repositorio.seade.gov.br/group/seade-municipios?groups=seade-municipios&res_format=CSV)
- SEADE — Produtos e municípios: [https://repositorio.seade.gov.br/group/](https://repositorio.seade.gov.br/group/) [repositorio.seade.gov](https://repositorio.seade.gov.br/group/)
- SEADE — Painel de dados sociais e econômicos: [https://painel.seade.gov.br/](https://painel.seade.gov.br/) [painel.seade.gov](https://painel.seade.gov.br/)
- ANPD — Guia de tratamento de dados pessoais pelo poder público: [https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_tratamento_de_dados_pessoais_pelo_poder_publico___defeso_eleitoral.pdf/@@display-file/file](https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_tratamento_de_dados_pessoais_pelo_poder_publico___defeso_eleitoral.pdf/@@display-file/file) [gov](https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_tratamento_de_dados_pessoais_pelo_poder_publico___defeso_eleitoral.pdf/@@display-file/file)
- ANPD — Guia de hipóteses legais de tratamento: [https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_legitimo_interesse.pdf/@@download/file](https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_legitimo_interesse.pdf/@@download/file) [gov](https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_legitimo_interesse.pdf/@@download/file)
- Gov.br — Guias de LGPD: [https://www.gov.br/int/pt-br/acesso-a-informacao/lgpd/guias](https://www.gov.br/int/pt-br/acesso-a-informacao/lgpd/guias) [gov](https://www.gov.br/int/pt-br/acesso-a-informacao/lgpd/guias)
- Gov.br — Guia de privacidade desde a concepção: [https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/ppsi-2.0/arquivos/guia-sobre-privacidade-desde-a-concepcao-e-por-padrao-v1-1-310826.pdf](https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/ppsi-2.0/arquivos/guia-sobre-privacidade-desde-a-concepcao-e-por-padrao-v1-1-310826.pdf) [gov](https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/ppsi-2.0/arquivos/guia-sobre-privacidade-desde-a-concepcao-e-por-padrao-v1-1-310826.pdf)
- Gov.br — Boas práticas de LGPD: [https://www.gov.br/planejamento/pt-br/acesso-a-informacao/tratamento-de-dados-pessoais/boas-praticas-lgpd.pdf/@@display-file/file](https://www.gov.br/planejamento/pt-br/acesso-a-informacao/tratamento-de-dados-pessoais/boas-praticas-lgpd.pdf/@@display-file/file) [gov](https://www.gov.br/planejamento/pt-br/acesso-a-informacao/tratamento-de-dados-pessoais/boas-praticas-lgpd.pdf/@@display-file/file)
- Cloudflare Workers — Variáveis de ambiente: [https://developers.cloudflare.com/workers/configuration/environment-variables/](https://developers.cloudflare.com/workers/configuration/environment-variables/) [developers.cloudflare](https://developers.cloudflare.com/workers/configuration/environment-variables/)
- Cloudflare Workers — Limites do plano gratuito: [https://developers.cloudflare.com/workers/platform/limits/](https://developers.cloudflare.com/workers/platform/limits/) [developers.cloudflare](https://developers.cloudflare.com/workers/platform/limits/)
- Cloudflare Workers — Preços e limites: [https://developers.cloudflare.com/workers/platform/pricing/](https://developers.cloudflare.com/workers/platform/pricing/) [developers.cloudflare](https://developers.cloudflare.com/workers/platform/pricing/)
- Cloudflare D1 — Preços: [https://developers.cloudflare.com/d1/platform/pricing/](https://developers.cloudflare.com/d1/platform/pricing/) [developers.cloudflare](https://developers.cloudflare.com/d1/platform/pricing/)
- Cloudflare D1 — Limites: [https://developers.cloudflare.com/d1/platform/limits/](https://developers.cloudflare.com/d1/platform/limits/) [developers.cloudflare](https://developers.cloudflare.com/d1/platform/limits/)
- Cloudflare Pages — Configuração de build: [https://developers.cloudflare.com/pages/configuration/build-configuration/](https://developers.cloudflare.com/pages/configuration/build-configuration/) [developers.cloudflare](https://developers.cloudflare.com/pages/configuration/build-configuration/)
- Cloudflare Workers — Configuração de builds: [https://developers.cloudflare.com/workers/ci-cd/builds/configuration/](https://developers.cloudflare.com/workers/ci-cd/builds/configuration/) [developers.cloudflare](https://developers.cloudflare.com/workers/ci-cd/builds/configuration/)