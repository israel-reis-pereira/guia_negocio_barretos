Planejamento técnico — Guia de Negócios de Barretos
Minha avaliação inicial: a stack Astro + Cloudflare Workers + Registro.br é viável para esse projeto. Eu manteria as três tecnologias e evitaria adicionar serviços desnecessários na primeira versão.

Também concordo com sua decisão de ser o único responsável pela inserção dos dados. Isso simplifica bastante o sistema, reduz riscos de informações falsas e dispensa a construção de um painel administrativo complexo.

Existe, porém, uma distinção importante: precisamos separar dados reais, dados verificáveis e dados disponíveis para importação automatizada. Nem tudo o que aparece no Perfil da Empresa no Google pode ser obtido livremente por uma API.

A arquitetura que eu recomendo inicialmente é:
1. Você mantém os dados em uma planilha.
2. Exporta a planilha para CSV.
3. Faz upload por uma área administrativa privada.
4. O sistema valida os campos e identifica duplicidades.
5. Registros válidos são armazenados em um banco de dados.
6. O site consulta esses registros e aplica filtros dinamicamente.
Assim, você mantém controle editorial sem precisar cadastrar cada empresa diretamente no código.
1. Validação da stack tecnológica

Viável
 Stack aprovada, com um pequeno ajuste na arquitetura.

Astro
Interface, páginas, SEO e apresentação dos estabelecimentos.

Cloudflare Workers
Execução do site, API, processamento de CSV e regras de negócio.

Cloudflare D1
Banco de dados SQL persistente para empresas, categorias e regiões.

Registro.br
Registro do domínio .com.br e gerenciamento de sua configuração DNS.


Análise de cada tecnologia
Tecnologia	Avaliação	Justificativa
Astro	Aprovado	Excelente para sites informativos e páginas indexáveis.
Cloudflare Workers	Aprovado	Executa APIs e aplicações Astro.
Cloudflare D1	Recomendado	Banco SQL adequado para o catálogo.
Cloudflare R2	Opcional	Armazenamento de imagens e arquivos.
Registro.br	Aprovado	Registro do domínio. Não é hospedagem.

Validação documental:
- A documentação oficial do Astro confirma o suporte à implantação de aplicações estáticas e renderizadas sob demanda em Cloudflare Workers. 
  
  Docs+1
- A Cloudflare documenta o D1 como banco SQL serverless para dados relacionais, incluindo cadastros e listagens de produtos. 
  
  Cloudflare Workers docs+1
- O Registro.br oferece gerenciamento DNS, mas não hospeda o site. A publicação e hospedagem ficam sob responsabilidade da Cloudflare. 
  
  Registro.br+1
Minha decisão técnica: utilizar Astro + Workers + D1 + Registro.br. Adicionar R2 somente quando houver necessidade de hospedar fotos, logotipos e capas.

Documentação oficial para acompanhar:
- Astro — Deploy no Cloudflare
- Cloudflare — Conexão com bancos de dados
- Cloudflare — Opções de armazenamento
- Registro.br — Características técnicas

2. De onde obter os dados reais das empresas?
Aqui está a parte mais importante da pesquisa.

Identifiquei três caminhos diferentes, mas eles não possuem a mesma finalidade.
Alternativa A — Receita Federal: dados abertos do CNPJ
Fonte oficial recomendada
A Receita Federal disponibiliza dados cadastrais públicos de pessoas jurídicas e estabelecimentos.

Fonte oficial:
Receita Federal — Dados abertos de cadastrosReceita Federal — Repositório de dados abertosEntre os dados disponíveis estão:
- CNPJ;
- Nome empresarial;
- Nome fantasia;
- Situação cadastral;
- Data de abertura;
- CNAE principal;
- CNAEs secundários;
- Endereço;
- Município;
- CEP;
- Telefone;
- E-mail, quando informado.
O catálogo oficial do Governo Federal também documenta uma API de consulta CNPJ. Entretanto, essa API Conecta é voltada ao compartilhamento de dados com órgãos e entidades públicas, não sendo uma API pública irrestrita para qualquer desenvolvedor. 

Catálogo de APIs governamentais+1

Existe também um serviço de consulta CNPJ oferecido pela Receita Federal que pode ser contratado por pessoas jurídicas, com exigência de certificado digital e-CNPJ e condições comerciais próprias. A oferta gratuita de demonstração é limitada a 30 dias ou 3.000 consultas, conforme as condições publicadas. 

Serviços e Informações do Brasil+1

Minha recomendação: começar pelo download dos dados abertos, não pela integração com uma API paga.

Você poderá filtrar os estabelecimentos de Barretos pelo código oficial do município e pela situação cadastral.

Atenção: CNPJ ativo não comprova que o estabelecimento esteja efetivamente funcionando, atendendo ao público ou oferecendo determinado serviço. Também não significa que seja um negócio relevante para seu guia comercial.
Alternativa B — Google Places API
Não recomendo como fonte principal de importação
A Google Maps Platform possui a Places API, que disponibiliza informações sobre estabelecimentos.

Documentação oficial:
- Places API — Place Details
- Places API — Campos disponíveis
- Places API — Políticas e atribuições
Alguns campos disponíveis:
Informação	Disponibilidade
Nome do estabelecimento	Sim
Endereço	Sim
Telefone	Sim, conforme disponibilidade
Website	Sim
Coordenadas	Sim
Horário de funcionamento	Sim
Categoria principal	Sim
Avaliação média	Sim
Quantidade de avaliações	Sim
Nível de preço	Sim, quando disponível
Avaliações individuais	Até 5
Fotos	Até 10 referências de fotos


Google for Developers+3
Problema importante: a política do Google restringe a extração, cópia, armazenamento e redistribuição de conteúdo do Google Maps fora dos serviços autorizados. Isso inclui nomes de empresas, endereços e avaliações. O Place ID possui exceção específica para armazenamento. 

Google for Developers+1

Portanto, não recomendo construir um robô que consulte o Google, extraia milhares de empresas e grave permanentemente essas informações no D1.

Você pode usar a Places API em funcionalidades próprias, respeitando as regras e atribuições, mas não deve tratá-la como uma base livre para montar seu catálogo.
Alternativa C — Cadastro próprio com validação oficial
Recomendação principal
Esta é a alternativa que oferece maior controle.

Você utiliza fontes oficiais para identificar e validar a existência cadastral dos estabelecimentos e complementa os dados comerciais manualmente.

Exemplo:
Campo	Fonte
Nome empresarial	Receita Federal
CNPJ	Receita Federal
Situação cadastral	Receita Federal
CNAE	Receita Federal
Endereço cadastral	Receita Federal
Nome de divulgação	Verificação própria
Categoria comercial	Classificação própria
Bairro	Conferência do endereço
WhatsApp	Confirmação própria
Preços	Informação publicada ou confirmada pelo negócio
Horário de funcionamento	Verificação própria
Descrição comercial	Produção própria
Fotos	Material autorizado pelo estabelecimento

Isso permite manter a origem e a confiabilidade de cada informação.

Importante: a validação cadastral oficial comprova o registro e sua situação perante a Receita Federal. A confirmação de que a empresa está realmente operando exige uma verificação adicional.

3. Avaliação dos campos que você apresentou do Google
Sua lista é uma boa referência para o modelo de dados, mas não devemos reproduzi-la integralmente.

Algumas informações não são necessárias para o seu projeto e outras possuem limitações de acesso.
Grupo de informações	Minha decisão
Identificação da empresa	Manter
Categorias	Manter
Localização	Manter
Horários	Manter
Telefones e links	Manter
Fotos e vídeos	Manter, com autorização adequada
Comodidades	Manter
Serviços e produtos	Manter, se disponíveis
Avaliações	Adiar
Perguntas e respostas do Google	Não implementar inicialmente
Mensagens privadas	Excluir
Métricas privadas do Google	Excluir
Postagens e promoções	Adiar

Há três distinções importantes:
1. Business Profile API: é destinada à gestão de perfis empresariais aos quais o usuário autenticado possui acesso. Não é um catálogo aberto de todas as empresas da cidade. 
   
   Google for Developers+2
2. Places API: oferece dados públicos de lugares, mas tem restrições específicas de armazenamento e reutilização. 
   
   Google for Developers+1
3. Performance API: disponibiliza métricas de desempenho dos perfis que o comerciante pode acessar, não métricas privadas de qualquer empresa da cidade. 
   
   Google for Developers+1

4. Como deve funcionar a importação CSV?
Essa será a principal funcionalidade administrativa do projeto.

Minha recomendação é não depender de um cadastro manual dentro do site. Você terá uma planilha-mestre, que será sua fonte de trabalho.
Fluxo de importação
1. Planilha-mestre
   
   Você adiciona, modifica e organiza as informações no Excel ou Google Sheets.
2. Exportação CSV
   
   Exporta o arquivo em UTF-8, com cabeçalhos padronizados.
3. Upload administrativo
   
   Acessa uma página privada, como /admin/importar, e envia o arquivo.
4. Validação automática
   
   O sistema verifica campos obrigatórios, formatos, CNPJ, categorias e duplicidades.
5. Prévia da importação
   
   Apresenta quantos registros serão inseridos, atualizados, ignorados ou rejeitados.
6. Gravação no D1
   
   Os registros aprovados são persistidos no banco de dados.
7. Atualização do catálogo
   
   O site passa a apresentar os dados importados e disponibiliza os filtros.

4.1. Regras de importação
Precisamos estabelecer regras claras.
Situação	Comportamento
Empresa nova	Inserir
CNPJ já cadastrado	Não duplicar
Empresa existente com dados alterados	Atualizar os campos enviados
Campo opcional vazio	Gravar como NULL
Campo obrigatório vazio	Rejeitar registro
CNPJ inválido	Rejeitar registro
Categoria inexistente	Rejeitar ou sinalizar para correção
Linha duplicada no próprio CSV	Processar apenas uma vez
Empresa com situação cadastral não ativa	Não publicar automaticamente

Atenção à duplicidade: o CNPJ de 14 dígitos deve ser o identificador principal quando disponível.

Para negócios sem CNPJ informado, podemos utilizar uma chave alternativa composta por nome normalizado e endereço. Essa alternativa deve gerar uma sinalização para conferência manual, pois não garante identificar todas as duplicidades.
4.2. Campos obrigatórios e opcionais
Sugiro esta estrutura inicial:
Campo	Obrigatório?
nome_da_empresa	Sim
categoria_principal	Sim
descricao_da_empresa	Não
cnpj	Não
nome_fantasia	Não
situacao_cadastral	Não
endereco	Não
bairro	Não
cep	Não
latitude	Não
longitude	Não
telefone	Não
whatsapp	Não
website_url	Não
horario_funcionamento	Não
preco_minimo	Não
preco_maximo	Não
faixa_de_preco	Não
categorias_secundarias	Não
servicos	Não
fonte_da_informacao	Sim
data_da_verificacao	Sim
status_publicacao	Sim

Os três últimos campos são importantes para rastreabilidade e controle editorial.
4.3. Exemplo de CSV
Este é um modelo ilustrativo, não uma lista de empresas reais.
nome_da_empresa,cnpj,categoria_principal,bairro,telefone,whatsapp,preco_minimo,preco_maximo,website_url,fonte_da_informacao,data_da_verificacao,status_publicacao
Empresa Exemplo,12345678000190,Alimentação,Centro,1730000000,,25.00,80.00,,Cadastro próprio,2026-11-08,rascunho


Observe que o WhatsApp e o site estão vazios. O sistema deve interpretar esses valores como NULL, não como informações inexistentes confirmadas.
4.4. Importação inteligente
Eu implementaria quatro resultados possíveis:
Inseridos
Novo registro

Empresas que ainda não existem no banco.
Atualizados
Alteração

Empresas identificadas que receberam informações novas.
Ignorados
Sem alteração

Registros já existentes e sem mudanças.
Rejeitados
Erro

Registros inválidos ou incompletos em campos obrigatórios.
Outro detalhe importante: a importação deve ser transacional. Se houver erro durante a gravação, não devemos deixar metade de uma importação aplicada sem informar o ocorrido.

O sistema também deve gerar um relatório com os números das linhas e os motivos de rejeição.

5. Sistema de filtros dinâmicos
Aqui está uma decisão que influencia diretamente a modelagem do banco.

Não recomendo armazenar tudo em um único campo de texto.

Precisamos organizar as informações para que o usuário consiga combinar vários filtros.
Filtros da primeira versão
Filtro	Funcionamento
Pesquisa	Nome, descrição e serviço
Categoria	Alimentação, saúde, beleza etc.
Subcategoria	Segmento específico
Região	Região administrativa definida para o projeto
Bairro	Bairro do estabelecimento
Preço	Faixa de preço informada
Aberto agora	Conforme horário cadastrado
WhatsApp	Empresas com contato disponível
Atendimento	Presencial, delivery ou domiciliar

Um cuidado com o filtro de preço
Existem dois conceitos diferentes:
- Nível de preço: econômico, moderado ou alto.
- Preço real: valor mínimo e máximo de um produto ou serviço.
O Google Places possui um campo de nível de preço, mas isso não equivale a uma tabela de preços comerciais. Para o seu guia, o preço real deverá ser informado manualmente ou confirmado diretamente com o estabelecimento. 

Google for Developers+1

Eu criaria inicialmente os seguintes campos:
preco_minimo
preco_maximo
faixa_de_preco
preco_verificado_em


Também permitiria filtrar somente empresas que possuem informações de preço cadastradas.
Região e bairro
Precisamos separar esses conceitos:
- regiao: agrupamento geográfico criado pelo próprio portal.
- bairro: localização específica do estabelecimento.
Não recomendo inventar uma divisão oficial de regiões de Barretos. Primeiro devemos definir quais bairros pertencem a cada região, com base em uma classificação geográfica documentada ou explicitamente apresentada como classificação editorial do portal.

6. Banco de dados recomendado
Minha escolha seria o Cloudflare D1.

Estrutura inicial:
Database: guia_barretos


businesses
Cadastro principal de estabelecimentos.id · cnpj · name · slug · description · neighborhood_id · category_id · phone · whatsapp · price_min · price_max · status

categories
Categorias e subcategorias comerciais.id · name · slug · parent_id

neighborhoods
Bairros e agrupamentos regionais.id · name · region_id

regions
Regiões utilizadas pelos filtros.id · name · slug

services
Serviços oferecidos por cada empresa.id · business_id · name · description · price

import_history
Histórico de importações e resultados.id · filename · imported_at · inserted · updated · skipped · rejected


Essa estrutura permite adicionar funcionalidades posteriormente sem precisar reconstruir o banco.
Como os filtros funcionarão tecnicamente?
O navegador envia os parâmetros selecionados para uma API.

Exemplo:
/api/businesses?
category=alimentacao
&neighborhood=centro
&min_price=20
&max_price=100


O Worker recebe os parâmetros e executa uma consulta SQL no D1.

O resultado é devolvido ao Astro para apresentação.

O importante é que os filtros sejam combináveis, sem precisar carregar toda a base de empresas no navegador.

7. Segurança: somente você administra o catálogo
Essa exigência deve ser implementada desde o início.

Minha recomendação é utilizar o Cloudflare Access para proteger a área administrativa.

Documentação oficial: Cloudflare Access — documentação

O funcionamento será:
- O site público pode ser acessado por qualquer visitante.
- A rota /admin exige autenticação.
- Somente seu endereço de e-mail autorizado consegue acessar a administração.
- O upload CSV fica restrito à área protegida.
- O Worker valida novamente a autorização antes de processar o arquivo.
- As credenciais e os segredos ficam no ambiente seguro do servidor, nunca no código público.
Não é necessário criar um sistema completo de usuários, permissões e cadastro de clientes.

8. Arquitetura final proposta
Arquitetura do Guia Comercial
Visitante
Pesquisa e navega pelo catálogo.

Astro
Interface, páginas, SEO e filtros.

Cloudflare Workers
API, processamento e regras de negócio.

Cloudflare D1
Empresas, categorias, regiões e serviços.

Área administrativa privada

Cloudflare Access

Upload CSV

Validação e deduplicação

Gravação no D1


Representação lógica da arquitetura proposta.
O domínio registrado no Registro.br será conectado à Cloudflare. A documentação de Custom Domains permite associar o Worker ao domínio e configurar os certificados necessários. 

Cloudflare Workers docs+1

9. Planejamento de desenvolvimento
Eu dividiria o projeto em seis etapas.
Etapa	Entrega	Prioridade
1	Estrutura Astro e identidade visual	Alta
2	Banco D1 e modelagem SQL	Alta
3	Importação CSV e validação	Alta
4	Busca e filtros dinâmicos	Alta
5	Páginas individuais e SEO	Alta
6	Mapa, imagens e funcionalidades extras	Posterior

Escopo da primeira versão (MVP)
O que entra:
- Página inicial.
- Barra de pesquisa.
- Categorias e subcategorias.
- Filtros por região e bairro.
- Filtros por preço.
- Listagem de empresas.
- Página individual de cada estabelecimento.
- Integração com D1.
- Upload CSV privado.
- Validação e prevenção de duplicidades.
- SEO básico.
- Layout responsivo para celular e computador.
O que fica para depois:
- Avaliações dos visitantes.
- Comentários.
- Cadastro de empresas por terceiros.
- Planos comerciais.
- Anúncios patrocinados.
- Integração automática com APIs externas.
- Inteligência artificial para classificação de empresas.
Isso mantém o desenvolvimento enxuto.

10. Decisões importantes antes de começar
Existem quatro pontos que precisamos definir para evitar retrabalho.
1. Origem inicial dos estabelecimentos

Dados abertos da Receita Federal como base inicial.

Cadastrar empresas manualmente, uma por uma.

Receita Federal + complementação e verificação manual (recomendado).


2. Organização geográfica

Regiões criadas pelo portal, agrupando bairros.

Somente bairros, sem agrupamento regional.

Regiões e bairros como filtros independentes.


3. Sistema de preços

Faixa de preço + valores reais dos produtos e serviços.

Somente econômico, moderado e alto.

Somente valores reais informados.


4. Critério de publicação

Somente empresas verificadas manualmente (recomendado).

Todos os CNPJs ativos de Barretos que se enquadrem nas categorias selecionadas.

Confirmar decisões e montar especificação técnica
11. Minha conclusão
A ideia é tecnicamente viável e não exige uma arquitetura complexa.

Eu seguiria esta estratégia:
1. Receita Federal para identificação cadastral.
2. Verificação manual para confirmar a realidade comercial.
3. Planilha CSV como fonte principal de alimentação.
4. Cloudflare D1 para armazenamento permanente.
5. Astro para páginas rápidas e indexáveis.
6. Workers para filtros, API e importação.
7. Cloudflare Access para garantir que somente você possa administrar o catálogo.
Uma observação estratégica: não confunda quantidade de CNPJs com quantidade de negócios que merecem aparecer no guia. Seu diferencial será oferecer informações comerciais úteis, verificadas e organizadas — não simplesmente reproduzir um cadastro público.

O objetivo é construir um produto que você consiga manter sozinho, mesmo sendo iniciante, e que possa evoluir sem precisar trocar de stack.

Fontes oficiais utilizadas
Todas as referências técnicas e institucionais desta análise são de documentação oficial.
Instituição	Documentação
Astro	Integração Cloudflare
Cloudflare	D1 e bancos de dados
Cloudflare	Access e segurança
Google	Business Profile API
Google	Políticas da Places API
Receita Federal	Dados cadastrais abertos
Registro.br	DNS e infraestrutura

As fontes oficiais sustentam as capacidades e limitações técnicas descritas; a arquitetura e o planejamento são recomendações de engenharia, não garantias dos fornecedores.