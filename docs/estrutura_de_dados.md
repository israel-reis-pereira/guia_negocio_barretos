# Perfil da Empresa no Google — Estrutura de Dados e Variáveis

## 1. Visão geral

O **Perfil da Empresa no Google** (antigo Google Meu Negócio) reúne informações comerciais, dados de localização, canais de contato, conteúdo visual, produtos, serviços, avaliações e métricas de desempenho.

Essas informações podem ser cadastradas pelo proprietário da empresa ou geradas a partir das interações dos usuários com o perfil.

Os dados são utilizados para apresentar a empresa na Pesquisa Google e no Google Maps.

Este documento organiza os campos identificados em variáveis com nomenclatura `snake_case`, facilitando seu aproveitamento em sistemas, bancos de dados, APIs, CRMs e dashboards.

---

## 2. Estrutura de dados

### 2.1. Informações básicas e identificação

Dados utilizados para identificar e descrever a empresa.

| Variável | Descrição |
|---|---|
| `nome_da_empresa` | Nome oficial do negócio exibido na Pesquisa Google e no Maps. |
| `categoria_principal` | Ramo principal de atuação da empresa. Exemplo: Restaurante, Advogado. |
| `categorias_secundarias` | Outros ramos de atuação associados ao negócio. |
| `descricao_da_empresa` | Resumo sobre o negócio, sua história e seus diferenciais. |
| `data_de_abertura` | Ano e mês em que a empresa começou a operar. |

### 2.2. Localização e áreas de atendimento

Informações geográficas utilizadas para localizar a empresa e identificar as regiões atendidas.

| Variável | Descrição |
|---|---|
| `endereco_fisico` | Endereço completo: logradouro, número, complemento, bairro, cidade, estado e CEP. |
| `coordenadas_geograficas` | Latitude e longitude utilizadas para posicionar a empresa no mapa. |
| `areas_de_cobertura` | Cidades, bairros ou regiões atendidas pela empresa, especialmente quando não existe atendimento em endereço aberto ao público. |

### 2.3. Horários e disponibilidade

Informações sobre os períodos de funcionamento e disponibilidade dos serviços.

| Variável | Descrição |
|---|---|
| `horario_regular` | Dias da semana e horários padrão de abertura e fechamento. |
| `horario_especial` | Alterações programadas para feriados, recessos ou eventos. |
| `horarios_especificos` | Horários destinados a serviços específicos, como entregas, happy hour ou atendimento a determinados públicos. |

### 2.4. Canais de contato e links

Informações utilizadas para permitir que os clientes entrem em contato com a empresa ou acessem seus canais digitais.

| Variável | Descrição |
|---|---|
| `telefone_principal` | Número principal para ligações de clientes. |
| `telefones_adicionais` | Números secundários ou contatos de outros setores. |
| `website_url` | Endereço do site oficial da empresa. |
| `link_agendamento` | URL para sistemas externos de reservas ou agendamentos. |
| `link_menu_cardapio` | URL direta para o cardápio ou lista de preços. |

### 2.5. Conteúdo visual e atributos

Informações visuais e características utilizadas para apresentar a empresa.

| Variável | Descrição |
|---|---|
| `fotos_do_perfil` | Imagens do logotipo, capa, ambientes internos, ambientes externos e equipe. |
| `videos_da_empresa` | Vídeos curtos do estabelecimento ou demonstrações de produtos e serviços. |
| `atributos_comodidades` | Características e comodidades, como Wi-Fi gratuito, acessibilidade e estacionamento gratuito. |
| `atributos_propriedade` | Identificadores relacionados à propriedade ou inclusão, como empresa de propriedade de mulheres. |

### 2.6. Portfólio comercial

Informações sobre os produtos e serviços oferecidos pela empresa.

| Variável | Descrição |
|---|---|
| `lista_de_serviços` | Títulos, descrições e preços dos serviços prestados. |
| `catalogo_de_produtos` | Produtos físicos com fotos, nomes, categorias, preços e links de compra. |

### 2.7. Interações e reputação

Dados públicos ou relacionados às interações dos clientes com o perfil.

| Variável | Descrição |
|---|---|
| `historico_de_avaliacoes` | Textos das avaliações publicadas pelos clientes. |
| `nota_media_estrelas` | Média geral das avaliações, em uma escala de 1 a 5 estrelas. |
| `respostas_da_empresa` | Respostas publicadas pelo proprietário às avaliações dos clientes. |
| `perguntas_dos_usuarios` | Perguntas publicadas pela comunidade no perfil da empresa. |
| `respostas_da_comunidade` | Respostas fornecidas por outros usuários ou pela própria empresa. |
| `mensagens_chat` | Histórico de conversas diretas e privadas por meio do chat do Google. |

### 2.8. Conteúdo dinâmico

Publicações utilizadas para divulgar novidades, ofertas e eventos.

| Variável | Descrição |
|---|---|
| `postagens_atualizacoes` | Textos e imagens relacionados às novidades e atualizações da empresa. |
| `postagens_ofertas` | Cupons de desconto, promoções, datas de validade e condições das ofertas. |
| `postagens_eventos` | Informações sobre eventos promovidos pela empresa, incluindo título, data e horário. |

### 2.9. Métricas de desempenho

Dados de desempenho e estatísticas disponibilizados ao gestor do perfil.

| Variável | Descrição |
|---|---|
| `visualizacoes_totais` | Quantidade de vezes que o perfil apareceu na Pesquisa Google ou no Maps. |
| `palavras_chave_busca` | Termos utilizados pelos usuários para encontrar a empresa. |
| `cliques_no_website` | Quantidade de acessos direcionados ao site da empresa. |
| `chamadas_telefonicas` | Quantidade de interações com o botão de ligação. |
| `solicitacoes_de_rota` | Quantidade de cliques para abrir o GPS e obter uma rota até o endereço. |
| `mensagens_recebidas` | Total de conversas iniciadas pelos clientes por meio do perfil. |

---

## 3. Lista consolidada de variáveis

Abaixo está a relação de todas as variáveis identificadas no material, sem as descrições, para facilitar a consulta e o reaproveitamento em projetos.

```text
# Informações básicas e identificação
nome_da_empresa
categoria_principal
categorias_secundarias
descricao_da_empresa
data_de_abertura

# Localização e áreas de atendimento
endereco_fisico
coordenadas_geograficas
areas_de_cobertura

# Horários e disponibilidade
horario_regular
horario_especial
horarios_especificos

# Canais de contato e links
telefone_principal
telefones_adicionais
website_url
link_agendamento
link_menu_cardapio

# Conteúdo visual e atributos
fotos_do_perfil
videos_da_empresa
atributos_comodidades
atributos_propriedade

# Portfólio comercial
lista_de_serviços
catalogo_de_produtos

# Interações e reputação
historico_de_avaliacoes
nota_media_estrelas
respostas_da_empresa
perguntas_dos_usuarios
respostas_da_comunidade
mensagens_chat

# Conteúdo dinâmico
postagens_atualizacoes
postagens_ofertas
postagens_eventos

# Métricas de desempenho
visualizacoes_totais
palavras_chave_busca
cliques_no_website
chamadas_telefonicas
solicitacoes_de_rota
mensagens_recebidas
```

---

## 4. Fontes de referência

O material original informa que a estrutura foi consolidada com base em duas fontes principais.

### 4.1. Documentação oficial de suporte do Google

Referência para informações sobre o gerenciamento do Perfil da Empresa, incluindo:

- Dados de identificação.
- Endereço e localização.
- Horários de funcionamento.
- Fotos e vídeos.
- Produtos e serviços.
- Publicações e ofertas.
- Avaliações e informações comerciais.

Fonte:

- [Ajuda do Perfil da Empresa no Google](https://support.google.com/business/)

### 4.2. Documentação técnica das APIs do Google Business Profile

Referência para a estrutura de dados utilizada por desenvolvedores e sistemas que integram informações do Perfil da Empresa.

O material menciona os seguintes grupos de APIs:

- Account Management API.
- Business Information API.
- Reviews API.
- Performance API.

Fonte:

- [Google Business Profile APIs — Google for Developers](https://developers.google.com/my-business/)

### 4.3. Referências complementares mencionadas no material original

- Google Business Profile.
- Google Help.
- VIX360.
- bundle.social.
- Gofind.

---

## 5. Considerações técnicas para desenvolvimento de sistemas

A nomenclatura `snake_case` foi utilizada para representar os dados em um formato familiar ao desenvolvimento de software e à integração entre sistemas.

Essa organização pode servir como ponto de partida para:

- Modelagem de bancos de dados.
- Criação de estruturas JSON.
- Integração com APIs.
- Desenvolvimento de CRMs.
- Construção de dashboards.
- Sistemas de gestão de empresas.
- Plataformas de consulta e divulgação de negócios locais.

### 5.1. Atenção à disponibilidade dos dados

A lista apresentada representa os campos identificados no material consultado. Ela não deve ser interpretada como uma garantia de que todos os campos estejam disponíveis para leitura ou gravação por meio das APIs do Google.

Antes de implementar uma integração, é necessário verificar individualmente:

1. Se o campo existe na documentação oficial da API.
2. Se o campo pode ser consultado ou apenas atualizado.
3. Se exige autenticação ou permissões específicas.
4. Se está disponível para todos os tipos de empresa.
5. Se possui limitações ou condições de acesso.

Também é importante diferenciar os dados cadastrados pelo proprietário, os dados gerados pelos usuários e as métricas disponibilizadas exclusivamente ao gestor.

---

## 6. Objetivo final

Este documento funciona como um inventário inicial dos dados associados ao Perfil da Empresa no Google.

Sua principal finalidade é fornecer uma referência organizada de campos e variáveis que podem ser utilizados no planejamento de sistemas, integrações, bancos de dados e ferramentas de gestão de empresas.

**Observação:** a estrutura deve ser validada com a documentação técnica atual do Google antes de ser utilizada como especificação definitiva de uma integração.
