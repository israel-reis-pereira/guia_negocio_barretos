Sim — dá para usar informações de um perfil do Google Empresa/Maps de forma segura, **desde que você não faça scraping, não copie conteúdo em massa e não trate dados pessoais sem base legal**. O caminho correto é usar a **Google Maps Platform / Places API** dentro das condições contratuais do Google, ou obter autorização direta do próprio estabelecimento.

## O que o link permite

O link `https://maps.app.goo.gl/...` é um link compartilhável do Google Maps. Ele pode levar a um estabelecimento no perfil do Google, mas **não autoriza extração automatizada** de nome, endereço, telefone, avaliações, fotos ou demais dados do perfil.

Os Termos do Google Maps Platform proíbem expressamente exportar, extrair ou fazer scraping de “Google Maps Content”, incluindo informações de locais e fichas comerciais; citam especificamente a proibição de copiar e salvar **nomes de empresas, endereços e avaliações de usuários**. [cloud.google](https://cloud.google.com/maps-platform/terms?hl=en_US)

## Riscos envolvidos

| Prática | Risco principal | Avaliação |
|---|---|---|
| Abrir o link manualmente e consultar informações | Uso pessoal/consulta | Geralmente aceitável, dentro das condições de uso do Google |
| Copiar dados manualmente para planilha ou cadastro | Pode violar os termos do Google se for para republicar, indexar ou revender | Evite armazenar e republicar |
| Criar robô para extrair perfis em massa | Violação contratual dos Termos do Google Maps | **Não faça** |
| Copiar avaliações, fotos, textos e dados de usuários | Violação contratual e possível problema de direitos autorais/dados de terceiros | **Não faça** |
| Usar Places API oficial e exibir dados na interface | Permitido se seguir licença, atribuição e restrições | **Recomendado** |
| Pedir autorização ao comércio para cadastrar dados | Base própria e transparente | **Recomendado** |

## LGPD: o que é dado pessoal

A LGPD protege dados de **pessoas naturais identificáveis ou identificáveis**. Dados corporativos como razão social, CNPJ, endereço comercial, telefone comercial e categoria de atividade normalmente não são, por si sós, dados pessoais. [planalto.gov](http://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)

Porém, podem se tornar dados pessoais quando identificam uma pessoa física, por exemplo:

- Nome do proprietário ou responsável.
- Telefone celular pessoal.
- E-mail pessoal.
- CPF.
- Foto ou biografia de uma pessoa.
- Avaliações que identifiquem usuários.
- Localização precisa vinculada a uma pessoa.

A LGPD exige base legal, finalidade específica, transparência, segurança, minimização de dados e direitos dos titulares. [planalto.gov](http://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)

## Como fazer sem problema judicial

### 1. Use a API oficial

Para buscar e exibir informações de estabelecimentos, utilize a **Places API** da Google Maps Platform, com uma chave própria, faturamento e limites de uso controlados.

Você pode consultar dados como:

- Nome do local.
- Endereço formatado.
- Categoria/tipo de negócio.
- Horário de funcionamento.
- Telefone comercial, quando disponível.
- Site.
- Avaliação média e quantidade de avaliações.
- Coordenadas.
- `place_id`.

A Places API pode ser usada inclusive sem um mapa do Google, desde que a aplicação forneça a atribuição exigida e não combine o conteúdo com um mapa de terceiros. [cloud.google](https://cloud.google.com/maps-platform/terms/maps-service-terms/index-20181015)

### 2. Não armazene conteúdo do Google

Não guarde em banco de dados, exporte, indexe ou republicue:

- Nome comercial.
- Endereço.
- Avaliações.
- Fotos.
- Descrições.
- Horários.
- Telefone.
- Coordenadas.

Os termos atuais proíbem pré-buscar, indexar, armazenar, redistribuir ou rehospedar esse conteúdo fora dos serviços do Google. [cloud.google](https://cloud.google.com/maps-platform/terms?hl=en_US)

A exceção prática é o `place_id`: o Google permite que ele seja armazenado, pois serve como identificador estável do local. [cloud.google](https://cloud.google.com/maps-platform/terms/maps-service-terms/index-20181015)

### 3. Estruture seu sistema assim

Para o diretório de empresas de Barretos, armazene apenas o mínimo necessário:

```text
empresa
├── id_interno
├── place_id_google
├── nome_informado_pelo_estabelecimento
├── categoria_principal
├── subcategoria
├── cnae
├── contato_comercial_informado
├── site_informado
├── consentimento_autorizacao
├── data_de_atualizacao
└── origem_do_dado
```

Em vez de copiar os dados do Google, salve o `place_id` e consulte a Places API em tempo real para exibir nome, endereço, telefone, horário e avaliações. Assim, o dado continua sendo fornecido e controlado pelo Google, e você não cria uma base replicada do conteúdo.

### 4. Peça autorização ao estabelecimento

A alternativa mais segura é cadastrar empresas por meio de um formulário próprio, em que o responsável informe:

- Nome fantasia e razão social.
- Categoria e subcategoria.
- Endereço.
- Telefone comercial.
- WhatsApp comercial.
- E-mail institucional.
- Site e redes sociais.
- Horário de funcionamento.
- Descrição dos serviços.
- Autorização para publicação.

Peça que a autorização seja feita por pessoa com poderes para representar a empresa e registre data, IP, versão do termo e finalidade do uso.

### 5. Separe dados da empresa e dados pessoais

Não misture dados do CNPJ com dados pessoais do sócio ou responsável. Se precisar cadastrar um responsável, informe claramente:

- Quem é o controlador dos dados.
- Qual a finalidade: validação e publicação do cadastro empresarial.
- Quais dados serão coletados.
- Por quanto tempo serão guardados.
- Como solicitar correção, exclusão ou acesso.

A LGPD prevê o direito do titular ao acesso facilitado às informações sobre o tratamento de seus dados. [planalto.gov](http://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)

## O que evitar

- **Não use Selenium, Puppeteer, Playwright ou scripts de scraping** para extrair dados do Google Maps ou do perfil da empresa.
- **Não compre ou use bases de dados raspadas** de Google Maps, Google Business Profile ou redes sociais.
- **Não replique avaliações, fotos ou comentários** de usuários em seu sistema.
- **Não cadastre dados pessoais de sócios** sem necessidade e sem base legal.
- **Não use dados de terceiros para prospecção em massa** sem verificar a origem, a licença e a finalidade permitida.
- **Não esconda a origem dos dados**: se exibir conteúdo do Google, mantenha a atribuição exigida.

## Recomendação prática

Para o seu sistema de categorias de empresas em Barretos, a arquitetura mais segura é:

1. O empresário cadastra ou reivindica o perfil.
2. Você armazena apenas dados empresariais autorizados e o `place_id`, se usar Google.
3. A Places API é consultada em tempo real para complementar ou exibir informações públicas.
4. Dados pessoais de responsáveis só entram com finalidade específica, aviso de privacidade e possibilidade de exclusão.
5. Avaliações e fotos permanecem no Google; seu sistema pode exibir um link ou componente autorizado, sem copiá-los.

## Fontes oficiais

- Lei Geral de Proteção de Dados Pessoais — LGPD, Lei nº 13.709/2018: [https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm](https://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm) [planalto.gov](http://www.planalto.gov.br/ccivil_03/_ato2015-2018/2018/lei/l13709.htm)
- LGPD — versão oficial no Portal da Legislação da Presidência da República: [https://legislacao.presidencia.gov.br/atos/?ano=2018&ato=293QzZ61UeZpWT79e&numero=13709&tipo=LEI](https://legislacao.presidencia.gov.br/atos/?ano=2018&ato=293QzZ61UeZpWT79e&numero=13709&tipo=LEI) [legislacao.presidencia.gov](https://legislacao.presidencia.gov.br/atos/?ano=2018&ato=293QzZ61UeZpWT79e&numero=13709&tipo=LEI)
- Google Maps Platform — Termos de Serviço, incluindo a proibição de scraping e cópia de nomes, endereços e avaliações: [https://cloud.google.com/maps-platform/terms?hl=en_US](https://cloud.google.com/maps-platform/terms?hl=en_US) [cloud.google](https://cloud.google.com/maps-platform/terms?hl=en_US)
- Google Maps Platform — Service Specific Terms, incluindo regras de cache e `place_id`: [https://cloud.google.com/maps-platform/terms/maps-service-terms](https://cloud.google.com/maps-platform/terms/maps-service-terms) [cloud.google](https://cloud.google.com/maps-platform/terms/maps-service-terms)
- Google Maps Platform — regras específicas da Places API, atribuição e cache: [https://cloud.google.com/maps-platform/terms/maps-service-terms/index-20181015](https://cloud.google.com/maps-platform/terms/maps-service-terms/index-20181015) [cloud.google](https://cloud.google.com/maps-platform/terms/maps-service-terms/index-20181015)
- Google Maps Platform — resumo dos serviços e condições aplicáveis: [https://cloud.google.com/maps-platform/terms/maps-services](https://cloud.google.com/maps-platform/terms/maps-services) [cloud.google](https://cloud.google.com/maps-platform/terms/maps-services)