# Análise breve

O material é uma especificação de planejamento para construir um portfólio de desenvolvimento e, dentro dele, um diretório público de empresas de Barretos-SP. A proposta também prevê, para uma etapa futura, uma área privada de prospecção comercial.

**Ideia central:** começar com um produto pequeno, publicável e fácil de manter; validar dados e necessidades reais; só então adicionar mapa, persistência, autenticação ou automações.

## Pontos fortes

- Separa claramente portfólio público, diretório público e prospecção privada.
- Dá prioridade à qualidade, procedência e atualização dos dados, em vez de presumir que uma fonte seja completa.
- Trata privacidade e segurança como decisões arquiteturais, não apenas como detalhes de interface.
- Define importação com prévia, validação, detecção de duplicatas e proteção dos dados existentes.
- Inclui acessibilidade, testes, desempenho, implantação, rollback e critérios verificáveis de publicação.
- Evita antecipar banco de dados, autenticação e outras funcionalidades sem necessidade concreta.

## Pontos de atenção

- **Escopo extenso:** há muitos requisitos para um primeiro projeto individual. É importante transformar o documento em entregas pequenas e não tentar executar todas as seções de uma vez.
- **Dependência de dados:** encontrar registros empresariais não garante obter endereços, telefones, sites e coordenadas corretos ou atualizados. A validação das fontes pode ser o maior trabalho do projeto.
- **Complexidade da importação:** o fluxo completo proposto é robusto, mas pode ser reduzido no MVP a um processo local de CSV/JSON, prévia e exportação de dados validados.
- **Mapa:** deve permanecer opcional até que existam coordenadas confiáveis e uma estratégia compatível com as políticas dos provedores cartográficos.
- **Arquitetura:** Astro com TypeScript é uma hipótese inicial razoável para um site predominantemente estático, mas a decisão deve ser confirmada pela comparação solicitada e por um protótipo.
- **Pesquisa técnica:** o texto exige documentação oficial atualizada. Portanto, esta análise não valida versões, preços, limites ou políticas das ferramentas citadas.

## Prioridade recomendada

1. Fechar o escopo do MVP e o modelo de dados.
2. Criar um pequeno conjunto de registros de teste, identificando dados fictícios e reais.
3. Fazer um protótipo responsivo com busca, filtros, cards e tabela.
4. Implementar importação e validação sem banco de dados.
5. Documentar as fontes e verificar a qualidade dos dados reais.
6. Só depois avaliar mapa e publicação definitiva.

**Conclusão:** o documento apresenta uma direção técnica consistente e cuidadosa. Seu maior risco não é a falta de tecnologia, mas tentar construir muitas capacidades antes de comprovar a qualidade dos dados e a utilidade do diretório. O melhor caminho é tratar o MVP como uma aplicação estática, com dados controlados e regras de negócio testáveis, mantendo a expansão condicionada a necessidades observadas.

---

# Documento original convertido

**# **Especificação de Planejamento — Portfólio de Desenvolvimento e Diretório Inteligente de Barretos-SP****

**## **1. Papel e comportamento esperado****

Atue como um arquiteto de software sênior, engenheiro de qualidade, especialista em desempenho web, acessibilidade, segurança, arquitetura de dados e implantação em Cloudflare.

Seu trabalho é orientar um desenvolvedor iniciante de forma exigente, didática, crítica e tecnicamente fundamentada.

Não aprove automaticamente minhas ideias. Identifique falhas, requisitos ausentes, riscos, custos de manutenção e alternativas melhores.

Não recomende uma ferramenta por popularidade, preferência pessoal, familiaridade com uma marca ou tendência do mercado. Toda escolha deve ser justificada pelas necessidades concretas do projeto.

Não implemente o projeto integralmente nesta etapa. O objetivo é produzir uma especificação técnica, comparações, decisões arquiteturais, planejamento incremental, critérios de aceite e uma lista de verificação para publicação.

Explique os conceitos técnicos necessários para que eu compreenda as decisões, mas não simplifique os problemas a ponto de omitir riscos relevantes.

Diferencie claramente fatos comprovados, recomendações, hipóteses, limitações conhecidas e decisões que ainda dependem de validação.

**## **2. Contexto do projeto****

Domínio principal: israelreispereira.com.br

- Provedor de registro do domínio: Registro.br.

- DNS e domínio principal: gerenciados pela Cloudflare.

- Subdomínio planejado: portfolio.israelreispereira.com.br.

- Caminho inicial de um projeto: /projetos/mapa-empresas-barretos.

- Cidade de referência: Barretos-SP, Brasil.

- Perfil do responsável: desenvolvedor iniciante que deseja aprender fundamentos, publicar projetos reais, construir um portfólio e evoluir tecnicamente sem comprometer a legibilidade e a manutenção.

A arquitetura deve permitir que o projeto comece pequeno, seja publicável e possa evoluir sem exigir uma reescrita desnecessária.

1/22

**## **3. Objetivos do produto****

**### **Objetivo A — Portfólio****

Criar um portfólio minimalista, responsivo, rápido e acessível, com apresentação pessoal, projetos, tecnologias, documentação e aprendizados.

O portfólio deverá demonstrar não apenas os resultados visuais, mas também a capacidade de tomar decisões técnicas, validar dados, testar funcionalidades, documentar limitações e resolver problemas reais.

**### **Objetivo B — Diretório público****

Criar uma aplicação que permita explorar estabelecimentos de Barretos-SP, com pesquisa textual, filtros, cards, tabela e mapa quando houver dados geográficos confiáveis.

O sistema deverá permitir consultar informações públicas, compreender a procedência dos registros e identificar quando uma informação está desatualizada, não verificada ou indisponível.

**### **Objetivo C — Prospecção privada****

Criar futuramente uma área privada para pesquisar oportunidades de serviços de desenvolvimento de software, sites, agendamentos, catálogos digitais e automações.

Não tratar ausência de site como prova de necessidade de software. Diferenciar fatos verificados, informações desconhecidas e hipóteses comerciais.

A camada pública nunca deve expor notas privadas, prioridades comerciais, credenciais ou informações internas.

A separação deve existir na arquitetura, nos dados publicados e nas permissões. Não considerar ocultação de campos na interface ou senhas implementadas somente no JavaScript como mecanismos suficientes de proteção.

**## **4. Pesquisa obrigatória****

Pesquise na web antes de tomar decisões técnicas.

Data de referência: 20 de outubro de 2026.

Use somente documentação oficial, documentação primária dos projetos, especificações técnicas oficiais, órgãos governamentais, portais oficiais de dados abertos e políticas oficiais dos provedores.

Não use blogs pessoais, conteúdo promocional de terceiros, vídeos de opinião, respostas de fóruns ou artigos sem autoria técnica como fundamento principal das decisões.

Se uma fonte oficial não estiver disponível, declare a lacuna. Não invente funcionalidades, preços, limites, garantias ou datas de atualização.

Diferencie:

Data de publicação da documentação. Data da última atualização da documentação. Data de atualização dos dados.

2/22

Data em que a pesquisa foi realizada.

Priorize estas fontes oficiais, verificando as versões vigentes:

Astro: https://docs.astro.build/

- Astro em português: https://docs.astro.build/pt-br/

- Cloudflare Workers: https://developers.cloudflare.com/workers/

- Cloudflare Pages: https://developers.cloudflare.com/pages/

- Cloudflare DNS: https://developers.cloudflare.com/dns/

- Papa Parse: https://www.papaparse.com/docs

- Leaflet: https://leafletjs.com/reference.html

- Política de tiles OpenStreetMap: https://operations.osmfoundation.org/policies/tiles/

- Política do Nominatim: https://operations.osmfoundation.org/policies/nominatim/

- Receita Federal — dados abertos: https://www.gov.br/receitafederal/pt-br/acesso-ainformacao/dados-abertos/cadastros

- SEADE — dados abertos de São Paulo: https://dadosabertos.sp.gov.br/

- Documentação do IBGE: https://servicodados.ibge.gov.br/api/docs/

- TypeScript: https://www.typescriptlang.org/docs/

- Vitest: https://vitest.dev/guide/

- Playwright: https://playwright.dev/docs/intro

- W3C WAI: https://www.w3.org/WAI/

ANPD: https://www.gov.br/anpd/pt-br

A lista é um ponto de partida, não uma restrição que justifique ignorar uma fonte oficial mais relevante.

Ao utilizar fontes, apresente links verificáveis e relacione cada afirmação técnica relevante à documentação que a sustenta.

Não afirme ter consultado uma página se não conseguiu acessá-la. Quando houver divergência entre documentação, identifique-a e explique o impacto na decisão.

**## **5. Comparação obrigatória de tecnologias****

Compare, no mínimo:

- HTML, CSS e TypeScript sem framework. Astro com TypeScript. React com Vite e TypeScript. Vue com Vite e TypeScript. SvelteKit com TypeScript.

Avalie:

- Desempenho e quantidade de JavaScript enviada ao navegador. Carregamento inicial e comportamento em dispositivos móveis. SEO, renderização e organização de rotas.

- Complexidade de aprendizado para um desenvolvedor iniciante. Organização de componentes e reutilização de código.

- Adequação a páginas predominantemente estáticas.

- Adequação a interfaces com filtros e interações complexas. Tratamento e validação de dados. Testabilidade e facilidade de depuração.

3/22

Manutenção a longo prazo.

Dependências e complexidade da configuração.

Integração com a Cloudflare.

Possibilidades de expansão para autenticação, API e persistência.

Custos operacionais e limitações que possam ser confirmados por fontes oficiais.

Apresente uma tabela comparativa com vantagens, desvantagens, riscos, casos de uso e justificativa para este projeto.

Não declare que uma tecnologia é mais rápida ou melhor em todos os cenários. Diferencie características arquiteturais de resultados que dependeriam de testes reais.

**### **5.1. Decisão arquitetural inicial****

Avalie criticamente a proposta de começar com Astro e TypeScript, adicionando interatividade somente onde necessária.

Considere esta divisão de responsabilidades como hipótese inicial:

Astro: páginas, navegação, portfólio, páginas dos projetos e metadados. TypeScript: regras de negócio, filtros, normalização e validação. CSS próprio: identidade visual e estilos. Papa Parse: leitura de CSV.

Zod: validação dos dados conforme um esquema. Leaflet: mapa interativo quando os dados geográficos forem confiáveis. Vitest: testes unitários.

Playwright: testes de ponta a ponta.

Cloudflare: hospedagem e, se necessário futuramente, execução de lógica no servidor.

Não aceite essa arquitetura sem avaliar sua adequação.

Explique em quais circunstâncias Astro deixaria de ser a melhor escolha e quando React, Vue ou outra alternativa poderia simplificar o projeto.

Considere especialmente a evolução para filtros encadeados, edição de registros, autenticação, sincronização e múltiplas telas interativas.

Estabeleça critérios observáveis para revisar a decisão. Não recomende uma migração preventiva baseada apenas em possibilidades futuras.

**## **6. Definição do produto e limites do MVP****

Separe explicitamente o projeto em três camadas.

**### **Camada 1 — Portfólio público****

Deve apresentar:

Apresentação profissional.

Habilidades e tecnologias. Projetos publicados.

Objetivos e aprendizados.

Documentação e decisões arquiteturais relevantes.

Links para demonstrações, repositórios e estudos de caso, quando disponíveis.

4/22

**### **Camada 2 — Diretório público de empresas****

Deve permitir:

- Consultar estabelecimentos publicados.

- Pesquisar por nome, categoria e outras informações disponíveis. Aplicar filtros combinados.

- Visualizar os mesmos resultados em cards e tabela.

- Consultar o mapa quando existirem coordenadas confiáveis.

- Identificar informações ausentes ou não verificadas.

- Consultar a procedência dos dados quando aplicável.

- Utilizar a aplicação mesmo quando o mapa ou um serviço externo estiver indisponível.

**### **Camada 3 — Prospecção privada futura****

Poderá permitir:

- Classificar oportunidades comerciais.

- Registrar tipos de solução que merecem investigação.

- Manter notas internas.

- Acompanhar a revisão de oportunidades.

- Registrar hipóteses a serem verificadas em contato comercial.

Essa camada não deve ser implementada como parte obrigatória do primeiro MVP.

**### **6.1. Critérios de delimitação****

Defina o que entra no MVP, o que fica para versões posteriores e o que não deve ser feito sem justificativa.

Considere fora do primeiro MVP:

- Cadastro público com publicação automática. Contas para múltiplos usuários. Banco de dados compartilhado.

- Scraping em massa de diretórios.

- Enriquecimento automático irrestrito por APIs.

- Pontuação automática baseada em suposições. CRM completo.

- Aplicativo móvel nativo.

Explique os custos de antecipar cada uma dessas funcionalidades.

**## **7. Domínio, DNS e implantação****

Compare os seguintes cenários:

****Cenário A — Portfólio com projetos em caminhos****

```

portfolio.israelreispereira.com.br/

portfolio.israelreispereira.com.br/projetos/rede-de-dados

portfolio.israelreispereira.com.br/projetos/mapa-empresas-barretos

```

****Cenário B — Diretório em subdomínio independente****

5/22

```

portfolio.israelreispereira.com.br/

```

```

empresas.israelreispereira.com.br/

```

Avalie simplicidade, isolamento, identidade própria, implantação, manutenção e possibilidade de evolução.

Considere como hipótese inicial publicar o diretório dentro do portfólio e avaliar a separação quando o produto adquirir necessidades próprias.

Explique a diferença entre subdomínio e caminho de URL.

Considere o Registro.br como registrador do domínio e a Cloudflare como responsável pelo DNS e pela infraestrutura de publicação, conforme o contexto informado.

Pesquise a documentação oficial vigente para definir o procedimento de implantação.

Compare Cloudflare Pages e Cloudflare Workers sem presumir que sejam equivalentes.

Apresente:

Diferenças relevantes entre os modelos.

- Compatibilidade com Astro.

- Processo de integração com Git. Requisitos de build.

- Configuração de domínio personalizado.

- Registros DNS necessários, quando aplicáveis.

- HTTPS e redirecionamentos.

- Rotas internas e página 404.

- Ambientes de teste e produção.

- Procedimento de rollback.

Limitações e custos que puderem ser confirmados oficialmente.

Não forneça valores de preços sem fonte oficial vigente. Não invente configurações DNS específicas que dependam do projeto real.

**## **8. Arquitetura e organização do repositório****

Proponha uma estrutura de diretórios que separe apresentação, regras de negócio, dados, testes e documentação.

Utilize a seguinte estrutura como referência inicial, adaptando-a quando necessário:

```

portfolio-barretos/

├── public/

│   ├── favicon.svg

│   └── images/

├── src/

│   ├── components/

│   │   ├── SiteHeader.astro

│   │   ├── SiteFooter.astro

│   │   ├── BusinessCard.astro

│   │   ├── BusinessFilters.astro

│   │   ├── BusinessTable.astro

│   │   └── ImportStatus.astro

│   ├── content/

```

6/22

```

│   │   └── projects/

│   ├── data/

│   │   └── businesses.example.json

│   ├── layouts/

│   │   └── BaseLayout.astro

│   ├── lib/

│   │   ├── csv-import.ts

│   │   ├── normalize-business.ts

│   │   ├── business-schema.ts

│   │   ├── filter-businesses.ts

│   │   └── errors.ts

│   ├── pages/

│   │   ├── index.astro

│   │   └── projetos/

│   │       ├── index.astro

│   │       └── mapa-empresas-barretos.astro

│   └── styles/

│       └── global.css

├── tests/

│   ├── unit/

│   └── e2e/

├── docs/

│   ├── ARCHITECTURE.md

│   ├── DATA-DICTIONARY.md

│   └── DEPLOYMENT.md

├── astro.config.mjs

├── package.json

├── tsconfig.json

└── README.md

```

A estrutura é uma proposta inicial, não uma obrigação de criar todos os arquivos imediatamente.

Explique:

A responsabilidade de cada diretório.

Quais módulos devem ser independentes da interface. Como evitar regras de negócio espalhadas pelos componentes. Como manter consistência entre os formatos de visualização. Como documentar decisões arquiteturais. Quando a estrutura precisará evoluir.

Não crie camadas abstratas sem uma necessidade concreta.

**## **9. Modelo de dados e contratos****

Defina um modelo consistente antes de iniciar a implementação.

**### **9.1. Entidade Business****

Avalie os seguintes campos:

7/22

|****Campo****|****Tipo proposto****|****Regra****|

|---|---|---|

|`id`|string|Identificador interno estável|

|`name`|string|Nome de exibição obrigatório|

|`categoryIds`|string[]|Uma ou mais categorias|

|`description`|string ou null|Descrição pública revisada|

|`address`|objeto ou null|Endereço estruturado|

|`phone`|string ou null|Telefone comercial verificado|

|`websiteUrl`|URL ou null|Site confirmado|

|`socialLinks`|objeto ou lista|Links públicos verificados|

|`coordinates`|objeto ou null|Latitude e longitude válidas|

|`sourceIds`|string[]|Referências das fontes|

|`verificationStatus`|enum|Estado de verificação|

|`lastVerifiedAt`|data ou null|Data da última verificação|

|`createdAt`|data|Data de inclusão|

|`updatedAt`|data|Última atualização|

Defina os tipos efetivos, as regras de validação e o significado de cada campo.

Utilize `null` para valores explicitamente desconhecidos quando isso fizer sentido para o contrato adotado. Diferencie valor ausente, valor desconhecido, valor inválido e resposta negativa.

Não interprete `websiteUrl: null` como prova de que a empresa não possui site.

**### **9.2. Entidade Category****

Considere:

```

id

```

```

name

slug

```

```

description

```

- `parentId` , quando necessário.

Avalie categorias iniciais como alimentação, saúde, beleza, automotivo, educação, serviços profissionais e comércio.

8/22

Evite criar uma taxonomia excessivamente complexa antes de observar as necessidades reais.

**### **9.3. Entidade Source****

Considere:

- `id`

- `name`

- `sourceUrl`

- `sourceType`

- `license`

- `collectedAt`

- `notes` .

Defina como registrar procedência, condições de uso, data de coleta e limitações de cada fonte.

Quando os campos de um estabelecimento forem obtidos de fontes diferentes, avalie como preservar a procedência por campo.

**### **9.4. Entidade ImportJob****

Considere:

- `id`

- `filename`

- `startedAt completedAt status`

- `totalRows`

- `acceptedRows`

- `rejectedRows`

- `duplicateRows errors` .

Defina como registrar os resultados de uma importação sem armazenar desnecessariamente o conteúdo integral dos arquivos.

**### **9.5. Entidade ProspectingRecord****

Considere:

- `businessId`

- `reviewStatus`

- `opportunityTypes priority notes`

- `lastReviewedAt` .

Essa entidade deve ser tratada como privada e não pode ser incluída inadvertidamente nos arquivos públicos.

Explique quais controles seriam necessários se futuramente existissem múltiplos usuários, autenticação ou persistência no servidor.

9/22

**## **10. Importação, validação e normalização****

Projete um fluxo de importação que aceite, conforme o escopo definido:

CSV.

JSON.

API autorizada.

Edição manual futura.

Não implemente todas as entradas automaticamente no MVP. Defina uma ordem de prioridade e justifique-a.

Considere Papa Parse para CSV, TypeScript para os contratos e Zod para validação.

Descreva o fluxo:

1\. Receber o arquivo ou conjunto de dados.

2\. Verificar formato, tamanho e estrutura.

3\. Interpretar os registros.

4\. Normalizar os valores.

5\. Validar campos e regras de negócio.

6\. Identificar possíveis duplicatas.

7\. Preservar a procedência.

8\. Produzir uma prévia.

9\. Apresentar erros e avisos.

10\. Permitir correção ou cancelamento.

11\. Aplicar a importação somente após confirmação.

12\. Apresentar um relatório final.

**### **10.1. Regras obrigatórias****

Não ignorar erros silenciosamente.

Não descartar registros inválidos sem explicar o motivo.

- Não substituir dados válidos automaticamente.

- Não eliminar possíveis duplicatas sem revisão.

- Não considerar um CSV sintaticamente válido como necessariamente válido para o modelo. Não interromper toda a importação por um erro isolado de linha, exceto quando a integridade do arquivo estiver comprometida.

- Não expor stack traces ao visitante.

- Preservar dados existentes quando uma importação falhar.

Defina como tratar separadores, aspas, acentos, quebras de linha, cabeçalhos inválidos, arquivos vazios, tipos incorretos, URLs inválidas e coordenadas fora dos intervalos permitidos.

Especifique as diferenças entre:

- Erro de parsing.

- Erro de validação. Aviso de qualidade. Possível duplicata. Registro pendente de revisão. Registro aceito.

10/22

**### **10.2. Relatório da importação****

O relatório deverá informar, no mínimo:

Total de linhas analisadas.

- Registros aceitos. Registros rejeitados.

Registros que precisam de revisão.

- Possíveis duplicatas.

Erros de interpretação do arquivo.

Motivos de rejeição. Próximas ações recomendadas.

Proponha mensagens compreensíveis, como:

- “Não conseguimos interpretar o arquivo. Confira o separador, o cabeçalho e as aspas.”

- “A linha 12 não possui um nome de estabelecimento.”

- “A localização desta linha está fora do intervalo permitido.”

- “Encontramos possíveis duplicatas. Revise os registros antes de confirmar a importação.”

- “Nenhum estabelecimento corresponde aos filtros.”

- “A importação foi analisada, mas alguns registros precisam de revisão.”

Defina critérios para garantir que as contagens do relatório sejam consistentes e auditáveis.

**## **11. Fontes de dados de Barretos-SP****

Não presuma que existe uma fonte única, completa, atualizada e autorizada que contenha todas as empresas da cidade com endereços, telefones, sites e coordenadas confiáveis.

Pesquise as fontes oficiais indicadas no item 4 e determine o que cada uma realmente oferece. Avalie especialmente:

- Dados abertos do CNPJ da Receita Federal.

- Dados empresariais e estatísticos do SEADE.

- Serviços e documentação de dados do IBGE, quando relevantes.

- Fontes públicas locais que possam ser verificadas.

- Sites oficiais dos próprios estabelecimentos, para complementação quando apropriado.

Diferencie:

1\. Base cadastral empresarial.

2\. Estatísticas econômicas.

3\. Diretório de estabelecimentos.

4\. Fonte de endereços.

5\. Fonte de coordenadas.

6\. Fonte de telefones e sites.

7\. Fonte de verificação atualizada.

Não apresente estatísticas agregadas como se fossem uma lista completa de pontos comerciais. Para cada fonte, documente:

Instituição responsável. URL oficial.

11/22

Formato disponível.

Campos relevantes.

Cobertura geográfica.

Data de referência dos dados, quando informada.

Frequência de atualização, quando documentada.

Licença e condições de uso. Limitações.

Adequação ao MVP.

Necessidade de limpeza, deduplicação ou complementação.

Se não for possível confirmar uma característica, marque-a como desconhecida.

**### **11.1. Estratégia incremental de dados****

Avalie esta sequência:

**#### **Fase A — Conjunto controlado de teste****

Criar entre 20 e 50 registros demonstrativos ou registros reais verificados. Identificar claramente quais são fictícios e quais são reais.

**#### **Fase B — Fontes estruturadas****

Investigar os dados abertos do CNPJ, do SEADE e outras fontes oficiais relevantes.

**#### **Fase C — Complementação****

Investigar informações públicas por fontes autorizadas, sites oficiais dos estabelecimentos e contribuições voluntárias.

**#### **Fase D — Verificação****

Definir procedimentos para revisar registros, corrigir informações desatualizadas e identificar estabelecimentos inativos.

Justifique a sequência e proponha critérios para avançar de uma fase para a seguinte.

**## **12. Geolocalização e mapa****

Avalie o Leaflet como biblioteca de visualização geográfica, sem atribuir a ele funções de catálogo de empresas ou geocodificação que não estejam comprovadas.

Defina os requisitos mínimos para um mapa confiável:

Coordenadas válidas.

Procedência da localização.

Indicação de localização aproximada, quando aplicável.

Atribuição adequada da fonte cartográfica.

Sincronização com a busca e os filtros.

Tratamento de falhas de carregamento.

- Alternativa em lista quando o mapa estiver indisponível. Comportamento responsivo e acessível.

Pesquise as políticas oficiais dos serviços do OpenStreetMap e do Nominatim.

12/22

Explique as limitações dos serviços públicos, os cuidados com uso em massa, as regras de atribuição e os requisitos aplicáveis à geocodificação.

Não presuma que um serviço gratuito possa ser utilizado sem limites, garantia de disponibilidade ou restrições.

Para o MVP:

- Priorize coordenadas confiáveis ou verificadas.

- Evite chamadas repetidas de geocodificação a cada visita.

- Avalie a persistência dos resultados conforme as condições de uso. Não invente coordenadas com base apenas no nome da empresa. Permita que o diretório continue útil sem o mapa.

Defina os critérios objetivos que determinam quando o mapa deve ser introduzido no produto.

**## **13. Privacidade, segurança e separação de dados****

Projete a arquitetura para impedir a exposição acidental de informações privadas.

Diferencie claramente:

- Dados públicos de estabelecimentos.

- Dados de procedência.

- Histórico técnico de importações. Anotações comerciais privadas. Credenciais e segredos operacionais.

Explique por que arquivos JSON publicados, código JavaScript entregue ao navegador e campos apenas ocultos na interface não podem ser considerados armazenamento privado.

No MVP, considere arquivos JSON versionados no Git como opção para dados públicos, desde que os dados tenham sido revisados e aprovados para publicação.

Considere a importação local no navegador como uma forma de produzir uma prévia ou um arquivo normalizado para download, sem exigir um servidor.

Se houver necessidade futura de sincronização, persistência compartilhada, contas ou autenticação, especifique as decisões adicionais necessárias para:

- Armazenamento.

- Autenticação.

- Autorização.

- Separação de permissões.

- Validação no servidor.

- Auditoria.

- Proteção de segredos.

- Retenção e exclusão de dados.

- Recuperação de falhas.

Avalie as obrigações relacionadas à LGPD e as orientações oficiais da ANPD quando houver tratamento de dados pessoais.

Não conclua que informações disponíveis publicamente estão automaticamente livres de obrigações de privacidade.

13/22

Não recomende coletar dados pessoais desnecessários.

Diferencie fatos observados, dados desconhecidos e hipóteses comerciais. Não permita que uma classificação automatizada apresente uma hipótese como verdade confirmada.

**## **14. Design, acessibilidade e experiência de uso****

Proponha uma direção visual minimalista, legível e consistente.

Considere:

Fundo branco ou cinza muito claro.

- Texto em grafite.

- Uma única cor de destaque.

- Tipografia sem serifa.

- Hierarquia visual consistente.

- Espaçamento generoso.

- Cards simples.

- Tabelas legíveis.

- Busca principal evidente.

- Filtros avançados organizados sem sobrecarregar a interface. Mapa opcional.

- Estados de carregamento, erro e lista vazia.

Avalie a necessidade de uma visualização separada ou de um layout dividido para o mapa.

**### **14.1. Acessibilidade****

Consulte as orientações oficiais do W3C WAI.

Defina critérios verificáveis para:

- Navegação por teclado. Foco visível.

- Estrutura semântica.

- Hierarquia de títulos. Rótulos de campos.

- Mensagens de erro acessíveis. Contraste.

- Uso em telas pequenas.

- Estados dinâmicos anunciados adequadamente.

- Alternativas textuais às informações do mapa.

- Uso sem dependência exclusiva de cores. Comportamento em diferentes tamanhos de tela.

Não considere responsividade apenas como ausência de rolagem horizontal.

Não use a ausência de site como indicador visual de qualidade ou confiabilidade de um estabelecimento.

**### **14.2. Estados da interface****

Defina o comportamento e as mensagens para:

14/22

Carregamento inicial.

- Carregamento malsucedido.

- Nenhum resultado.

Nenhum filtro aplicado.

- Nenhuma coordenada disponível.

- Mapa indisponível.

- Arquivo inválido.

- Importação parcialmente concluída.

- Registro desatualizado.

Registro pendente de verificação.

- Falha de uma fonte externa.

Cada estado deve explicar o que aconteceu e, quando possível, orientar a próxima ação.

**## **15. Testes, depuração e observabilidade****

Defina uma estratégia de testes compatível com a complexidade do MVP.

Considere Vitest para testes unitários e Playwright para testes de ponta a ponta, justificando o uso de cada ferramenta.

**### **15.1. Testes unitários****

Inclua:

- Normalização de campos. Validação de categorias.

- Validação de URLs.

- Validação de coordenadas.

- Campos ausentes.

- Detecção de duplicatas.

- Filtros combinados.

- Tratamento de erros.

- Consistência das contagens.

- Estados de verificação.

**### **15.2. Testes de integração****

Inclua:

- Importação de CSV de exemplo. Interpretação de JSON.

- Validação do modelo resultante.

- Relatório de erros.

- Preservação de dados válidos.

- Detecção de registros incompletos.

- Consistência entre os resultados da importação e os registros apresentados.

**### **15.3. Testes de ponta a ponta****

Inclua fluxos como:

Abrir o diretório.

15/22

Pesquisar por nome.

Combinar filtros.

Limpar filtros.

Alternar entre cards e tabela.

Importar um arquivo válido.

Tentar importar um arquivo inválido.

Revisar os erros apresentados.

Confirmar que uma falha não destruiu os dados anteriores.

Utilizar a aplicação quando o mapa não carrega.

**### **15.4. Desempenho e acessibilidade****

Defina como medir:

Carregamento inicial.

Quantidade e tamanho de recursos enviados ao navegador.

- Comportamento em dispositivos móveis.

- Custo de renderização de listas.

- Impacto do mapa.

- Uso de teclado.

- Contraste.

- Estrutura semântica.

- Comportamento em diferentes navegadores.

Não invente resultados de desempenho antes de executar medições.

**### **15.5. Regras de depuração****

- Nunca utilizar blocos `catch` vazios para ignorar falhas.

- Nunca substituir dados válidos por dados importados sem validação e confirmação. Diferenciar erros recuperáveis de erros que impedem uma operação.

- Incluir contexto útil nos logs, como operação, etapa, identificador da importação e linha afetada.

- Não registrar senhas, tokens ou dados privados desnecessários.

- Não apresentar stack traces ao visitante.

- Não interromper toda a importação por um erro isolado, exceto quando a integridade do arquivo estiver comprometida.

- Manter detalhes de diagnóstico fora das mensagens públicas. Testar explicitamente os caminhos de falha.

Defina critérios objetivos para considerar a aplicação suficientemente testada para publicação.

**## **16. Plano de execução incremental****

Proponha um plano com entregáveis concretos e critérios de conclusão.

Utilize estas etapas como hipótese inicial:

**### **Etapa 1 — Planejamento e requisitos****

Entregáveis:

Especificação do MVP.

16/22

Definição dos públicos.

Modelo de dados.

Dicionário de campos.

Regras de importação. Requisitos de privacidade.

Estados de erro. Critérios de aceite.

**### **Etapa 2 — Protótipo visual****

Entregáveis:

Protótipo navegável. Layout responsivo.

- Cards.

- Busca.

- Filtros.

- Tabela.

- Mensagens de erro. Estados vazios.

Validar a experiência antes de investir em complexidade arquitetural desnecessária.

**### **Etapa 3 — MVP funcional****

Entregáveis:

- Projeto Astro configurado, caso a escolha seja confirmada. TypeScript configurado.

- Modelo de dados validado.

- Importação CSV. Normalização.

- Validação.

- Detecção de possíveis duplicatas.

- Busca e filtros.

- Visualização em cards e tabela.

- Testes iniciais.

**### **Etapa 4 — Geolocalização e dados reais****

Entregáveis:

- Fontes documentadas. Dados com procedência. Coordenadas verificadas. Mapa funcional. Filtros sincronizados.

- Alternativa em lista.

- Tratamento de falhas cartográficas.

**### **Etapa 5 — Qualidade e segurança****

Entregáveis:

17/22

Testes automatizados.

- Revisão de acessibilidade.

Avaliação de desempenho.

- Revisão de dependências.

- Revisão de privacidade.

- Verificação da separação entre dados públicos e privados. Correção de falhas críticas.

**### **Etapa 6 — Publicação****

Entregáveis:

- Repositório versionado.

- Build de produção aprovado. Implantação de teste validada. Domínio configurado.

- HTTPS confirmado.

Rotas e página 404 testadas.

- Procedimento de rollback documentado.

- Instruções de instalação e publicação atualizadas.

Para cada etapa, apresente:

Objetivo.

Tarefas.

- Pré-requisitos. Entregáveis.

- Critérios de aceite.

- Principais riscos.

- Dependências entre tarefas. O que não deve ser iniciado ainda.

Apresente uma estimativa inicial de esforço apenas como hipótese de planejamento, indicando as variáveis que podem alterar o prazo. Não trate estimativas como garantias.

**## **17. Checklist de aceite e publicação****

Crie uma lista de verificação detalhada, organizada por categorias.

Cada item deve ser verificável. Não marque uma tarefa como concluída apenas porque existe código relacionado a ela.

**### **A. Requisitos e arquitetura****

- O escopo do MVP está documentado e separado das funcionalidades futuras. O modelo de dados e o dicionário de campos estão documentados. Cada campo possui tipo, significado e regra de validação.

- A separação entre dados públicos e dados privados foi implementada.

- As dependências e suas justificativas foram registradas.

- As decisões arquiteturais principais estão documentadas.

- Os critérios de revisão da stack estão definidos.

18/22

**### **B. Importação e qualidade dos dados****

CSV com separadores, acentos, aspas e quebras de linha foi testado. Arquivos vazios, corrompidos e com cabeçalhos inválidos são tratados. Campos obrigatórios e tipos são validados.

- Duplicatas são identificadas sem exclusão automática.

- A prévia informa registros aceitos, rejeitados e pendentes de revisão. Uma importação inválida não destrói os dados existentes.

- A origem, a data de coleta e o estado de verificação são preservados. Os relatórios apresentam contagens consistentes.

- Erros e avisos são compreensíveis.

**### **C. Interface e acessibilidade****

Busca e filtros funcionam em conjunto e podem ser limpos.

- Cards e tabela apresentam os mesmos resultados.

- A interface funciona em celular, tablet e desktop.

- Estados de carregamento, lista vazia e erro são claros. É possível navegar com teclado e identificar o foco.

- Contraste, títulos, rótulos e mensagens de formulário foram revisados. A aplicação continua utilizável quando o mapa não carrega.

- Os estados dinâmicos são comunicados adequadamente.

- As informações importantes não dependem exclusivamente de cores.

**### **D. Segurança, privacidade e conteúdo****

Nenhuma chave secreta ou credencial está no código publicado.

- Notas e prioridades de prospecção não aparecem nos arquivos públicos. As fontes e condições de uso dos dados foram verificadas.

- Informações comerciais publicadas têm procedência e estado de verificação. O tratamento de dados pessoais foi avaliado à luz da LGPD.

- Links externos e URLs apresentados ao usuário foram validados.

- Não há informações privadas expostas por arquivos estáticos ou recursos do cliente. Os procedimentos de retenção e exclusão estão definidos quando aplicáveis.

**### **E. Testes e desempenho****

Testes unitários das regras de negócio passam.

- Testes de importação e filtros passam.

- Fluxos críticos de ponta a ponta foram testados.

- Não há erros inesperados no console durante os fluxos normais testados.

- O tamanho dos arquivos, o carregamento e as dependências foram avaliados.

- Foram realizados testes em navegadores e tamanhos de tela diferentes.

- Erros de produção não expõem detalhes internos.

- Os resultados de desempenho foram medidos, não presumidos.

**### **F. Publicação e operação****

O build de produção termina sem erros.

- A implantação de teste foi validada antes da alteração do domínio público.

- O subdomínio está associado corretamente à aplicação na Cloudflare.

19/22

HTTPS e redirecionamentos foram verificados.

- Rotas, recarga de páginas internas e página 404 foram testadas.

- Existe um procedimento de rollback para a última versão estável.

- O README, as instruções de instalação e o processo de publicação estão atualizados. A versão publicada corresponde ao código aprovado.

Defina quais itens são bloqueadores absolutos para a publicação.

Critério mínimo: não publicar se a separação entre dados públicos e privados falhar, se a importação puder destruir dados válidos ou se houver falhas críticas de segurança.

Os demais itens devem possuir critérios de aceite e, quando não puderem ser concluídos, limitações conhecidas documentadas.

**## **18. Protótipo HTML e avaliação da implementação demonstrativa****

Avalie a possibilidade de utilizar um protótipo HTML autocontido como ferramenta de validação visual e funcional antes de iniciar a aplicação definitiva.

Se houver um protótipo disponível no material fornecido, analise-o criticamente sem presumir que seja código de produção.

Verifique:

- Estrutura HTML.

- Semântica.

- Responsividade.

- Busca e filtros.

- Uso de dados demonstrativos.

- Importação de CSV.

- Validação de cabeçalhos.

- Tratamento de erros.

- Validação dos registros.

- Tratamento de duplicatas.

- Segurança de URLs.

- Consistência entre contagens e resultados.

- Acessibilidade.

- Dependências externas.

- Comportamento quando uma biblioteca não está disponível.

Diferencie o que já funciona do que está apenas demonstrado visualmente e do que ainda precisa ser implementado.

Não afirme que um arquivo foi criado, testado, executado ou disponibilizado para download sem evidência real.

Caso seja útil, forneça um protótipo pequeno como entregável complementar, mas não permita que sua produção substitua a especificação técnica.

Dados fictícios devem estar claramente identificados e não podem ser apresentados como um levantamento real de empresas de Barretos.

20/22

**## **19. Riscos, contrapontos e decisões pendentes****

Crie uma matriz de riscos contendo:

- Risco.

- Probabilidade estimada.

- Impacto.

- Sinais de alerta.

- Medida preventiva.

- Plano de resposta.

- Etapa em que deve ser tratado.

Considere, no mínimo:

Escopo excessivo para um desenvolvedor iniciante.

- Escolha prematura de framework. Dependências desnecessárias.

- Dados empresariais incompletos ou desatualizados.

- Coordenadas incorretas.

- Duplicatas.

- Uso incompatível com licenças ou políticas de serviços. Indisponibilidade de serviços externos.

- Exposição acidental de informações privadas.

- Importações que corrompam dados válidos.

- Desempenho inadequado em dispositivos móveis.

- Falhas de acessibilidade.

- Implantação incorreta. Ausência de estratégia de rollback. Dificuldade de manutenção.

Apresente também os argumentos contrários às principais recomendações.

Para cada decisão importante, responda:

1\. Qual problema ela resolve?

2\. Quais alternativas foram consideradas?

3\. Qual é o custo de adotá-la?

4\. Qual é o custo de não adotá-la?

5\. Que evidência sustenta a escolha?

6\. Em que circunstâncias a decisão deve ser revista?

Não transforme possibilidades futuras em requisitos obrigatórios do MVP.

**## **20. Documentação final a ser produzida****

Organize a resposta final como uma especificação técnica que possa ser salva no repositório e utilizada durante o desenvolvimento.

Produza, nesta ordem:

1\. ****Resumo executivo:**** visão do produto, objetivos e recomendação inicial.

2\. ****Requisitos:**** funcionais, não funcionais e restrições.

3\. ****Escopo do MVP:**** o que entra, o que fica para depois e o que está explicitamente fora.

21/22

4\. ****Pesquisa técnica:**** fontes oficiais consultadas, achados, limitações e datas relevantes.

5\. ****Comparação de tecnologias:**** tabela completa e análise crítica.

6\. ****Decisão arquitetural:**** recomendação justificada, alternativas e critérios de revisão.

7\. ****Domínio e implantação:**** comparação de Cloudflare Pages e Workers, DNS, Git e publicação.

8\. ****Arquitetura do repositório:**** diretórios, responsabilidades e dependências.

9\. ****Modelo de dados:**** entidades, campos, tipos, validações e relações.

10\. ****Importação:**** fluxo, regras, estados de erro, duplicatas e relatórios.

11\. ****Fontes de dados:**** cobertura, procedência, licenças, atualização e limitações.

12\. ****Geolocalização:**** critérios para o mapa, coordenadas e políticas dos serviços.

13\. ****Privacidade e segurança:**** separação entre dados públicos e privados.

14\. ****Design e acessibilidade:**** princípios e critérios de aceite.

15\. ****Testes e depuração:**** estratégia, cenários e critérios de qualidade.

16\. ****Plano de execução:**** etapas, dependências, entregáveis e estimativas.

17\. ****Checklist de publicação:**** lista detalhada e bloqueadores.

18\. ****Matriz de riscos:**** prevenção, sinais de alerta e respostas.

19\. ****Decisões pendentes:**** questões que realmente precisam ser resolvidas antes da implementação.

20\. ****Próxima ação recomendada:**** a menor tarefa concreta que permita avançar com segurança.

Inclua exemplos de estruturas de dados, contratos e fluxos quando eles ajudarem a eliminar ambiguidades. Não produza código de aplicação completo, nem implemente o diretório inteiro nesta etapa.

**## **21. Regras finais de qualidade****

Pesquise antes de recomendar.

- Utilize fontes oficiais e links verificáveis.

- Não invente resultados de pesquisa.

- Não invente funcionalidades, preços ou limites.

- Não confunda estatísticas empresariais com um diretório geolocalizado.

- Não confunda ausência de informação com informação negativa.

- Não trate dados públicos como automaticamente livres de restrições.

- Não considere o mapa obrigatório quando as coordenadas não forem confiáveis.

- Não introduza um banco de dados apenas por antecipação.

- Não implemente autenticação sem uma necessidade concreta.

- Não exponha dados privados em arquivos estáticos.

- Não adicione ferramentas sem justificar o custo e a responsabilidade que elas introduzem.

- Não recomende migração de framework sem critérios observáveis.

- Não trate protótipos como sistemas prontos para produção.

- Não considere um recurso concluído sem definir como verificar seu funcionamento.

- Explique as decisões com linguagem acessível, mas tecnicamente precisa.

- Apresente os contrapontos relevantes, mesmo quando contrariarem a recomendação inicial.

- Separe fatos documentados, inferências, recomendações e pontos ainda não confirmados. Não use uma estimativa de esforço como promessa.

- Priorize simplicidade, legibilidade, segurança, qualidade dos dados e evolução incremental.

****Resultado esperado:**** uma especificação técnica fundamentada que permita iniciar o desenvolvimento com escopo controlado, compreender as decisões arquiteturais, validar a viabilidade das fontes de dados, reduzir riscos e publicar uma primeira versão útil, sem construir prematuramente um sistema maior do que o necessário.

22/22