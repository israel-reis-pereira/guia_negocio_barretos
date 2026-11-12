
# WORKFLOW

Objetivo: definir responsabilidades, validação cruzada e economia de contexto.

## 1. MAPA DE ESPECIALIDADES

| Skill | Responsabilidades |
| discovery | Conceito, MVP, sumário, mapa mental, feedback, marketing, contrato |
| architecture | Stack, framework, CMS, Headless CMS, frontend, backend, BD, CRUD, arquitetura, fluxos, regras |
| infrastructure | Hospedagem, servidor, domínio, DNS, SSL, email, armazenamento, backup, versionamento, migração |
| development | WooCommerce, multisite, loja virtual, integrações, design, tratamento de erros |
| security-compliance | LGPD, credenciais, riscos, acessos, privacidade |
| validation | Testes, falhas, acertos, revisão técnica, critérios de aceite |
| release | Publicação, SEO, migração, homologação, infraestrutura |
| maintenance | Monitoramento, escalonamento, feedback, incidentes, correções |

## 2. VALIDAÇÃO CRUZADA

| Executor | Validador |
| discovery | Responsável + cliente |
| architecture | development |
| infrastructure | security-compliance |
| development | validation |
| security-compliance | validation |
| validation | architecture + security-compliance, conforme o risco |
| release | validation + infrastructure |
| maintenance | validation |

## 3. REGRAS DE VALIDAÇÃO

- PASS: evidências suficientes e critérios atendidos.
- FAIL: falha identificada.
- BLOCKED: falta informação, acesso ou dependência.
- N/A: verificação não aplicável, com justificativa.

Uma skill não pode aprovar a própria entrega como única evidência.

Falhas devem retornar à especialidade responsável.
Após correção, executar novamente os testes afetados.

## 4. ECONOMIA DE CONTEXTO

1. Ativar somente skills necessárias.
2. Consultar somente documentos relevantes.
3. Não repetir informações já documentadas.
4. Preferir skills a subagentes quando não houver paralelismo.
5. Investigar até duas tentativas de correção antes de solicitar decisão humana.
6. Atualizar somente documentos afetados.
7. Pesquisar fontes oficiais quando a informação puder mudar.
8. Diferenciar fatos, hipóteses e recomendações.
9. Não confundir aprovação técnica com aprovação do cliente.
10. Não executar ações irreversíveis sem autorização.

## 5. FLUXO PADRÃO

DISCOVERY
   ↓
ARCHITECTURE
   ↓
INFRASTRUCTURE + SECURITY
   ↓
DEVELOPMENT
   ↓
VALIDATION
   ↓
RELEASE
   ↓
MAINTENANCE

As etapas podem retornar às anteriores quando houver falhas.

## 6. RESPONSABILIDADE HUMANA

O responsável pelo projeto aprova:
- Escopo e mudanças.
- Orçamento e contratação.
- Decisões comerciais.
- Riscos aceitos.
- Tratamento de dados e responsabilidades legais.
- Publicação e alterações críticas em produção.

## 7. HISTÓRICO

Registrar alterações relevantes em CHANGELOG.md.
Registrar decisões técnicas em ARCHITECTURE.md.
Registrar falhas em records/FAILURES.md.
Registrar testes em records/VALIDATIONS.md.
Registrar solicitações em records/FEEDBACK.md.
