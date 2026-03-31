# Skills

Repositório central de skills para uso com Claude Code, Antigravity e Cursor.

---

## Estrutura

```
skills/
├── anthropics/          # Skills oficiais da Anthropic
├── antigravity-kit/     # Skills do Antigravity Kit
├── n8n/                 # Skills de automação com N8N
├── stitch/              # Skills do Google Stitch
├── supabase/            # Skills do Supabase
├── superpowers/         # Skills do repositório Superpowers
├── vercel/              # Skills do Vercel
├── master-skill.md      # Arquivo de referência da Master Skill
├── README.md            # Este arquivo
└── z-novas-skills/      # Zona de entrada para skills novas (processada pelo classificar novas)
```

---

## O que é a Master Skill

A **Master Skill** é um orquestrador global. Em vez de copiar skills manualmente para cada projeto, você usa um único comando e ela faz isso por você — puxando apenas o que é relevante para o contexto de trabalho atual.

Ela é ativada exclusivamente pelo comando `/master-skill`.

---

## Instalação

### 1. Clone o repositório

```bash
git clone https://github.com/kevindbotelho/skills
```

### 2. Instale a Master Skill globalmente

Copie o arquivo `master-skill.md` para a pasta de workflows globais do seu agente. O caminho varia conforme a ferramenta — no Antigravity, por exemplo, fica em:

```
C:\Users\<seu-usuario>\.gemini\antigravity\global_workflows\master-skill.md
```

No Claude Code e no Cursor, o caminho é diferente — consulte a documentação de cada ferramenta para localizar a pasta de comandos globais.

No **Cursor**, tem um detalhe importante: para aparecer no `/`, organize assim:

```txt
C:\Users\<seu-usuario>\.cursor\skills\master-skill\SKILL.md
```

Ou seja, o `master-skill.md` vira uma pasta `master-skill` com o arquivo `SKILL.md` dentro.

> O arquivo `master-skill.md` na raiz deste repo é o backup/referência. O que funciona de verdade é a cópia na pasta correta do agente.

### 3. Configure o cofre na primeira execução

Abra qualquer projeto no seu agente e rode:

```
/master-skill
```

Ele vai perguntar o caminho absoluto da pasta onde está este repositório. Informe o caminho completo, por exemplo:

```
C:\Users\kevin\Downloads\skills
```

A configuração é salva em `.masterskill.json` na raiz do projeto. Nas próximas execuções, é lida automaticamente.

---

## Comandos disponíveis

### Carregar um grupo de skills

```
/master-skill frontend
/master-skill backend
/master-skill banco-de-dados
/master-skill arquitetura
/master-skill qualidade
/master-skill ia
/master-skill dados
/master-skill deploy
/master-skill geral
```

Copia todas as skills do grupo para a pasta `skills/` do projeto ativo.

### Carregar uma skill individual

```
/master-skill quero a skill de brainstorming
/master-skill quero a skill de supabase
```

Busca a skill pelo nome em todos os grupos e copia para `skills/`.

### Listar grupos disponíveis

```
/master-skill liste as skills
```

Exibe todos os grupos e o número de skills em cada um.

### Classificar skills novas

```
/master-skill classificar novas
```

Lê cada pasta dentro de `z-novas-skills/`, entende o que cada skill faz, compara com as skills já existentes no grupo candidato e decide:
- **Cobertura nova** → adiciona ao cofre e atualiza a Master Skill automaticamente
- **Duplicata** → pede confirmação antes de adicionar
- **Ambíguo** → apresenta o raciocínio e pede sua decisão

Ao final, `z-novas-skills/` fica vazia.

### Reset

```
/master-skill reset
```

Apaga o `.masterskill.json` e permite redefinir o caminho do cofre.

---

## Como adicionar skills novas

1. Baixe a skill nova (pasta com `SKILL.md` dentro)
2. Jogue a pasta dentro de `z-novas-skills/`
3. No seu agente, rode `/master-skill classificar novas`
4. Ele lê, avalia e incorpora automaticamente

---

## Grupos e suas skills

| Grupo | Conteúdo |
|---|---|
| `frontend` | Stitch, React, Next.js, Tailwind, Shadcn, design de UI |
| `backend` | Python, APIs, Node.js, N8N, arquitetura de servidor |
| `banco-de-dados` | Supabase, modelagem, queries |
| `arquitetura` | Planejamento de sistema, PRD, orquestração de agentes |
| `qualidade` | Code review, debugging, testes, TDD |
| `ia` | API do Claude, MCP, roteamento inteligente |
| `dados` | Excel, PowerPoint, Word, PDF |
| `deploy` | Vercel, CI/CD, infraestrutura |
| `geral` | Git, bash, documentação, escrita |

---

## Fontes

- [anthropics/skills](https://github.com/anthropics/skills)
- [obra/superpowers](https://github.com/obra/superpowers)
- [msitarzewski/agency-agents](https://github.com/msitarzewski/agency-agents)
- [vudovn/antigravity-kit](https://github.com/vudovn/antigravity-kit)
- [supabase/agent-skills](https://github.com/supabase/agent-skills)
- [vercel-labs/agent-skills](https://github.com/vercel-labs/agent-skills)
- [google-labs-code/stitch-skills](https://github.com/google-labs-code/stitch-skills)
- [render-oss/skills](https://github.com/render-oss/skills)
