---
name: start-project
description: Skill para fundar um novo projeto do zero com IA, usando Spec-Driven Development leve. Use quando o usuário quiser começar um novo projeto (webapp, automação, script, API), precisar montar a fundação antes de codar, ou quiser definir spec, stack, convenções e tarefas antes da primeira linha de código. Acione também quando o usuário mencionar "começar projeto", "novo webapp", "setup inicial", "estrutura do projeto", "nova automação" ou qualquer variação.
---

# Start Project (SDD Leve)

Skill para fundar projetos do zero de forma estruturada, antes de qualquer linha de código de feature.

Usado **uma única vez por projeto** — numa conversa dedicada de fundação. Ao final, todos os artefatos estarão prontos e o usuário fecha este chat e começa o projeto com base no que foi produzido aqui.

O processo funciona em cinco fases:

1. Capturar a ideia sem assumir nada
2. Construir a `spec.md` — o **quê** e o **porquê**, sem tecnologia
3. Construir a `plan.md` + `constitution.md` — o **como** técnico e as regras imutáveis
4. Gerar `tasks.md` e estrutura de pastas
5. Validar e entregar o pacote completo

Seu trabalho é identificar onde o usuário está nesse processo e avançar etapa a etapa. Se ele chegar com "quero fazer um app de X", começa do zero. Se já tiver uma ideia clara mas nenhum documento, pula direto para a Fase 2. Seja flexível.

Se o usuário disser "pode pular as perguntas, já sei o que quero", vá em frente sem cerimônia.

---

## Comunicando com o usuário

Preste atenção no nível técnico pelo contexto:

- Se o usuário usa termos como "monorepo", "RLS", "edge functions", "cronjob" naturalmente — use jargão técnico livremente.
- Se o usuário descreve tudo em linguagem de produto ("quero que o usuário consiga fazer X") — explique termos técnicos brevemente antes de usá-los.

Em caso de dúvida, uma definição rápida entre parênteses resolve.

---

## FASE 1 — Captura da Ideia

Entenda o que o usuário quer construir. Não escreva nada ainda. Faça uma rodada de perguntas, espere as respostas, e só então pergunte o que ainda estiver em aberto. Não despeje tudo de uma vez.

**Perguntas essenciais:**

1. O que este projeto faz e qual problema ele resolve?
2. Para quem é? (uso pessoal, equipe interna, produto público?)
3. Quais são as 3–5 funcionalidades mais importantes para o MVP?
4. Existe alguma integração externa essencial? (APIs, autenticação, banco de dados, serviços externos?)
5. O usuário tem preferência de stack ou quer uma sugestão?

Extraia o máximo da mensagem inicial e pergunte só o que realmente está em aberto. Quando o usuário responder, confirme seu entendimento em 2–3 frases antes de avançar.

---

## FASE 2 — `spec.md` (O Quê e o Porquê)

> **Regra de ouro desta fase:** nenhuma tecnologia, nenhum framework, nenhuma decisão técnica entra aqui. Apenas produto.

Com as respostas em mãos, gere o `spec.md`. Este documento descreve intenção — ele deve continuar válido mesmo que você troque React por Vue ou Python por Go amanhã.

**Estrutura do `spec.md`:**

```markdown
# spec.md

## Visão Geral
O que é este projeto e qual problema ele resolve. 2–4 frases.

## Usuários-Alvo
Quem vai usar, em que contexto, com que frequência.

## Funcionalidades do MVP
Lista priorizada do que entra na primeira versão. Para cada item:
- Nome da funcionalidade
- O que o usuário consegue fazer com ela
- Critério de aceite: como saber que está pronto?

## Fluxos do Usuário
Os caminhos principais que um usuário percorre no produto.
Descreva em linguagem natural, não em diagramas técnicos.

## Fora do Escopo
O que explicitamente NÃO entra no MVP.
Esta seção é tão importante quanto as anteriores — ela evita que a IA invente coisas.

## Regras de Negócio
Restrições, lógicas e comportamentos que não são óbvios.
Ex: "um usuário só pode ter um projeto ativo por vez", "o relatório só é gerado se houver ao menos 10 registros".

## Perguntas em Aberto
Use [PRECISA DEFINIR: pergunta específica] para qualquer ambiguidade que ainda não foi resolvida.
Não assuma. Se não foi especificado, marque aqui.
```

Apresente o `spec.md` ao usuário e peça confirmação antes de seguir. Diga algo como: *"Aqui está a spec. Leia com atenção — este documento vai guiar todas as decisões técnicas. Corrija qualquer coisa que não refletir sua visão. Nenhum [PRECISA DEFINIR] deve sobrar antes de avançar."*

Só avance quando o usuário aprovar e não houver mais marcadores `[PRECISA DEFINIR]`.

---

## FASE 3 — `plan.md` + `constitution.md`

Esta fase tem duas entregas separadas com responsabilidades distintas.

### 3A — `constitution.md` (Regras Imutáveis)

A `constitution.md` é o DNA do projeto. É lida pela IA em **toda conversa futura** e define o que nunca pode ser violado. Diferente de convenções de estilo, ela contém **gates** — checagens que a IA deve fazer antes de escrever qualquer código.

**Estrutura da `constitution.md`:**

```markdown
# constitution.md

## Princípios Fundamentais
Descreva em 3–5 frases a filosofia do projeto.
Ex: "Este projeto prioriza legibilidade sobre performance. Nenhuma abstração deve ser criada antes de existir pelo menos 3 usos reais dela."

## Stack Definida
Liste cada camada com a escolha feita e o motivo em uma linha.
| Camada       | Escolha         | Motivo                          |
|---|---|---|
| Framework    | Next.js 14      | App Router, RSC, boa integração com Vercel |
| Linguagem    | TypeScript      | Tipagem estrita reduz bugs em runtime |
| ...          | ...             | ...                             |

## Convenções de Código
- Linguagem e tipagem (ex: TypeScript strict, sem `any` sem justificativa)
- Onde cada tipo de arquivo vive (componentes, hooks, services, types)
- Padrão de estilo (ex: Tailwind apenas, sem CSS inline)
- Padrão de fetch de dados
- Padrão de formulários e validação
- Convenções de nomenclatura (ex: componentes PascalCase, hooks camelCase com prefixo `use`)
- O que nunca fazer (ex: nunca chamar API diretamente de um componente, sempre usar a camada /services)

## Gates de Implementação
Antes de escrever código para qualquer feature, a IA deve verificar:

### Gate de Simplicidade
- [ ] A solução usa o menor número de arquivos e camadas possível?
- [ ] Existe abstração sendo criada sem 3+ usos reais?
- [ ] Alguma dependência nova está sendo adicionada sem necessidade clara?

### Gate de Arquitetura
- [ ] O arquivo está sendo criado no lugar correto conforme as convenções?
- [ ] A feature está usando os padrões definidos (fetch, forms, estilo)?
- [ ] Alguma regra de negócio da spec.md está sendo ignorada ou assumida?

### Gate Anti-Invenção
- [ ] A IA está adicionando algo que NÃO foi pedido?
- [ ] Alguma funcionalidade "fora do escopo" da spec está sendo implementada?

Se algum gate falhar, a IA deve parar, apontar o problema e perguntar antes de continuar.

## O Que Nunca Fazer
Lista explícita de anti-padrões proibidos neste projeto.
Ex:
- Nunca usar `any` em TypeScript
- Nunca criar componentes com mais de 200 linhas sem dividir
- Nunca fazer chamada de API fora da pasta /services
- Nunca commitar sem atualizar o PROGRESS.md
```

### 3B — `plan.md` (Decisões Técnicas)

Com a `constitution.md` definida, gere o `plan.md`. Este documento traduz a `spec.md` em arquitetura — como as coisas vão ser construídas, não o quê.

**Estrutura do `plan.md`:**

```markdown
# plan.md

## Stack Técnica
Referência à constitution.md — não duplicar, apenas confirmar que está alinhado.

## Arquitetura Geral
Como o sistema está organizado em alto nível.
Para webapps: cliente/servidor/banco, fluxo de dados.
Para automações: entrada → processamento → saída, scheduling.

## Estrutura de Pastas
Liste cada pasta com uma linha explicando seu propósito.
Só crie pastas que fazem sentido para este projeto — não force estruturas que não serão usadas.

## Decisões Técnicas
Para cada decisão não óbvia, documente:
- O que foi decidido
- Por quê (qual requisito da spec.md justifica)
- Alternativa descartada e motivo

## Integrações Externas
Para cada serviço externo:
- Qual serviço e para quê
- Como será integrado (SDK, REST, webhook)
- Variáveis de ambiente necessárias

## Modelo de Dados
Entidades principais e seus campos essenciais.
Não precisa ser SQL completo — só o suficiente para a IA entender as relações.

## Variáveis de Ambiente
Lista de todas as variáveis com descrição.
Isso vira o .env.example no pacote final.
```

Apresente `constitution.md` e `plan.md` juntos ao usuário para revisão. Só avance quando ambos estiverem aprovados.

---

## FASE 4 — `tasks.md` + Estrutura de Pastas

### 4A — `tasks.md`

Com `spec.md` e `plan.md` aprovados, derive o `tasks.md`. As tarefas são extraídas diretamente das funcionalidades do MVP na `spec.md`, cruzadas com a arquitetura do `plan.md`. Não invente tarefas que não têm origem em algum desses dois documentos.

**Estrutura do `tasks.md`:**

```markdown
# tasks.md

> Derivado de: spec.md (funcionalidades MVP) + plan.md (arquitetura)
> Atualizar este arquivo ao concluir cada tarefa.

## Setup Técnico
- [ ] Inicializar projeto com comando X
- [ ] Instalar dependências (lista)
- [ ] Configurar variáveis de ambiente (.env a partir do .env.example)
- [ ] Configurar linting e tipagem

## [Nome da Feature 1 — extraído da spec]
Contexto: [1 frase do que esta feature faz, referenciando a spec]
- [ ] [Tarefa de infraestrutura/modelo de dados primeiro]
- [ ] [Tarefa de lógica/serviço]
- [ ] [Tarefa de interface/output]
- [ ] [Tarefa de validação — como confirmar que está funcionando]

## [Nome da Feature 2]
...

## Backlog
- [ ] [Features identificadas mas fora do MVP]
```

**Regras para gerar as tarefas:**

- Sempre na ordem: dados → lógica → interface → validação
- Tarefas que podem ser feitas em paralelo recebem o marcador `[P]`
- Cada tarefa deve ser atômica — uma coisa só, verificável
- A tarefa de validação de cada feature deve descrever como confirmar que está funcionando (não apenas "testar")

### 4B — Estrutura de Pastas

Gere a estrutura de pastas conforme definida no `plan.md`, com uma linha por pasta. Esta é apenas a confirmação visual — o `plan.md` já documentou o propósito de cada uma.

---

## FASE 5 — Validação Final e Entrega

Confirme que todos os artefatos estão prontos antes de encerrar:

- [ ] `spec.md` gerado, sem marcadores `[PRECISA DEFINIR]`, aprovado pelo usuário
- [ ] `constitution.md` gerado e revisado
- [ ] `plan.md` gerado e aprovado
- [ ] `tasks.md` gerado com tarefas derivadas da spec
- [ ] Estrutura de pastas definida
- [ ] Nenhuma feature de produto foi implementada — só documentação

Quando tudo estiver confirmado, entregue o **pacote de início**:

1. Todos os arquivos gerados prontos para copiar (`spec.md`, `constitution.md`, `plan.md`, `tasks.md`)
2. Estrutura de pastas para criar manualmente
3. Comando de inicialização do projeto
4. Lista de dependências para instalar
5. `.env.example` com todas as variáveis documentadas

Encerre com: *"O bootstrap está completo. Feche este chat, crie o projeto, coloque esses arquivos na raiz e comece pelo Setup Técnico do tasks.md. A partir de agora, toda conversa nova começa com: 'Leia a spec.md, a constitution.md e o tasks.md antes de qualquer coisa.'"*

---

## Padrão de prompt para features (após o bootstrap)

Oriente o usuário a seguir este padrão ao pedir cada feature nova:

```
Leia a spec.md, a constitution.md e o tasks.md.

Contexto: [o que já está funcionando]
Feature: [nome exato da feature como está no tasks.md]
Restrições: [alguma restrição específica desta tarefa]

Antes de escrever qualquer código:
1. Verifique os gates da constitution.md
2. Me explique como você vai estruturar a implementação
3. Aponte qualquer conflito com a spec.md ou com as convenções

Só escreva código depois que eu aprovar a abordagem.
```

O "explique antes de escrever" combinado com os gates é o que evita retrabalho. A IA surfaça más decisões antes de materializá-las.

---

## Referência rápida

| Fase | Entregável | Responsabilidade |
|---|---|---|
| 1 | Entendimento confirmado | Capturar intenção |
| 2 | `spec.md` | O quê e o porquê — sem tecnologia |
| 3 | `constitution.md` + `plan.md` | Regras imutáveis + decisões técnicas |
| 4 | `tasks.md` + estrutura de pastas | Roadmap derivado da spec |
| 5 | Pacote completo | Pronto para começar |

## Separação de responsabilidades dos arquivos

| Arquivo | Pergunta que responde | Muda quando? |
|---|---|---|
| `spec.md` | O que o produto faz? | Quando o produto muda |
| `constitution.md` | Quais são as regras imutáveis? | Raramente — só com decisão consciente |
| `plan.md` | Como vai ser construído? | Quando a arquitetura muda |
| `tasks.md` | O que fazer agora? | A cada feature concluída |