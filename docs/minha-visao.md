Projeto: Guia Comercial de Barretos
1. Objetivo do sistema
Criar uma plataforma informativa que permita:
- Encontrar negócios e serviços de Barretos.
- Pesquisar empresas pelo nome.
- Filtrar estabelecimentos por categoria e subcategoria.
- Encontrar negócios por bairro.
- Consultar endereço, telefone, WhatsApp e horário de funcionamento.
- Visualizar empresas em mapas.
- Acessar páginas individuais dos estabelecimentos.
- Divulgar empresas locais.

2. Estrutura do site
Página	Funcionalidade
Início	Apresentação e busca de negócios
Categorias	Listagem de segmentos comerciais
Explorar negócios	Catálogo com filtros
Detalhes do negócio	Perfil completo da empresa
Mapa	Localização dos estabelecimentos
Sobre	Informações sobre o projeto
Cadastro de empresa	Formulário para novos negócios

3. Sistema de filtros e pesquisa
Os filtros completos também poderão incluir:
- Aberto agora.
- Atendimento por WhatsApp.
- Atendimento presencial ou online.
- Avaliação dos usuários.
- Faixa de preço.
- Empresas com perfil verificado.

4. Página individual dos negócios


5. Requisitos
-Você mantém os dados em uma planilha.
-Exporta a planilha para CSV.
-Faz upload por uma área administrativa privada.
-O sistema valida os campos e identifica duplicidades.
-Registros válidos são armazenados em um banco de dados.
-O site consulta esses registros e aplica filtros dinamicamente.

6. Stack
Astro+Cloudflare Workers+Cloudflare D1+Cloudflare R2(opcional)+Registro.br(vai ser um subdominio do meu site principal(israelreispereira.com.br))

7. Onde obter os dados oficiais
alternativa1:
https://www.gov.br/receitafederal/pt-br/acesso-a-informacao/dados-abertos/cadastros
https://www.gov.br/receitafederal/dados
alternativa2:
https://developers.google.com/maps/documentation/places/web-service/place-details
https://developers.google.com/maps/documentation/places/web-service/data-fields
https://developers.google.com/my-business/content/overview
https://developers.google.com/maps/documentation/places/web-service/policies
alternativa3:
Você utiliza fontes oficiais para identificar e validar a existência cadastral dos estabelecimentos e complementa os dados comerciais manualmente.

8. Referencia de atributos passados pela IA do google mode:
Aqui estão todos os dados mantidos pelo Perfil da Empresa no Google, estruturados diretamente em variáveis organizadas por escopo (seguindo o padrão de nomenclatura snake_case comum em programação):

Informações Básicas e Identificação
• nome_da_empresa: Nome oficial do negócio exibido na busca e no Maps.
• categoria_principal: Ramo principal de atuação (ex: "Restaurante", "Advogado").
• categorias_secundarias: Outros ramos secundários para ajudar no ranqueamento.
• descricao_da_empresa: Resumo sobre o negócio, história ou diferenciais.
• data_de_abertura: Ano e mês em que a empresa começou a operar.

Localização e Áreas de Atendimento
• endereco_fisico: Logradouro, número, complemento, bairro, cidade, estado e CEP.
• coordenadas_geograficas: Latitude e longitude para fixar o alfinete exato no mapa.
• areas_de_cobertura: Cidades, bairros ou regiões atendidas em domicílio (caso não haja endereço físico).

Horários e Disponibilidade
• horario_regular: Dias da semana e horários de abertura e fechamento padrão.
• horario_especial: Alterações programadas para feriados, recessos ou eventos.
• horarios_especificos: Janelas de tempo para serviços específicos (ex: horário de entrega, happy hour, atendimento a idosos).

Canais de Contato e Links
• telefone_principal: Número principal para ligações de clientes.
• telefones_adicionais: Números secundários ou de outros setores.
• website_url: Link para a página web oficial da empresa.
• link_agendamento: URL para sistemas externos de reservas ou consultas.
• link_menu_cardapio: URL direta para o cardápio ou lista de preços (comum em restaurantes).

Conteúdo Visual e Atributos
• fotos_do_perfil: Imagens do logotipo, capa, fotos internas, externas e da equipe.
• videos_da_empresa: Vídeos curtos do local ou de demonstração de produtos.
• atributos_comodidades: Tags de características (ex: "Wi-Fi gratuito", "Acessível para cadeirantes", "Estacionamento gratuito").
• atributos_propriedade: Identificadores de inclusão (ex: "Empresa de proprietárias mulheres").

Portfólio Comercial
• lista_de_serviços: Títulos, descrições e preços dos serviços prestados.
• catalogo_de_produtos: Fotos, nomes, categorias, preços e links de compra para produtos físicos.

Interações e Reputação (Dados Públicos)
• historico_de_avaliacoes: Texto das resenhas deixadas pelos clientes.
• nota_media_estrelas: Média geral de 1 a 5 estrelas baseada nas avaliações.
• respostas_da_empresa: Textos de réplica enviados pelo proprietário às avaliações.
• perguntas_dos_usuarios: Dúvidas postadas pela comunidade no perfil.
• respostas_da_comunidade: Respostas dadas por outros usuários ou pela própria empresa.
• mensagens_chat: Histórico de conversas diretas e privadas via chat do Google.

Conteúdo Dinâmico
• postagens_atualizacoes: Textos e imagens de novidades do dia a dia.
• postagens_ofertas: Cupons de desconto, promoções com data de validade e termos.
• postagens_eventos: Título, data e horário de eventos promovidos pela empresa.

Métricas de Desempenho (Dados Privados / Insights)
• visualizacoes_totais: Quantidade de vezes que o perfil apareceu na busca ou no Maps.
• palavras_chave_busca: Termos exatos que os usuários digitaram para encontrar a empresa.
• cliques_no_website: Número de acessos direcionados ao site.
• chamadas_telefonicas: Quantidade de cliques no botão "Ligar".
• solicitacoes_de_rota: Cliques para abrir o GPS em direção ao endereço.
• mensagens_recebidas: Total de chats iniciados por clientes através do perfil.

9. Fluxo de importação
-Planilha-mestre
   Você adiciona, modifica e organiza as informações no Excel ou Google Sheets.
-Exportação CSV
   Exporta o arquivo em UTF-8, com cabeçalhos padronizados.
-Upload administrativo
   Acessa uma página privada, como /admin/importar, e envia o arquivo.
-Validação automática
   O sistema verifica campos obrigatórios, formatos, CNPJ, categorias e duplicidades.
-Prévia da importação
   Apresenta quantos registros serão inseridos, atualizados, ignorados ou rejeitados.
-Gravação no D1
   Os registros aprovados são persistidos no banco de dados.
-Atualização do catálogo
   O site passa a apresentar os dados importados e disponibiliza os filtros.

10. Regras de importação
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

11. Campos obrigatorios pensados(pode passar por reavaliação)
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

12. Exemplar de de csv
nome_da_empresa,cnpj,categoria_principal,bairro,telefone,whatsapp,preco_minimo,preco_maximo,website_url,fonte_da_informacao,data_da_verificacao,status_publicacao
Empresa Exemplo,12345678000190,Alimentação,Centro,1730000000,,25.00,80.00,,Cadastro próprio,2026-11-08,rascunho

13. Importação inteligente
-Inseridos
Novo registro
Empresas que ainda não existem no banco.
-Atualizados
Alteração
Empresas identificadas que receberam informações novas.
-Ignorados
Sem alteração
Registros já existentes e sem mudanças.
-Rejeitados
Erro
Registros inválidos ou incompletos em campos obrigatórios.