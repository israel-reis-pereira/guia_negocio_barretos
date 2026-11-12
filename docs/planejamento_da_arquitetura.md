# Portal de Utilidade Pública de Barretos
## Planejamento de Arquitetura, Dados e Funcionalidades

**Status:** Planejamento inicial  
**Objetivo:** Construir um portal público de utilidade local, com alto desempenho, baixo custo operacional e manutenção simplificada.

---

# 1. Visão Geral do Projeto

A proposta é desenvolver um portal de utilidade pública para Barretos, reunindo informações sobre empresas, oportunidades de emprego, serviços autônomos e ferramentas úteis para a população.

A arquitetura deve priorizar:

- Máximo desempenho na entrega de páginas.
- Custo operacional próximo de zero, sempre que possível.
- Baixo consumo de recursos computacionais.
- Experiência simples, especialmente em dispositivos móveis.
- Facilidade de atualização e manutenção.
- Ausência de cadastro obrigatório para os visitantes.
- Possibilidade de expansão modular sem reconstruir o projeto.

**Premissa principal:** o público consome informações, enquanto a administração controla e publica os dados.

Isso reduz a necessidade de autenticação pública, escrita constante no banco e sistemas complexos de gerenciamento.

# 2. Arquitetura Tecnológica Planejada

A proposta inicial utiliza uma arquitetura moderna baseada em processamento na borda (Edge Computing).

| Camada | Tecnologia | Responsabilidade |
|---|---|---|
| Domínio | Registro.br | Registro do domínio `.br` |
| DNS e CDN | Cloudflare | DNS, distribuição de conteúdo e infraestrutura de borda |
| Frontend | Astro | Geração de páginas e renderização |
| Adaptador | @astrojs/cloudflare | Integração do Astro com Cloudflare |
| Computação | Cloudflare Workers | APIs, rotas dinâmicas e regras de negócio |
| Banco de dados | Cloudflare D1 | Dados relacionais utilizando SQLite |
| Armazenamento | Cloudflare R2 | Imagens, logotipos, documentos e arquivos |
| ORM | Drizzle ORM | Consultas e migrations do banco |
| Estilização | Tailwind CSS | Construção de interfaces leves |
| Ferramentas | Wrangler CLI | Desenvolvimento, configuração e deploy |

## 2.1. Justificativa da arquitetura

### Astro

Responsável pela entrega das páginas do portal.

- Geração estática (SSG) para conteúdo relativamente permanente.
- Renderização sob demanda (SSR) para informações dinâmicas.
- JavaScript enviado ao navegador somente quando necessário.
- Componentes interativos por meio da arquitetura Astro Islands.

### Cloudflare Workers

Responsável pela execução de funcionalidades dinâmicas.

- Processamento de APIs.
- Comunicação com o D1.
- Regras de negócio.
- Importação de dados.
- Operações administrativas.

### Cloudflare D1

Banco de dados relacional baseado em SQLite.

Será utilizado principalmente para:

- Cadastro de empresas.
- Cadastro de vagas e serviços.
- Relacionamento entre empresas e oportunidades.
- Consultas com filtros.
- Controle de validade dos anúncios.
- Consulta de status de ordens de serviço, caso implementada.

### Cloudflare R2

Armazenamento de arquivos.

Será utilizado para:

- Logotipos das empresas.
- Fotografias de produtos.
- Portfólios de prestadores.
- Imagens de trabalhos realizados.
- Documentos e outros arquivos públicos.

### Drizzle ORM

Proposta de utilização para facilitar:

- Consultas ao D1.
- Organização das operações SQL.
- Criação de migrations.
- Evolução da estrutura do banco.

# 3. Diretrizes de Desempenho e Infraestrutura

O objetivo é evitar processamento desnecessário e aproveitar ao máximo a infraestrutura gratuita.

## 3.1. Estratégia de renderização

Utilizar duas estratégias de renderização conforme a natureza dos dados:

| Conteúdo | Estratégia | Justificativa |
|---|---|---|
| Páginas institucionais | SSG | Conteúdo pouco variável |
| Perfis de empresas | SSG ou estratégia híbrida | Informações relativamente permanentes |
| Empregos e serviços | SSR ou estratégia híbrida | Informações que mudam frequentemente |
| Ferramentas e calculadoras | Processamento no navegador | Evitar consultas desnecessárias ao servidor |

## 3.2. Cuidados técnicos

- Evitar dependências pesadas que dependam de módulos nativos do Node.js incompatíveis com o ambiente dos Workers.
- Manter as rotas de API enxutas.
- Utilizar índices nas colunas frequentemente filtradas do D1.
- Utilizar carregamento tardio (lazy loading) para imagens.
- Preferir processamento local no navegador quando possível.
- Utilizar R2 para arquivos, evitando armazenar imagens diretamente no banco.
- Evitar consultas repetitivas ao D1 quando os dados puderem ser entregues estaticamente.

## 3.3. Integração do domínio

O domínio permanecerá registrado no Registro.br.

A proposta é utilizar os servidores DNS fornecidos pela Cloudflare, configurando os nameservers no painel do Registro.br.

Não é necessário transferir o registro do domínio.

# 4. Estrutura Funcional do Portal

O projeto terá dois painéis principais, compartilhando a mesma base de dados.

## 4.1. Painel de Empresas e Perfis

Objetivo: apresentar empresas e estabelecimentos de Barretos em um diretório público.

### Filtros principais

- Categoria: comércio, saúde, agronegócio e serviços.
- Bairro ou região.
- Status de funcionamento.
- Atendimento via WhatsApp.

### Informações dos perfis

- Nome da empresa.
- Logotipo.
- Descrição resumida.
- Categoria.
- Endereço.
- Bairro.
- Horário de funcionamento.
- Telefone.
- WhatsApp.
- Link para localização no mapa.
- Vagas e serviços vinculados.
- Produtos ou serviços em destaque, quando disponíveis.

### Ações disponíveis

- Chamar no WhatsApp.
- Ver rota no mapa.
- Ligar diretamente.
- Consultar oportunidades disponíveis.
- Visualizar produtos e serviços.

## 4.2. Painel de Empregos e Serviços

Objetivo: reunir oportunidades de emprego e profissionais autônomos em um único ambiente de consulta.

### Filtros principais

- Categoria da oferta.
- Área de atuação.
- Bairro ou região.
- Tipo de contratação.
- Turno.

### Categorias de oferta

1. Vaga de emprego:
   - CLT.
   - Temporário.
   - Outras modalidades de contratação.

2. Prestador de serviço:
   - Eletricista.
   - Diarista.
   - Pintor.
   - Pedreiro.
   - Jardineiro.
   - Frete.
   - Outros profissionais autônomos.

### Informações das oportunidades

- Título.
- Descrição.
- Faixa salarial ou valor do serviço.
- Requisitos resumidos.
- Empresa ou profissional responsável.
- Data de publicação.
- Data de expiração.
- Contato.

### Ações disponíveis

- Candidatar-se via WhatsApp.
- Entrar em contato com o contratante.
- Acessar formulário ou e-mail, quando disponível.

# 5. Integração entre Empresas, Empregos e Serviços

Os dois painéis devem compartilhar a mesma estrutura de dados.

A empresa será o registro principal, enquanto as vagas e oportunidades serão registros relacionados.

### Relacionamento proposto

- Tabela `empresas`: armazena os dados permanentes das empresas.
- Tabela `vagas_servicos`: armazena oportunidades e serviços vinculados às empresas.

Uma empresa poderá possuir várias oportunidades.

Ao acessar o perfil de uma empresa, o cidadão poderá visualizar automaticamente suas vagas e serviços disponíveis.

### Diferenças entre os registros

| Característica | Empresas | Empregos e Serviços |
|---|---|---|
| Frequência de atualização | Baixa | Alta |
| Natureza dos dados | Relativamente permanentes | Temporários |
| Renderização sugerida | SSG | SSR ou híbrida |
| Validade | Até alteração ou encerramento | Prazo definido |
| Relacionamento | Registro principal | Registro vinculado |

### Validade das oportunidades

As oportunidades poderão ter prazo de expiração de 15 ou 30 dias.

A consulta SQL poderá considerar a data de expiração:

```sql
WHERE data_expiracao > DATE('now')
```

Também deverá existir a possibilidade de encerrar uma oportunidade manualmente.

# 6. Estratégia de Alimentação e Atualização dos Dados

A prioridade é evitar a criação de um painel administrativo complexo.

Foram identificadas três alternativas.

## 6.1. Planilha + CSV

**Funcionamento:**

1. Organizar empresas e oportunidades em uma planilha.
2. Exportar os dados em CSV.
3. Acessar uma rota administrativa privada.
4. Enviar o arquivo.
5. Um Worker processa os registros.
6. Os dados são atualizados em lote no D1.

**Vantagens:**
- Controle total antes da publicação.
- Facilidade de organização.
- Atualização centralizada.
- Pouca complexidade operacional.

**Limitação:**
- Exige exportação e envio manual a cada atualização.

## 6.2. Google Forms + Apps Script

**Funcionamento:**

1. O comerciante preenche um Google Forms.
2. Os dados são enviados para uma planilha.
3. Um Apps Script executa o evento `onFormSubmit`.
4. O script envia os dados em JSON para um Worker.
5. O Worker registra a solicitação no D1 com status pendente.
6. O administrador revisa e aprova a publicação.

**Vantagens:**
- Reduz a necessidade de digitação manual.
- Permite receber informações diretamente dos comerciantes.
- Aproveita ferramentas gratuitas.

**Limitação:**
- Exige moderação para evitar duplicidades, spam e informações incorretas.

## 6.3. Astro estático + CSV no Build

**Funcionamento:**

1. Os dados são organizados em uma planilha.
2. O CSV é disponibilizado para o processo de build.
3. O Astro lê os dados.
4. As páginas são geradas estaticamente.
5. Um novo deploy publica as alterações.

**Vantagens:**
- Excelente desempenho.
- Não exige consultas ao D1 para entregar as páginas geradas.
- Reduz o processamento dinâmico.

**Limitação:**
- Uma nova publicação é necessária para atualizar os dados.

## 6.4. Fluxo híbrido sugerido

A proposta inicial é combinar Google Forms, Google Sheets, CSV, Cloudflare Access e D1.

Fluxo:

1. **Coleta:** comerciantes enviam informações por Google Forms.
2. **Curadoria:** os dados são organizados e revisados em uma planilha.
3. **Publicação:** somente registros aprovados entram na aba `Publicados`.
4. **Importação:** o administrador exporta os dados em CSV.
5. **Atualização:** um Worker importa os registros para o D1.
6. **Entrega:** o Astro disponibiliza as informações ao público.

### Organização da planilha

Inicialmente, utilizar duas abas:

- `Empresas`
- `Vagas_Servicos`

A aba de empresas será atualizada com menor frequência.

A aba de vagas e serviços será atualizada com maior frequência.

### Proteção administrativa

Utilizar Cloudflare Zero Trust (Access) para proteger a rota `/admin`, permitindo acesso somente ao administrador autorizado.

A proposta é evitar a implementação inicial de um sistema próprio de login e gerenciamento de sessões.

# 7. Estratégia de Estilização

## Tailwind CSS

A proposta é utilizar Tailwind CSS integrado ao Astro.

### Justificativas

- Geração de CSS durante o build.
- Remoção de classes não utilizadas.
- Ausência de JavaScript adicional de execução do framework.
- Facilidade de criação de componentes reutilizáveis.
- Boa integração com páginas Astro.
- Possibilidade de manter arquivos CSS compactos.

A intenção é preservar a filosofia de baixo JavaScript do Astro.

# 8. Funcionalidades Complementares Reaproveitáveis

Durante a análise de 15 projetos independentes, foram identificadas funcionalidades que podem ser incorporadas ao portal principal.

A prioridade é reaproveitar recursos que não exijam autenticação complexa ou operações constantes no servidor.

## 8.1. Projeto 5 — Catálogo Digital com Sacola no WhatsApp

**Aplicação no portal:**

Adicionar uma pequena vitrine de produtos ou serviços nos perfis das empresas.

Exemplos:
- Moda country.
- Produtos de lojas locais.
- Produtos de comércio em geral.

**Funcionamento:**

- Exibir de 3 a 6 produtos em destaque.
- Permitir selecionar produtos.
- Montar uma sacola no navegador.
- Utilizar JavaScript leve e LocalStorage.
- Enviar o pedido diretamente para o WhatsApp da loja.

**Impacto técnico:**

- Imagens armazenadas no R2.
- Sacola processada no navegador.
- Sem necessidade de consultas constantes ao D1.

## 8.2. Projeto 8 — Quadro de Avisos e Cotações

**Aplicação no portal:**

Criar uma seção de utilidade pública e rural.

Possíveis conteúdos:
- Cotações agrícolas.
- Informações relacionadas ao agronegócio.
- Comunicados locais.
- Avisos de interesse da população.

**Funcionamento:**

- Informações organizadas em planilha.
- Atualização via CSV.
- Exibição pública.
- Identificação da fonte e data de atualização.

**Impacto técnico:**

Baixa complexidade e possibilidade de utilizar a mesma estratégia de atualização dos demais conteúdos públicos.

## 8.3. Projeto 7 — Rastreador de Ordem de Serviço

**Aplicação no portal:**

Disponibilizar uma consulta simples para oficinas e assistências técnicas.

**Funcionamento:**

1. O cliente informa um código único.
2. O sistema consulta o registro.
3. Exibe somente o status da ordem de serviço.

Exemplos de status:
- Em análise.
- Em andamento.
- Pronto.

**Impacto técnico:**

- Uma tabela adicional no D1.
- Atualização por CSV.
- Consulta simples.
- Não exibir informações pessoais.

## 8.4. Projeto 11 — Calculadora de Tintas e Orçamento

**Aplicação no portal:**

Criar uma seção chamada `Ferramentas Úteis` ou `Calculadoras para a População`.

Público:
- Moradores.
- Pintores.
- Prestadores de serviços.

**Funcionamento:**

- Processamento em JavaScript puro.
- Cálculo realizado no navegador.
- Geração de orçamento.
- Utilização de `window.print()` para impressão ou geração de PDF pelo navegador.
- Compartilhamento pelo WhatsApp.

**Impacto técnico:**

- Sem consultas ao D1.
- Sem processamento no Worker para os cálculos.
- Baixo custo operacional.

## 8.5. Projeto 12 — Catálogo Digital e Portfólio de Obras

**Aplicação no portal:**

Adicionar uma galeria de trabalhos realizados aos perfis dos prestadores de serviços.

Exemplos:
- Pintores.
- Pedreiros.
- Jardineiros.
- Outros profissionais autônomos.

**Funcionamento:**

- Minigaleria com até quatro fotos.
- Imagens dos trabalhos concluídos.
- Carregamento sob demanda.

**Impacto técnico:**

- Imagens armazenadas no R2.
- Lazy loading.
- Reaproveitamento da estrutura de perfis.
- Baixo impacto na infraestrutura.

# 9. Projetos que Devem Permanecer Separados

Os outros projetos identificados apresentam características que aumentariam a complexidade do portal.

A recomendação inicial é mantê-los separados.

| Projetos | Funcionalidade | Motivo para não incorporar agora |
|---|---|---|
| 1 e 10 | Cobrança e Caderneta de Fiado | Dados financeiros privados e permissões por estabelecimento |
| 2 e 9 | Agendamentos e Pedidos de Cozinha | Operações internas e atualizações em tempo real |
| 3 | Avaliações | Necessidade de regras próprias de publicação e moderação |
| 4 | Recibos Médicos | Possível tratamento de dados sensíveis de saúde |
| 6 | Disparo VIP | Consentimento e integração com APIs de comunicação |
| 13 | Diário de Obra | Controle de acesso, fotos e gestão de arquivos |
| 14 | Controle de Recebimentos | Gestão financeira privada |
| 15 | Central de Parcerias | Aprovações entre partes e controle de comissões |

Esses projetos poderão ser desenvolvidos futuramente como produtos SaaS independentes.

A possibilidade é oferecê-los comercialmente às empresas e profissionais que já utilizam o portal público.

# 10. Visão Consolidada dos 15 Projetos

A estratégia é dividir as ideias em dois caminhos.

## 10.1. Caminho 1 — Portal Público de Barretos

**Objetivo:** construir uma plataforma gratuita de consulta e utilidade local.

### Núcleo principal

1. Painel de Empresas e Perfis.
2. Painel de Empregos e Serviços.

### Funcionalidades complementares reaproveitadas

| Projeto | Funcionalidade incorporada |
|---|---|
| 5 | Mini-vitrine de produtos com sacola no WhatsApp |
| 7 | Consulta simplificada de status de ordem de serviço |
| 8 | Quadro de avisos e cotações |
| 11 | Calculadora de tintas e orçamento |
| 12 | Portfólio de trabalhos dos prestadores |

Todas essas funcionalidades devem seguir a mesma filosofia: simplicidade, baixo custo e mínimo processamento no servidor.

## 10.2. Caminho 2 — Produtos SaaS Futuros

Os projetos que exigem operações privadas poderão se transformar em produtos independentes.

Possibilidades:
- Gestão financeira.
- Controle de fiado.
- Agendamentos.
- Pedidos de cozinha.
- Recibos.
- Diário de obras.
- Controle de recebimentos.
- Gestão de parcerias.

A ideia é desenvolver esses produtos posteriormente, aproveitando o relacionamento com empresas e profissionais cadastrados no portal.

# 11. Estratégia de Implementação

Para evitar expansão prematura do escopo, a implementação deverá acontecer por etapas.

## Fase 1 — Fundação

- Criar o projeto Astro.
- Configurar o adaptador Cloudflare.
- Configurar Tailwind CSS.
- Preparar Cloudflare Workers.
- Criar banco D1.
- Criar bucket R2.
- Configurar domínio e DNS.
- Preparar ambiente de desenvolvimento com Wrangler.

## Fase 2 — Estrutura de dados

- Criar tabela de empresas.
- Criar tabela de vagas e serviços.
- Definir relacionamentos.
- Criar índices para filtros.
- Definir regras de expiração.
- Preparar importação CSV.

## Fase 3 — Painéis principais

- Desenvolver painel de empresas.
- Desenvolver painel de empregos e serviços.
- Implementar filtros.
- Criar perfis individuais.
- Implementar links para WhatsApp.
- Implementar integração entre empresas e oportunidades.

## Fase 4 — Administração e atualização

- Criar rota `/admin`.
- Proteger acesso com Cloudflare Access.
- Implementar importação CSV.
- Integrar planilhas.
- Criar fluxo de revisão e publicação.

## Fase 5 — Funcionalidades complementares

Priorizar:
1. Mini-vitrines.
2. Portfólios de profissionais.
3. Quadro de avisos e cotações.
4. Calculadoras.
5. Consulta de ordens de serviço.

## Fase 6 — Expansão futura

Avaliar a transformação dos projetos independentes em produtos SaaS.

---

# 12. Princípios que Devem Orientar o Desenvolvimento

1. **Desempenho primeiro:** evitar funcionalidades que adicionem processamento sem benefício proporcional.
2. **Custo mínimo:** priorizar serviços gratuitos e operações eficientes.
3. **Simplicidade:** não implementar sistemas complexos quando uma solução mais simples atende à necessidade.
4. **Dados centralizados:** compartilhar a estrutura de empresas entre os diferentes módulos.
5. **Renderização adequada:** utilizar SSG para conteúdo estável e processamento dinâmico somente quando necessário.
6. **Pouco JavaScript:** priorizar HTML e CSS, adicionando interatividade apenas quando necessário.
7. **Segurança:** proteger operações administrativas e evitar exposição de informações privadas.
8. **Modularidade:** permitir que novas funcionalidades sejam adicionadas sem comprometer o núcleo.
9. **Manutenção simples:** priorizar planilhas, CSV e processos administrativos enxutos.
10. **Foco no usuário:** oferecer acesso rápido às informações, principalmente em dispositivos móveis.

# 13. Observações e Pendências Técnicas

Este documento consolida propostas e recomendações levantadas durante o planejamento. Não representa uma arquitetura já implementada ou validada em produção.

Antes da implementação, será necessário:

- Confirmar os limites e preços atuais dos serviços Cloudflare.
- Validar a estratégia de SSG e SSR nas versões atuais do Astro e do adaptador Cloudflare.
- Definir o modelo definitivo do banco D1.
- Definir identificadores únicos para empresas e profissionais.
- Estabelecer regras de atualização, exclusão e expiração dos registros.
- Definir a estratégia de cache.
- Avaliar proteção contra abuso nas consultas públicas.
- Definir cuidados com LGPD, especialmente para informações de contato e ordens de serviço.
- Testar o processo de importação CSV e tratamento de duplicidades.
- Validar os custos de armazenamento e operações do R2.

**Observação:** os números de limites gratuitos mencionados nas conversas originais são referências levantadas naquele momento e precisam ser confirmados na documentação oficial antes de orientar decisões de produção.

---

# 14. Direção Geral do Projeto

A visão é construir primeiro um portal público de utilidade local, capaz de concentrar informações relevantes para a população de Barretos.

A prioridade não é criar um sistema administrativo complexo nem transformar todas as ideias em um único software.

A prioridade é desenvolver uma base tecnológica enxuta, eficiente e sustentável, com dois painéis principais e funcionalidades complementares que realmente agreguem valor.

A arquitetura planejada é:

**Astro + Tailwind CSS + Cloudflare Workers + Cloudflare D1 + Cloudflare R2 + Registro.br.**

O desenvolvimento deverá priorizar o núcleo do portal. Os demais projetos serão incorporados somente quando houver justificativa funcional e técnica.

**Objetivo final:** oferecer uma plataforma pública rápida, acessível, útil e de baixo custo, mantendo aberta a possibilidade de transformar ideias independentes em produtos SaaS no futuro.