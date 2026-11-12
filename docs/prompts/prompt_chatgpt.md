# Pesquisa Jurídica e Técnica — LGPD, Fontes de Dados e Publicação do Catálogo de Negócios de Barretos/SP

## 1. Contexto do projeto

Estamos desenvolvendo um catálogo digital público e informativo de empresas e prestadores de serviços de Barretos/SP.

O objetivo é permitir que moradores encontrem negócios locais por meio de pesquisa textual, categorias e filtros.

O MVP terá:

- Página inicial com busca.
- Listagem de empresas.
- Filtros por categoria e bairro.
- Página individual de cada estabelecimento.
- Informações comerciais essenciais.
- No máximo uma imagem principal por empresa.
- Painel administrativo privado.
- Importação de dados por CSV.
- Catálogo público somente para leitura.

O desenvolvedor trabalha sozinho e precisa minimizar os custos de desenvolvimento, infraestrutura e manutenção.

A intenção é preparar uma base inicial de empresas antes de visitar os estabelecimentos. Posteriormente, os responsáveis poderão conferir, corrigir e complementar as informações.

## 2. Objetivo da pesquisa

Realizar uma pesquisa jurídica e técnica atualizada para determinar:

1. Quais informações empresariais podem ser coletadas.
2. Quais informações podem ser armazenadas.
3. Quais informações podem ser publicadas.
4. Quais bases legais podem justificar o tratamento de dados pessoais.
5. Quais fontes podem ser utilizadas legalmente.
6. Quais cuidados específicos devem ser adotados para MEIs e empresários individuais.
7. Como permitir que os responsáveis solicitem correções, atualização ou remoção de informações.
8. Como estruturar um processo de coleta e importação por CSV com rastreabilidade.

Não presumir que dados encontrados publicamente podem ser livremente reproduzidos.

Não considerar que a finalidade informativa do projeto, por si só, autoriza qualquer tratamento de dados pessoais.

## 3. Fontes prioritárias

Pesquisar prioritariamente documentos oficiais e fontes primárias.

### 3.1 Legislação

- Lei nº 13.709/2018 — Lei Geral de Proteção de Dados Pessoais.
- Texto atualizado da legislação.
- Dispositivos relacionados a dados pessoais, bases legais, legítimo interesse, transparência, direitos dos titulares, registros de tratamento e segurança.

Fonte:
https://www2.camara.leg.br/legin/fed/lei/2018/lei-13709-14-agosto-2018-787077-normaatualizada-pl.html

### 3.2 Autoridade Nacional de Proteção de Dados

Pesquisar:

- Guia Orientativo de Legítimo Interesse.
- Orientações sobre dados pessoais publicamente acessíveis.
- Direitos dos titulares.
- Orientações para agentes de tratamento de pequeno porte.
- Regulamentações aplicáveis ao controlador e ao operador.

Fontes:
https://www.gov.br/anpd/

https://www.gov.br/anpd/pt-br/centrais-de-conteudo/materiais-educativos-e-publicacoes/

https://www.gov.br/anpd/pt-br/assuntos/titular-de-dados-1/direito-dos-titulares

### 3.3 Receita Federal

Pesquisar:

- Dados abertos do CNPJ.
- Dicionário de dados.
- Campos disponíveis.
- Frequência de atualização.
- Formatos de download.
- Condições de utilização.
- Possibilidade de filtrar estabelecimentos de Barretos/SP.
- Campos que podem identificar pessoas naturais.

Fontes:
https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/dados-abertos/cadastros

https://www.gov.br/receitafederal/dados

Não presumir que todos os campos do CNPJ são adequados para publicação.

### 3.4 Google

Pesquisar os termos e políticas oficiais relacionados a:

- Google Maps Platform.
- Google Business Profile.
- Google Business Profile APIs.
- Extração, armazenamento, cache e redistribuição de informações.
- Direitos de utilização de fotografias e conteúdo de terceiros.

Fontes:
https://cloud.google.com/maps-platform/terms

https://developers.google.com/my-business/content/policies

Determinar expressamente se é permitido copiar em massa nomes, endereços, telefones, fotografias e outros dados de perfis do Google para formar uma base própria.

Não implementar scraping ou automação de coleta do Google sem comprovação de permissão contratual.

## 4. Pesquisas obrigatórias

### Pesquisa A — Enquadramento jurídico do catálogo

Avaliar a aplicação da LGPD ao catálogo público de negócios locais.

Distinguir:

- Dados de pessoas jurídicas.
- Dados pessoais de empresários individuais.
- Dados de MEIs.
- Dados de funcionários e representantes.
- Dados de contato comercial.
- Dados de contato pessoal.

Apresentar exemplos concretos relacionados ao projeto.

### Pesquisa B — Bases legais

Avaliar quais bases legais poderiam fundamentar a coleta, o armazenamento e a publicação dos dados.

Analisar especialmente:

- Consentimento.
- Legítimo interesse.
- Dados pessoais cujo acesso é público.
- Dados tornados manifestamente públicos pelo titular.
- Outras hipóteses legais eventualmente pertinentes.

Para legítimo interesse, realizar a análise de:

1. Finalidade.
2. Necessidade.
3. Balanceamento e salvaguardas.

Não afirmar que legítimo interesse é automaticamente aplicável ao catálogo.

Identificar situações em que a publicação deve depender de autorização ou confirmação do responsável.

### Pesquisa C — MEIs e empresários individuais

Investigar os riscos de:

- Publicar nome civil como nome comercial.
- Expor endereço residencial.
- Publicar telefone pessoal.
- Associar dados pessoais ao CNPJ.
- Reproduzir informações que originalmente foram disponibilizadas para outra finalidade.

Propor uma política de minimização de dados.

### Pesquisa D — Fontes de dados

Comparar:

1. Receita Federal — dados abertos do CNPJ.
2. Sites oficiais das empresas.
3. Diretórios e associações comerciais.
4. Informações fornecidas pelos próprios estabelecimentos.
5. Google Maps e Perfil da Empresa no Google.
6. Outras fontes públicas oficiais que possam ser encontradas.

Para cada fonte, apresentar:

- Órgão ou responsável.
- URL oficial.
- Tipo de informação disponível.
- Formato.
- Frequência de atualização.
- Licença ou termos de uso.
- Possibilidade de utilização no catálogo.
- Restrições.
- Riscos jurídicos.
- Custo de acesso.
- Conclusão: permitida, condicionada, não recomendada ou inconclusiva.

### Pesquisa E — Direitos dos titulares

Definir como o catálogo deverá receber e tratar solicitações de:

- Correção.
- Atualização.
- Oposição ao tratamento.
- Exclusão, quando cabível.
- Informações sobre origem e finalidade do tratamento.

Avaliar como implementar um canal de contato simples e gratuito.

### Pesquisa F — Governança e segurança

Definir medidas proporcionais ao porte do projeto:

- Registro da origem dos dados.
- Registro da data da coleta.
- Histórico de atualizações.
- Controle de acesso ao painel.
- Proteção dos arquivos CSV.
- Política de retenção.
- Processo de remoção.
- Registro das solicitações dos titulares.
- Proteção contra acesso não autorizado.

Verificar as orientações aplicáveis aos agentes de tratamento de pequeno porte, sem presumir dispensa de todas as obrigações da LGPD.

## 5. Resultado técnico esperado

Com base nas pesquisas, elaborar uma proposta de estrutura de dados para importação por CSV.

Avaliar campos como:

- nome_fantasia
- razao_social
- cnpj
- categoria
- subcategoria
- descricao_comercial
- bairro
- endereco_comercial
- telefone_comercial
- whatsapp_comercial
- site
- instagram
- horario_funcionamento
- imagem_principal
- fonte_dados
- url_fonte
- data_coleta
- data_ultima_verificacao
- status_validacao
- status_publicacao
- observacoes_internas

Não incluir automaticamente todos os campos.

Classificar cada campo como:

- Essencial.
- Opcional.
- Condicionado à confirmação.
- Não recomendado.
- Não publicar.

Justificar a classificação de cada campo.

Distinguir informações internas de informações exibidas publicamente.

## 6. Processo de alimentação recomendado

Comparar três processos:

### Processo 1 — Base oficial inicial

Identificar empresas em fontes oficiais, realizar filtragem e preparar registros candidatos.

### Processo 2 — Validação humana

Conferir os dados, verificar a origem, eliminar informações pessoais desnecessárias e identificar registros que exigem confirmação.

### Processo 3 — Confirmação pelo estabelecimento

Criar um fluxo simples para o responsável confirmar, corrigir e complementar as informações.

Avaliar se é juridicamente adequado publicar cada registro antes da confirmação do responsável e em quais condições.

Não presumir que um aviso de que os dados são públicos substitui uma base legal adequada.

## 7. Organização das fontes no projeto

Propor uma estrutura de documentação, preferencialmente:

docs/
  legal/
    LGPD_LEGISLACAO.md
    ANPD_LEGITIMO_INTERESSE.md
    ANPD_DIREITOS_TITULARES.md
    ANPD_AGENTES_PEQUENO_PORTE.md
    FONTES_DE_DADOS_E_LICENCAS.md
    POLITICA_DE_COLETA_E_PUBLICACAO.md
    MATRIZ_DE_DADOS_E_BASES_LEGAIS.md
    CHECKLIST_DE_CONFORMIDADE_MVP.md

Para cada fonte consultada, registrar:

- Título.
- Órgão responsável.
- URL oficial.
- Data de publicação.
- Data da última atualização, quando disponível.
- Data de acesso.
- Dispositivos ou seções relevantes.
- Resumo fiel.
- Aplicação ao projeto.
- Pendências de interpretação.

Não salvar apenas resultados de mecanismos de busca. Priorizar documentos oficiais completos, textos legislativos e guias originais.

Se um documento não puder ser baixado, registrar o link oficial e explicar a limitação.

Não substituir uma fonte oficial por um resumo de terceiros sem justificar.

## 8. Regras de confiabilidade

- Não inventar dispositivos legais.
- Não atribuir à ANPD orientações que não estejam nos documentos consultados.
- Não tratar interpretações como obrigações expressas da lei.
- Não afirmar que o projeto está juridicamente regular apenas com base nesta pesquisa.
- Identificar informações desatualizadas.
- Registrar divergências entre fontes.
- Identificar pontos que exigem avaliação de profissional jurídico.
- Distinguir fatos, interpretações e recomendações técnicas.

## 9. Entrega final

Apresentar:

1. Resumo executivo.
2. Análise jurídica aplicada ao projeto.
3. Comparação das fontes de dados.
4. Matriz de dados permitidos, condicionados e não recomendados.
5. Avaliação específica de MEIs.
6. Processo recomendado de coleta e validação.
7. Estrutura de CSV recomendada.
8. Documentação que deverá ser criada.
9. Riscos que impedem a publicação.
10. Checklist para liberar o MVP.

**Não alterar código, banco de dados ou arquivos de produção nesta etapa.**

Esta é uma etapa de pesquisa, documentação e alinhamento de requisitos. A implementação somente deverá começar após a análise e aprovação das decisões.