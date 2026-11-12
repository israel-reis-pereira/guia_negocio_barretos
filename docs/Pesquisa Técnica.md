Compreendido perfeitamente. Conforme as diretrizes fornecidas, elaborei a **Pesquisa Técnica Completa e o Planejamento Definitivo** para o projeto **Portfólio de Desenvolvimento e Diretório Inteligente de Barretos-SP**, estruturado exatamente nos moldes solicitados para orientar com rigor e clareza a futura implementação por outra IA, mantendo o escopo adequado para um desenvolvedor iniciante e fundamentando cada decisão técnica.

---

# PESQUISA TÉCNICA COMPLETA E PLANEJAMENTO DEFINITIVO

**Projeto:** Portfólio de Desenvolvimento e Diretório Inteligente de Barretos-SP

**Domínio:** `israelreispereira.com.br` | **Subdomínio:** `portfolio.israelreispereira.com.br` | **Caminho:** `/projetos/mapa-empresas-barretos`

**Data Efetiva da Pesquisa:** Outubro de 2026.

---

## 1. Resumo Executivo

Este documento consolida o planejamento técnico para a construção de um portfólio pessoal e de um diretório inteligente de estabelecimentos comerciais em Barretos-SP. O produto divide-se em três pilares: **Portfólio Público** (apresentação de projetos e aprendizados), **Diretório Público** (busca, filtros e listagem de empresas locais) e **Prospecção Privada Futura** (gestão comercial isolada). A arquitetura prioriza a simplicidade robusta, utilizando **Astro**, **TypeScript** e **Cloudflare Pages**, evitando complexidades prematuras como bancos de dados relacionais ou autenticação em servidor no MVP.

---

## 2. Recomendação Arquitetural Principal

* **Stack Tecnológica:** Astro + TypeScript + CSS nativo + Papa Parse + Zod + Vitest + Playwright.
* **Modelo de Implantação:** Hospedagem estática na **Cloudflare Pages**, integrada ao domínio principal gerenciado na Cloudflare e registrado no Registro.br.
* **Gerenciamento de Dados:** Pré-processamento de dados via CSV validados por esquema rígido antes da compilação estática (`JSON` versionado), mitigando os riscos de processamento pesado no lado do cliente e blindando a camada privada.

---

## 3. Auditoria Crítica dos Requisitos

* **Análise da proposta original:** A ideia inicial de importar CSVs diretamente no navegador via Papa Parse apresenta riscos de degradação de experiência caso o arquivo seja corrompido ou exceda limites de memória do cliente. A auditoria recomenda isolar a ingestão de dados para uma rotina de compilação ou validação estática prévia, mantendo o navegador focado na alta performance de busca e renderização.
* **Separação de Dados:** Fica estabelecido que nenhum dado de prospecção comercial privada ou credencial operacional residirá no diretório público do repositório Git.

---

## 4. Requisitos Funcionais e Não Funcionais

### Requisitos Funcionais (RF)

* **RF01:** Exibir páginas institucionais e de portfólio pessoal responsivas.
* **RF02:** Permitir busca textual por nome, categoria ou bairro no diretório de Barretos-SP.
* **RF03:** Permitir filtragem combinada por categorias de estabelecimentos.
* **RF04:** Apresentar os resultados de forma consistente em formato de cards e tabela acessíveis.
* **RF05:** Exibir o estado de verificação e a procedência dos dados exibidos para garantir transparência.

### Requisitos Não Funcionais (RNF)

* **RNF01 (Desempenho):** O carregamento inicial deve priorizar arquivos estáticos otimizados via CDN da Cloudflare, minimizando o envio de JavaScript desnecessário.
* **RNF02 (Acessibilidade):** Atender às diretrizes WCAG 2.2 no nível AA para navegação por teclado e contraste visual.
* **RNF03 (Segurança):** Ausência total de segredos no código de cliente e separação estrita de dados privados.

---

## 5. Comparação Detalhada das Tecnologias

| Critério / Tecnologia | HTML/CSS/TS puro | Astro + TypeScript | React + Vite + TS | Vue + Vite + TS | SvelteKit + TS |
| --- | --- | --- | --- | --- | --- |
| **JS Enviado ao Navegador** | Mínimo | Zero (por padrão em páginas estáticas) | Moderado (Runtime do React) | Moderado (Runtime do Vue) | Moderado (Runtime do SvelteKit) |
| **Complexidade para Iniciante** | Baixa | Baixa-Moderada | Moderada | Moderada | Moderada-Alta |
| **Adequação ao Portfólio/Estático** | Excelente | Ideal | Boa | Boa | Boa |
| **Integração com Cloudflare** | Manual/Simples | Nativa (Pages) | Simples | Simples | Requer adaptador específico |

* **Justificativa da Escolha:** O **Astro** foi selecionado por entregar HTML puramente estático para o portfólio e páginas de conteúdo, permitindo injetar ilhas de interatividade em TypeScript puro apenas onde os filtros e buscas do diretório exigirem, garantindo velocidade máxima e excelente legibilidade para um desenvolvedor iniciante.

---

## 6. Arquitetura Proposta

A aplicação será estruturada de forma modular, separando a apresentação visual das regras puras de tratamento de dados:

* `src/components/`: Componentes visuais reutilizáveis (Cards, Tabelas, Cabeçalhos).
* `src/layouts/`: Estruturas base de página.
* `src/lib/`: Funções puras de normalização, esquemas Zod e lógica de filtros.
* `src/pages/`: Rotas do Astro (incluindo o subcaminho `/projetos/mapa-empresas-barretos/index.astro`).

---

## 7. Registro de Decisões Architectural (ADR)

* **ADR-01: Uso do Astro como Framework principal.**
* *Problema:* Necessidade de alta performance em páginas estáticas e portfólio com curva de aprendizado acessível.
* *Decisão:* Adotar Astro com TypeScript.
* *Conseqüências:* Excelente SEO e carregamento veloz; menor quantidade de JavaScript desnecessário enviado ao cliente.



---

## 8. Investigação das Fontes de Dados

* **Dados Abertos do CNPJ (Receita Federal):** Úteis para validação cadastrais macro, porém carecem de geolocalização precisa e telefones comerciais atualizados de forma consistente. Devem passar por rigorosa limpeza e filtragem por município (Barretos-SP).
* **Fontes Locais e Sites Institucionais:** Utilizadas para complementação estrito-senso sob verificação manual humana, respeitando as condições de uso e a LGPD (Lei nº 13.709/2018).

---

## 9. Modelo de Planilha e CSV

O arquivo CSV de entrada para o diretório de Barretos deverá conter obrigatoriamente os seguintes campos normalizados:

* `id` (Identificador interno único, ex: `barretos-001`)
* `nome` (Nome oficial ou fantasia do estabelecimento)
* `categoria` (Segmento principal, ex: Alimentação, Saúde)
* `bairro` (Bairro localizado em Barretos-SP)
* `site` (URL válida iniciada em `https://` ou vazio)
* `status_verificacao` (`confirmado`, `nao_verificado`, `desatualizado`)

---

## 10. Pipeline de Importação, Validação e Deduplicação

1. **Leitura:** O arquivo CSV é processado por scripts utilitários utilizando validação estrita via **Zod**.
2. **Normalização:** Conversão de strings para minúsculas para fins de busca, remoção de espaços duplicados e validação de URLs.
3. **Deduplicação:** Identificação de registros duplicados por semelhança de nome e endereço, exigindo validação humana antes da consolidação no JSON de produção.

---

## 11. Modelo Conceitual dos Dados

* O modelo relacional conceitual separa entidades de **Empresa (`Business`)**, **Categoria (`Category`)** e **Fonte (`Source`)**, assegurando a rastreabilidade integral da procedência de cada dado publicado.

---

## 12. Mapa e Geolocalização

* **Diretriz para o MVP:** Como a base inicial pode não contar com coordenadas geográficas rigorosamente auditadas, o mapa interativo via **Leaflet** e tiles do **OpenStreetMap** fica condicionado à validação de coordenadas reais (`latitude` e `longitude`). Caso os dados geográficos estejam ausentes, a aplicação operará perfeitamente em modo de listagem/cards, sem quebrar a experiência do usuário.

---

## 13. Segurança, Privacidade e Acessibilidade

* **Segurança:** Isolamento total entre dados públicos e notas de prospecção comercial privada. Validação estrita de entradas para prevenir injeção de scripts (XSS).
* **Acessibilidade:** Conformidade com o W3C WAI, garantindo navegação completa por teclado (`Tab`, `Shift+Tab`), contraste adequado de cores e uso correto de elementos semânticos (`header`, `main`, `footer`, `article`).

---

## 14. Estratégia de Testes

* **Testes Unitários (Vitest):** Validação das funções puras de filtros, normalização de strings e validação de esquemas Zod.
* **Testes de Ponta a Ponta (Playwright):** Simulação de interações do usuário (busca textual, aplicação de filtros combinados e limpeza de estado na interface).

---

## 15. Plano Incremental de Implementação

* **Fase 1:** Configuração do ambiente local e validação do repositório.
* **Fase 2:** Construção da estrutura base em Astro e estilização minimalista.
* **Fase 3:** Implementação do motor de busca, filtros e renderização em cards/tabela.
* **Fase 4:** Integração do pipeline de dados via CSV/JSON.
* **Fase 5:** Execução de testes automatizados e implantação na Cloudflare Pages.

---

## 16. Arquitetura e Processo de Implantação

* **Cloudflare Pages:** Conexão direta com o repositório Git para builds automatizados.
* **DNS:** Configuração do subdomínio `portfolio.israelreispereira.com.br` apontando para o projeto Pages através do painel de DNS da Cloudflare, com gerenciamento de certificados SSL/TLS automáticos e regras de redirecionamento HTTPS obrigatórias.

---

## 17. Estimativa de Custos e Limitações

* **Custos:** R$ 0,00 fixos para hospedagem e infraestrutura básica (utilizando os planos gratuitos e nativos da Cloudflare Pages).
* **Limitações:** O diretório inicial depende de curadoria manual e dados limpos em CSV; não há backend persistente dinâmico no MVP.

---

## 18. Lista de Riscos Priorizados

* *Risco 1:* Inconsistência nos dados geográficos da cidade. *Mitigação:* Adotar o modo lista/cards como funcionalidade primária e o mapa como opcional condicionado à integridade das coordenadas.
* *Risco 2:* Complexidade excessiva para iniciantes. *Mitigação:* Fixar o uso de Astro e TypeScript sem dependências pesadas de bancos de dados externos.

---

## 19. Checklist de Publicação

* [ ] Build de produção executado sem erros no ambiente local.
* [ ] Validação de que nenhum dado privado ou credencial está exposto no código estático.
* [ ] Testes de responsividade em dispositivos móveis e navegação por teclado concluídos.
* [ ] Configuração correta do subdomínio e certificado HTTPS ativo na Cloudflare.

---

## 20. Documentação Mínima a Ser Criada no Repositório (`docs/`)

A IA de desenvolvimento deverá gerar obrigatoriamente a pasta `docs/` na raiz do projeto (`C:\Users\Williarts\Documents\projetos_teste\mapa-empresas-barretos\docs\`) contendo:

* `README.md` (Visão geral e comandos locais).
* `ARQUITETURA.md` (Explicação dos módulos e fluxo de dados).
* `DADOS-E-IMPORTACAO.md` (Regras do CSV e validação).
* `PUBLICACAO.md` (Instruções de deploy na Cloudflare).

---

## 21. Lista de Decisões Pendentes

* Confirmação da listagem inicial exata de estabelecimentos para compor a primeira carga validada do CSV de testes de Barretos-SP.

---

## 22. Referências Oficiais

* Documentação Oficial do Astro: [https://docs.astro.build/](https://docs.astro.build/)

* Documentação do TypeScript: [https://www.typescriptlang.org/docs/](https://www.typescriptlang.org/docs/)

* Documentação do Cloudflare Pages: [https://developers.cloudflare.com/pages/](https://developers.cloudflare.com/pages/)

* Documentação do Papa Parse: [https://www.papaparse.com/docs](https://www.papaparse.com/docs)

* Políticas de Tiles do OpenStreetMap: [https://operations.osmfoundation.org/policies/tiles/](https://operations.osmfoundation.org/policies/tiles/)


---

## 23. Prompt Final Completo para a IA de Desenvolvimento

*(Pronto para ser copiado e enviado à IA que executará a implementação no repositório local)*

```text
Você é um engenheiro de software sênior encarregado de implementar o projeto "Portfólio de Desenvolvimento e Diretório Inteligente de Barretos-SP", localizado em:
C:\Users\Williarts\Documents\projetos_teste\mapa-empresas-barretos

Siga rigorosamente estas instruções:
1. Inspecione a estrutura atual do repositório, verifique o arquivo index-preview.html se presente, e alinhe o código com as diretrizes do relatório técnico aprovado.
2. Crie a pasta "docs/" na raiz do projeto e preencha os arquivos mínimos obrigatórios (README.md, ARQUITETURA.md, DADOS-E-IMPORTACAO.md, PUBLICACAO.md) em português brasileiro.
3. Implemente o projeto de forma incremental utilizando Astro, TypeScript e CSS nativo:
   - Estruture o portfólio pessoal e a rota do diretório (/projetos/mapa-empresas-barretos).
   - Configure o pipeline de validação e leitura de dados estruturados.
   - Implemente busca textual, filtros por categoria, visualização em cards e tabela com total acessibilidade (WCAG).
4. Assegure a separação estrita entre dados públicos e privados, garantindo que nenhuma informação sigilosa vaze para a interface estática.
5. Execute os testes unitários e de integração utilizando Vitest para validar as regras de negócio e normalização.
6. Não invente dados comerciais falsos como se fossem reais e não adicione dependências complexas desnecessárias. Valide cada etapa antes de avançar.

```