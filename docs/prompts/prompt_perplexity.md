# Como pesquisar e documentar a conformidade com a LGPD

Para o **Guia Comercial de Barretos**, a pesquisa deve priorizar fontes primárias brasileiras — Lei, ANPD, Receita Federal, SEADE e Google — e produzir uma pasta de referências que a IA possa ler antes de implementar ou importar dados. A recomendação é usar **curadoria manual própria** para o primeiro MVP, publicando apenas dados comerciais públicos e necessários, sem scraping de perfis do Google.

## 1. Decisão recomendada

Para começar sem custo e com menor risco jurídico, adote esta ordem:

1. **Curadoria manual própria em planilha/CSV** — recomendada como fonte primária do MVP.
2. **Formulário Google para sugestões e autorizações** — canal complementar de entrada.
3. **Dados abertos da Receita Federal** — apoio para validar CNPJ, razão social, CNAE e endereço cadastral.
4. **API oficial do Google** — apenas para consulta/exibição autorizada, não para criar uma base copiada.
5. **Scraping de Google Empresa/Maps** — não utilizar.

A curadoria manual é a opção mais segura porque você controla quais campos entram no catálogo, pode evitar dados pessoais e consegue documentar a origem de cada informação.

## 2. O que pesquisar primeiro

Crie uma pasta `docs/research/lgpd/` e salve, para cada tema, um arquivo `.md` com:

- Pergunta de pesquisa.
- Fonte oficial consultada.
- Data de acesso.
- Trecho ou resumo relevante.
- Decisão aplicada ao projeto.
- Link da fonte.
- Status: `aprovado`, `pendente` ou `bloqueado`.

### Arquivos recomendados

```text
docs/research/lgpd/
├── 01-lgpd-principios.md
├── 02-base-legal-dados-empresariais.md
├── 03-dados-pessoais-meis.md
├── 04-fontes-publicas-receita-federal.md
├── 05-google-maps-e-places-api.md
├── 06-formulario-google-e-consentimento.md
├── 07-direitos-dos-titulares.md
├── 08-retention-e-exclusao.md
└── 09-privacy-policy.md
```

## 3. Perguntas de pesquisa

Use estas perguntas como roteiro de busca. Elas devem ser respondidas com fonte oficial e data de acesso.

| Tema | Pergunta para pesquisar | Resultado esperado |
|---|---|---|
| LGPD | Quais são os princípios aplicáveis ao tratamento de dados? | Finalidade, necessidade, transparência, segurança e qualidade |
| Base legal | Quando é possível tratar dados pessoais? | Consentimento, obrigação legal, legítimo interesse, entre outras hipóteses |
| Dados empresariais | CNPJ, razão social e endereço comercial são dados pessoais? | Normalmente não, salvo quando identificam pessoa física |
| MEI | Como tratar nome civil, CPF e endereço residencial de MEI? | Não publicar sem necessidade e sem base legal adequada |
| Receita Federal | Quais campos podem ser usados dos dados abertos do CNPJ? | CNPJ, razão social, CNAE, situação cadastral e endereço |
| Google | Posso copiar dados de perfis do Google Empresa? | Não; usar API oficial ou dados informados pelo próprio comércio |
| Formulário | Quais avisos devem existir no Google Forms? | Finalidade, responsável, dados coletados, direitos e contato |
| Direitos | Quais direitos devem ser atendidos? | Acesso, correção, exclusão, portabilidade e revogação |
| Retenção | Por quanto tempo guardar dados? | Definir prazo por finalidade e política de exclusão |
| Segurança | Quais medidas mínimas adotar? | Acesso restrito, backups, senhas, minimização e logs |

## 4. Como pesquisar nas ferramentas

Nas ferramentas de IA, use prompts curtos, específicos e que exijam fontes primárias. Não aceite resposta sem link oficial e data de atualização.

### Prompt padrão

```text
Pesquise apenas em fontes oficiais brasileiras e internacionais primárias.

Tema: [inserir tema]

Pergunta: [inserir pergunta]

Requisitos:
1. Priorize ANPD, Planalto, Receita Federal, SEADE, IBGE, Google Cloud e documentação oficial.
2. Apresente apenas informações verificáveis.
3. Para cada afirmação, inclua link direto da fonte oficial.
4. Informe a data de publicação ou atualização da fonte, quando disponível.
5. Diferencie lei, regulamento, guia orientativo e opinião jurídica.
6. Aponte lacunas, exceções e riscos.
7. Não invente normas, artigos, prazos ou interpretações.
8. Ao final, entregue:
   - Resposta objetiva
   - Fontes oficiais com links
   - Riscos jurídicos
   - Decisão prática para um catálogo de empresas em Barretos
   - Campos que devo evitar publicar
```

### Exemplo aplicado

```text
Pesquise apenas em fontes oficiais brasileiras.

Tema: Publicação de dados de MEI em um guia comercial local.

Pergunta: Posso publicar nome civil, CPF, endereço residencial e telefone pessoal de um MEI em um catálogo de empresas?

Requisitos:
1. Priorize LGPD, ANPD e Receita Federal.
2. Cite artigos específicos da Lei nº 13.709/2018.
3. Diferencie dados empresariais de dados pessoais.
4. Informe quais campos podem ser publicados e quais devem ser evitados.
5. Explique as hipóteses legais possíveis.
6. Aponte riscos e medidas de mitigação.
7. Entregue links oficiais no final.
```

## 5. O que trazer para a IA ler

Após cada pesquisa, salve um arquivo curto, estruturado e verificável. Exemplo:

```md
# LGPD — Dados de MEI

## Pergunta
Posso publicar nome civil, CPF e endereço residencial de um MEI?

## Resposta
Não publique dados pessoais desnecessários. O catálogo deve usar nome fantasia,
categoria, endereço comercial, telefone comercial e canais públicos de contato.

## Fonte oficial
- Lei nº 13.709/2018 — Planalto
- ANPD — Guia orientativo

## Decisão do projeto
- `legalName`: não publicar automaticamente.
- `ownerName`: não publicar.
- `cpf`: não coletar nem publicar.
- `residentialAddress`: não coletar nem publicar.
- `businessPhone`: pode publicar se for público e comercial.
- `personalPhone`: não publicar.

## Status
Aprovado para o MVP.

## Data de verificação
2026-11-12
```

## 6. Regras para o catálogo

### Campos permitidos

| Campo | Publicação |
|---|---|
| Nome fantasia | Sim |
| Categoria e subcategoria | Sim |
| Endereço comercial | Sim, se público |
| Telefone comercial | Sim, se público |
| WhatsApp comercial | Sim, se público |
| Site oficial | Sim |
| Instagram/Facebook oficial | Sim |
| Horário de funcionamento | Sim |
| Descrição dos serviços | Sim |
| Imagem do estabelecimento | Sim, com autorização ou licença adequada |
| Faixa de preço | Sim, apenas quando aplicável |

### Campos que exigem cautela

| Campo | Decisão recomendada |
|---|---|
| Razão social | Publicar apenas se for necessário e não expuser pessoa física |
| CNPJ | Publicar apenas quando útil e público |
| Nome do proprietário | Evitar |
| CPF | Não publicar |
| Endereço residencial | Não publicar |
| Telefone pessoal | Não publicar |
| E-mail pessoal | Não publicar |
| Foto do proprietário | Não publicar sem autorização |
| Avaliações de usuários | Não copiar do Google |
| Coordenadas exatas de residência | Não publicar |

## 7. Fluxo de curadoria manual

### Planilha inicial

Crie uma planilha com estas colunas:

```text
id
slug
name
legal_name
cnpj
category
subcategory
neighborhood
address
phone
whatsapp
website
instagram
price_range
description
image_url
source
source_url
status
verified_at
notes_private
```

### Regras de preenchimento

- Use apenas fontes públicas e verificáveis.
- Registre a URL de onde cada dado foi obtido.
- Não copie avaliações, fotos ou textos do Google sem autorização.
- Marque registros não conferidos como `unverified`.
- Use `needs_review` quando houver divergência entre fontes.
- Não publique automaticamente dados importados da Receita Federal.
- Antes de publicar, confirme telefone, endereço e situação de funcionamento.

### Exemplo de linha

```csv
padaria-exemplo,padaria-exemplo,Padaria Exemplo,,00.000.000/0000-00,Alimentação e Bebidas,Padarias,Centro,"Rua Exemplo, 123, Barretos - SP","(17) 3000-0000",,https://exemplo.com.br,,,"$","Padaria com pães, bolos e cafés.",https://exemplo.com.br/logo.jpg,site-oficial,https://exemplo.com.br,verified,2026-11-12,
```

## 8. Formulário Google

O formulário deve coletar apenas dados necessários para publicar o comércio.

### Campos sugeridos

- Nome do estabelecimento.
- Categoria.
- Subcategoria.
- Bairro.
- Endereço comercial.
- Telefone comercial.
- WhatsApp comercial.
- Site.
- Instagram.
- Horário de funcionamento.
- Descrição.
- Link de uma imagem autorizada.
- Nome e cargo do responsável.
- E-mail institucional.
- Aceite da política de privacidade.
- Autorização para publicação.

### Aviso obrigatório

```text
Os dados informados serão utilizados exclusivamente para criar, validar e
publicar o cadastro do seu estabelecimento no Guia Comercial de Barretos.

Não solicitamos CPF, dados bancários, senhas ou documentos pessoais.

Você pode solicitar correção, atualização ou exclusão do cadastro pelo e-mail:
contato@seudominio.com.br
```

## 9. Política de privacidade

Crie uma página `/privacidade` com:

- Identificação do responsável pelo site.
- Finalidade do tratamento.
- Dados coletados.
- Base legal.
- Prazo de retenção.
- Compartilhamento com terceiros.
- Direitos do titular.
- Canal de contato.
- Como solicitar exclusão ou correção.
- Uso de cookies e analytics, se houver.
- Data da última atualização.

## 10. Checklist de conformidade

Antes de publicar cada empresa, confirme:

- [ ] O estabelecimento existe e está em operação.
- [ ] O endereço é comercial, não residencial.
- [ ] O telefone é comercial ou autorizado.
- [ ] O WhatsApp é comercial ou autorizado.
- [ ] O site e as redes sociais são oficiais.
- [ ] A imagem tem autorização ou licença adequada.
- [ ] Não há CPF, documento ou dado sensível exposto.
- [ ] Não há nome civil ou endereço residencial de MEI.
- [ ] A fonte do dado está registrada.
- [ ] A data de verificação está preenchida.
- [ ] O registro está com status `verified`.
- [ ] Existe canal de correção e exclusão.

## 11. O que evitar

- Não use scraping de Google Maps ou Google Empresa.
- Não copie avaliações, fotos, descrições ou horários do Google para armazenar no seu banco.
- Não publique dados pessoais de sócios, MEIs ou responsáveis.
- Não use dados de terceiros sem verificar origem e permissão.
- Não publique uma base inteira de CNPJs sem revisão.
- Não use o nome, logo ou marca de Barretos de forma que sugira vínculo oficial com a Prefeitura.
- Não prometa informações em tempo real que você não consegue garantir.

## 12. Fontes oficiais para pesquisa

- ANPD — página institucional e materiais orientativos: [https://anpd.gov.br/](https://anpd.gov.br/) [anpd.gov](https://anpd.gov.br/)
- ANPD — Guia orientativo de tratamento de dados pessoais pelo poder público: [https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_tratamento_de_dados_pessoais_pelo_poder_publico___defeso_eleitoral.pdf/@@display-file/file](https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_tratamento_de_dados_pessoais_pelo_poder_publico___defeso_eleitoral.pdf/@@display-file/file) 
- ANPD — Guia sobre hipóteses legais de tratamento de dados pessoais: [https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_legitimo_interesse.pdf/@@download/file](https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/guia_legitimo_interesse.pdf/@@download/file) 
- Gov.br — Guias de LGPD: [https://www.gov.br/int/pt-br/acesso-a-informacao/lgpd/guias](https://www.gov.br/int/pt-br/acesso-a-informacao/lgpd/guias) 
- Gov.br — Guia de privacidade desde a concepção e por padrão: [https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/ppsi-2.0/arquivos/guia-sobre-privacidade-desde-a-concepcao-e-por-padrao-v1-1-310826.pdf](https://www.gov.br/governodigital/pt-br/privacidade-e-seguranca/ppsi-2.0/arquivos/guia-sobre-privacidade-desde-a-concepcao-e-por-padrao-v1-1-310826.pdf) 
- Gov.br — Boas práticas de LGPD: [https://www.gov.br/planejamento/pt-br/acesso-a-informacao/tratamento-de-dados-pessoais/boas-praticas-lgpd.pdf/@@display-file/file](https://www.gov.br/planejamento/pt-br/acesso-a-informacao/tratamento-de-dados-pessoais/boas-praticas-lgpd.pdf/@@display-file/file) 
- Planalto — Lei nº 13.709/2018, LGPD: [https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) 
- Receita Federal — Repositório de dados abertos: [https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/dados](https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/dados) 
- Receita Federal — Layout dos dados abertos do CNPJ: [https://www.gov.br/receitafederal/dados/cnpj-metadados.pdf/@@download/file](https://www.gov.br/receitafederal/dados/cnpj-metadados.pdf/@@download/file) 
- Receita Federal — Arquivos dos dados abertos do CNPJ: [https://arquivos.receitafederal.gov.br/dados/cnpj/dados_abertos_cnpj/](https://arquivos.receitafederal.gov.br/dados/cnpj/dados_abertos_cnpj/) 
- SEADE — Repositório de dados abertos: [https://repositorio.seade.gov.br/dataset/](https://repositorio.seade.gov.br/dataset/) 
- SEADE — Conjuntos municipais em CSV: [https://repositorio.seade.gov.br/group/seade-municipios?groups=seade-municipios&res_format=CSV](https://repositorio.seade.gov.br/group/seade-municipios?groups=seade-municipios&res_format=CSV) 
- SEADE — Painel de dados sociais e econômicos: [https://painel.seade.gov.br/](https://painel.seade.gov.br/) 
- Google Maps Platform — Termos de serviço: [https://cloud.google.com/maps-platform/terms?hl=en_US](https://cloud.google.com/maps-platform/terms?hl=en_US) 
- Google Maps Platform — Termos específicos dos serviços: [https://cloud.google.com/maps-platform/terms/maps-service-terms](https://cloud.google.com/maps-platform/terms/maps-service-terms)