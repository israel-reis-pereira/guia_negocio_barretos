
# INFRASTRUCTURE

status: [planejamento / configurada / produção]
atualizado: [AAAA-MM-DD]

## HOSPEDAGEM
nome: [nome da hospedagem]
plano: [plano]
servidor: [tipo / configuração]
regiao: [região]
url_painel: [URL]

## DOMÍNIO E DNS
dominio: [domínio]
registrador: [registrador]
dns: [provedor]
nameservers: [referência]
registros: [A / AAAA / CNAME / MX / TXT]

## SSL
provedor: [emissor]
renovacao: [automática / manual]
validade: [data / monitoramento]

## BANCO DE DADOS
provedor: [provedor]
tecnologia: [tecnologia]
versao: [versão]
ambiente: [ambiente]

## ARMAZENAMENTO
provedor: [provedor]
tipo: [local / objeto / outro]
limites: [capacidade]

## EMAIL
provedor: [provedor]
smtp: [serviço]
spf: [status]
dkim: [status]
dmarc: [status]

## BACKUP
frequencia: [frequência]
retencao: [período]
destino: [local seguro]
ultimo_teste_restauracao: [data]

## VERSIONAMENTO
plataforma: [GitHub / GitLab / outra]
repositorio: [URL]
branch_principal: [branch]

## MIGRAÇÃO
origem: [origem]
destino: [destino]
estrategia: [estratégia]
rollback: [procedimento]

## CUSTOS
mensal: [valor]
anual: [valor]
limites: [limites relevantes]

REGRAS:
- Não armazenar senhas, tokens ou chaves.
- Não expor IPs ou detalhes sensíveis desnecessariamente.
- Registrar mudanças de infraestrutura.
- Confirmar backup antes de migrações.
