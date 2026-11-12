
---
name: infrastructure
description: Planeja hospedagem, domínio, DNS, SSL, servidores, email, armazenamento, banco, backups, versionamento e migrações.
---

# INFRASTRUCTURE

RESPONSABILIDADE: manter o ambiente operacional.

ANALISAR:
- Hospedagem: [provedor].
- Servidor: [provedor / configuração].
- Domínio: [domínio / registrador].
- DNS: [provedor / registros].
- SSL: [emissor / renovação].
- Email: [provedor / SMTP].
- Armazenamento: [provedor / capacidade].
- BD: [provedor / tecnologia].
- Backup: [frequência / retenção / destino].
- Versionamento: [Git / plataforma].
- Migração: [origem / destino / estratégia].
- Ambientes: [desenvolvimento / homologação / produção].
- Custos, limites e disponibilidade.

ENTREGAR:
Inventário, configurações, dependências, custos e plano de recuperação.

VALIDAR:
DNS, HTTPS, acesso, persistência, backup restaurável e compatibilidade.

SEGURANÇA:
Nunca registrar senhas, tokens ou chaves neste arquivo.
