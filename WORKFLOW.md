# WORKFLOW.md — Gestão de Roadmap

**Versão:** v1.1 — 2026-06-15
**Status:** ativo
**Responsável:** Victor Leonardo Arimatea Queiroz — Diretor de Transformação Digital
**Repositório:** wkf-roadmap-geral (W04)

---

## Seção 1 — Identificação

| Campo | Valor |
|---|---|
| Nome do processo | Gestão de Roadmap |
| ID | W04 |
| Versão | v1.1 |
| Status | ativo |
| Data de criação | 2026-06-04 |
| Responsável | DTD/SETIS/SES-DF |
| Skill associada | S04 `skl-github-orquestracao` — depósito e atualização dos artefatos |
| Repositório de destino | `hub-entrada` (ROADMAP.md + staging.md) e P02 `hub-memoria` (relatório de sessão) |
| Ciclo fixo | Sextas-feiras à tarde — uma vez por semana |
| Repositório âncora | Este workflow é genérico e replicável. Versões específicas podem derivar dele sem alterá-lo. |

---

## Seção 2 — Missão e contexto organizacional

### Missão

Transformar o ROADMAP de lista de tarefas em instrumento estratégico vivo —
capaz de registrar o que foi construído, comunicar para onde o projeto vai,
e processar ideias emergentes antes que se percam.

### Por que este processo existe

Projetos evoluem de formas não planejadas. Ideias surgem em momentos inesperados.
Implementações acontecem sem que o planejamento original as previsse. Sem um
processo periódico de revisão, o ROADMAP acumula drift — fica descolado da
realidade — e perde sua função estratégica.

Este workflow resolve três problemas simultâneos:

1. **Drift de registro:** entregáveis implementados que não aparecem no ROADMAP
2. **Perda de ideias:** insights que surgem em conversas e nunca são capturados
3. **Desconexão estratégica:** o ROADMAP técnico não comunica valor para instâncias superiores

### Arquitetura de camadas do ROADMAP

O ROADMAP opera em três camadas com públicos distintos:

| Camada | Público | Pergunta central | Tom |
|---|---|---|---|
| **Interna** | Mantenedor + equipe futura | O que foi feito, como, por quê, status real | Técnico |
| **Estratégica** | SETIS, chefias, Fórum de Subsecretários | Que valor estamos gerando? | Executivo |
| **Pública** | Institucional, externo | O que a DTD faz pela SES-DF? | Institucional |

Cada entregável recebe um **estado de curadoria** que determina em quais camadas aparece:

| Estado | Símbolo | Camadas visíveis |
|---|---|---|
| `interno` | 🔒 | Apenas interna |
| `estratégico` | 📊 | Interna + estratégica |
| `público` | 🌐 | Todas as camadas |

### A Staging Area

A `staging.md` é o mecanismo central deste workflow. É um arquivo separado
dentro do `hub-entrada` que recebe dois tipos de entrada:

**Tipo 1 — Registros automáticos:** a S04 deposita ao final de cada operação
no ecossistema. Registram fatos consumados — algo foi feito.


**Princípio da staging (C9):**
A staging não é um repositório de tarefas — é uma camada de governança entre
ideias brutas e fatos operacionais. Um item na staging representa uma ideia que
ainda não foi avaliada quanto ao seu valor para o ecossistema. Nenhuma ideia avança
diretamente para o ROADMAP sem passar por aqui. A staging preserva o controle
do mantenedor sobre o que entra no ecossistema e garante que nenhuma decisão
de design seja tomada por impulso ou por acumulação silenciosa.

**Tipo 2 — Ideias capturadas:** qualquer manifestação de ideia identificada
em sessões com o Claude, seja por sinalização explícita do mantenedor ou por
mineração ativa do contexto pelo agente.

Nada na `staging.md` é oficial. Tudo aguarda processamento na sessão semanal.

> **Nota para agentes futuros:** caso a `staging.md` tenha crescido a ponto
> de comprometer a navegabilidade do `hub-entrada`, avaliar migração para
> repositório próprio `hub-staging`. Critério sugerido: mais de 50 itens
> ativos simultâneos ou arquivo acima de 500 linhas. Apresentar proposta
> ao mantenedor antes de executar.

### Quem pode acionar este workflow

- O Diretor de Transformação Digital — acionamento da sessão semanal
- O Claude — ao identificar que a staging.md acumulou itens suficientes
  para justificar sessão extraordinária (critério: mais de 10 itens Tipo 1
  ou qualquer ideia Tipo 2 com mais de 7 dias sem processamento)

---

## Seção 3 — Estado final esperado

Uma sessão bem-sucedida deste workflow satisfaz todos os critérios abaixo:

- [ ] Staging area lida integralmente — nenhum item ignorado
- [ ] Cada item da staging recebeu uma decisão explícita do mantenedor
- [ ] Itens aprovados migraram para a zona confirmada correta do ROADMAP
- [ ] Itens arquivados registram motivo e data no arquivo histórico da staging
- [ ] ROADMAP.md atualizado com estado de curadoria correto para cada entregável
- [ ] Resumo Executivo gerado para itens com estado `estratégico` ou `público`
  *(placeholder — aguarda criação do wkf-resumo-executivo)*
- [ ] Relatório de sessão produzido e encaminhado ao W03 para depósito no P02
- [ ] S04 acionada para depósito de todos os artefatos gerados
- [ ] Staging area limpa ao final — apenas itens em status `maturando` permanecem

---

## Seção 4 — Etapas do processo

| # | Etapa | Executor | Tipo | Entrada | Saída |
|---|---|---|---|---|---|
| 0 | Acionamento da sessão | Humano ou Claude | Manual | Dia da semana (sexta) ou critério extraordinário | Sessão iniciada |
| 1 | Escaneamento do ecossistema | Claude | Automatizada | sumario.md, backlogs, CHANGELOG, ROADMAP.md | Retrato fiel do estado real |
| 2 | Leitura da staging.md | Claude | Automatizada | staging.md completa | Lista estruturada de itens pendentes |
| 3 | Apresentação do estado real | Claude | Manual | Retrato + staging | Panorama apresentado ao mantenedor |
| 4 | Diálogo estratégico | Claude + Humano | Manual | Panorama apresentado | Visão estratégica emergente |
| 5 | Curadoria da staging | Humano (decidir) + Claude (executar) | Manual | Itens da staging + visão estratégica | Decisão para cada item |
| 6 | Atualização do ROADMAP | Claude | Automatizada em sessão autenticada | Decisões da curadoria | ROADMAP.md atualizado por camadas |
| 7 | Geração do Resumo Executivo | Claude | Manual | Itens estratégico/público aprovados | Rascunho do Resumo Executivo |
| 8 | Revisão do Resumo Executivo | Humano | Manual | Rascunho | Resumo Executivo aprovado |
| 9 | Relatório de sessão | Claude | Manual | Histórico completo da sessão | Relatório narrativo → W03 |
| 10 | Depósito via S04 | S04 (IA) | Automatizada em sessão autenticada | Todos os artefatos aprovados | Repositórios atualizados, staging limpa |

### Detalhamento das etapas críticas

#### Etapa 1 — Escaneamento do ecossistema

O Claude lê obrigatoriamente, nesta ordem:

```
GET hub-fonte/sumario.md          → versões e status de todos os repositórios
GET hub-entrada/CHANGELOG.md      → o que foi feito desde a última sessão
GET hub-entrada/ROADMAP.md        → estado confirmado atual
GET hub-entrada/staging.md        → itens pendentes de curadoria
```

O resultado é um **retrato fiel** — não interpretação, não julgamento.
Apenas: o que existe, em que versão, o que mudou, o que está pendente.

#### Etapa 4 — Diálogo estratégico

Esta é a etapa central do workflow. O Claude não é um formulário — é um
interlocutor que desafia a visão estratégica do mantenedor.

**Estrutura do diálogo:**

1. Claude apresenta o panorama sem julgamento
2. Claude faz até 3 perguntas provocadoras sobre o estado atual
3. Mantenedor responde livremente
4. Claude analisa as respostas e identifica implicações estratégicas
5. Claude faz novas perguntas se necessário
6. Visão estratégica do período emerge do diálogo

**Perguntas provocadoras — exemplos:**
- *"O que foi construído esta semana serve ao objetivo declarado no ROADMAP? Ou abrimos um caminho diferente?"*
- *"Há alguma implementação desta semana que muda a prioridade do que estava planejado?"*
- *"Das ideias na staging, qual resolve um problema que você já sentiu mais de uma vez?"*
- *"O que está no ROADMAP como 'próxima ação' ainda é a coisa mais importante a fazer?"*
- *"Se você tivesse que apresentar o ecossistema ao Secretário amanhã, o que diria em duas frases?"*

O diálogo encerra quando o mantenedor consegue responder com clareza:
*onde estamos, por que chegamos aqui, e para onde vamos*.

#### Etapa 5 — Curadoria da staging

Para cada item da staging, o mantenedor toma uma das quatro decisões:

| Decisão | Significado | Destino |
|---|---|---|
| **Aprovar** | O item entra no ROADMAP confirmado | Migra para zona confirmada com estado de curadoria |
| **Maturar** | A ideia tem potencial mas precisa de mais reflexão | Permanece na staging com nota de raciocínio |

**Critério de maturação (C10):** um item em status `maturando` só retorna à
curadoria quando: (a) o mantenedor trouxer nova evidência ou contexto que permita
decidir, ou (b) a sessão W04 seguinte identificar que a dependência declarada foi
resolvida. Itens que permanecem em `maturando` por mais de 3 sessões consecutivas
sem evolução recebem revisão obrigatória — com decisão entre manter, arquivar
ou rejeitar. Sem este critério, `maturando` vira sinônimo de "não decidido"
e acumula indefinidamente.

| **Arquivar** | A ideia foi avaliada e não avança agora | Vai para seção de arquivo da staging com motivo e data |
| **Rejeitar** | O item não pertence ao ROADMAP | Arquivado com status `rejeitado` — nunca deletado |

**Regra:** nenhum item pode permanecer em status neutro após uma sessão.
Todo item recebe uma decisão. `Maturar` é uma decisão válida — omissão não é.

#### Etapa 7 — Geração do Resumo Executivo (placeholder)

*Este artefato aguarda a criação do `wkf-resumo-executivo`.*

Por ora, o Claude gera um rascunho de texto livre com:
- Período coberto
- Principais entregas com estado de curadoria `estratégico` ou `público`
- Próximos passos relevantes para instâncias superiores
- Eventuais decisões que requerem atenção ou aprovação externa

Formato: Markdown estruturado, linguagem executiva, máximo 1 página A4.

---

## Seção 5 — Skills e subprocessos consumidos

| Recurso | Tipo | Papel | Link |
|---|---|---|---|
| skl-github-orquestracao | S04 | Depósito de todos os artefatos gerados na sessão | [→](https://github.com/victorarimatea/skl-github-orquestracao) |
| wkf-registro-sessao | W03 | Registro narrativo da sessão de revisão estratégica | [→](https://github.com/victorarimatea/wkf-registro-sessao) |
| hub-fonte/sumario.md | M01 | Fonte de verdade do estado do ecossistema (Etapa 1) | [→](https://github.com/victorarimatea/hub-fonte) |
| hub-entrada/staging.md | — | Staging area — receptor de registros e ideias | [→](https://github.com/victorarimatea/hub-entrada) |
| hub-memoria | P02 | Repositório de destino do relatório de sessão | privado |

---

## Seção 6 — Histórico de problemas

*Nenhum problema registrado — workflow em criação.*

Os problemas serão registrados aqui no formato P01, P02... à medida que
forem identificados em execuções reais, seguindo o padrão do ecossistema:
sintoma → causa raiz → solução → status.

---

## Seção 7 — Roadmap de automação

| Etapa | Status atual | Condição para próxima evolução |
|---|---|---|
| Escaneamento do ecossistema | 🔄 Manual — Claude lê via web_fetch | Automático quando GitHub MCP estiver disponível |
| Captura de ideias sinalizadas | 🔄 Manual — mantenedor sinaliza explicitamente | Idem |
| Mineração ativa de ideias | ❌ Não implementada | Implementar instrução na S04 após 3 execuções do workflow para calibrar critérios de detecção |
| Curadoria da staging | ❌ Manual — requer decisão humana | Permanece manual por design — decisão estratégica não é automatizável |
| Geração do Resumo Executivo | ❌ Placeholder — aguarda wkf-resumo-executivo | Criar wkf-resumo-executivo como workflow independente |
| Depósito via S04 | 🔄 Automático em sessões autenticadas | Idem |
| Ciclo fixo semanal | ❌ Não implementado — depende de lembrete manual | GitHub MCP + integração de calendário no longo prazo |

---

## Seção 9 — Histórico de versões

| Versão | Data | Tipo | Descrição |
|---|---|---|---|
| v1.1 | 2026-06-15 | Melhoria | Princípio da staging formalizado na Seção 2 (C9); critério de maturação adicionado à Etapa 5 (C10) — itens em `maturando` por 3+ sessões recebem revisão obrigatória |
| v1.0 | 2026-06-04 | Criação | Processo inaugural de gestão de roadmap com staging area, diálogo estratégico e três camadas de curadoria |

## Seção 8 — Referências e dependências

- M01 `hub-fonte` — convenções de nomenclatura e sumário do ecossistema
- S04 `skl-github-orquestracao` — protocolo obrigatório para toda operação no GitHub
- W03 `wkf-registro-sessao` — workflow irmão para registro narrativo da sessão
- P02 `hub-memoria` — repositório de destino dos relatórios de sessão
- `hub-entrada/ROADMAP.md` — documento principal gerenciado por este workflow
- `hub-entrada/staging.md` — staging area criada junto com este workflow

### Nota sobre o wkf-resumo-executivo

O Resumo Executivo é o artefato de saída da camada estratégica deste workflow.
Ele merece um workflow próprio — `wkf-resumo-executivo` — que defina estrutura,
linguagem, critérios de aprovação e processo de distribuição para SETIS e
instâncias superiores. Este workflow é dependência futura de W04 e deve ser
criado após as primeiras execuções reais, quando os padrões de conteúdo
estiverem mais claros.

### Nota sobre a mineração ativa de ideias na S04

A instrução de mineração ativa — busca de candidatos a ideia nas interlinhas
das conversas — será adicionada à S04 após 3 execuções deste workflow.
O objetivo é calibrar primeiro os critérios de detecção com base em casos
reais antes de automatizar. Implementar antes pode gerar ruído excessivo.
