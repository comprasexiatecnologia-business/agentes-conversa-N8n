# Exia Tecnologia — Framework de Agentes Conversacionais n8n

> **Repositório privado da Exia** dedicado exclusivamente a criar, adaptar, revisar e manter agentes conversacionais de WhatsApp no **n8n**. Ferramentas de desenvolvimento: **Claude Code** e **OpenAI Codex**.

Este README é o guia de instalação **do zero, em ordem de execução**, no Mac. Inclui a conexão do repositório, as instruções internas da Exia, o **plugin de skills oficiais do n8n**, o MCP da instância e um teste seguro de leitura.

**Documentação de processos:** [POP 005 — Framework de Agentes Conversacionais](https://docs.google.com/document/d/1it3FQwCw9aZP7e32jzaxiRgjyP8xvo-BIYo7tE-VT40/edit).

---

## 1. O que você está instalando?

| Camada | Função | Onde fica |
|---|---|---|
| Repositório privado da Exia | Bases n8n por segmento, prompts humanizados e padrões | GitHub + cópia local |
| `CLAUDE.md` | Regras operacionais do Claude Code neste projeto | Raiz do repositório |
| `AGENTS.md` | Regras operacionais do Codex neste projeto | Raiz do repositório |
| Skill privada `exia-agentes-n8n` | Metodologia Exia de reuso, extensões e BSPA | `.claude/skills/` e `.agents/skills/` |
| Plugin oficial `n8n-skills` | Boas práticas, expressões, arquitetura, testes e MCP n8n | Instalado no agente |
| MCP `n8n-mcp` | Acesso autorizado à instância n8n | Configurado por agente |

**Importante:** o repositório **não instala automaticamente** plugins, skills oficiais ou MCP na máquina. Cada agente precisa ser configurado uma vez por ambiente. Os arquivos `CLAUDE.md`, `AGENTS.md` e a skill privada só funcionarão após estarem presentes na cópia local.

**Instância de referência da Exia:** `https://workflow.exiadigital.shop`. Em outra instalação, substitua pela URL-base autorizada.

---

## 2. Pré-requisitos (faça uma vez)

- Mac com Terminal e acesso à internet.
- Git instalado e acesso autorizado ao repositório privado.
- Claude Code e/ou Codex CLI instalados, com login realizado.
- Instância n8n **2.2.0 ou superior**, com **Settings → Instance-level MCP** habilitado.
- Para o plugin oficial no Codex, versão **0.142.0 ou superior**.

Abra o Terminal e confira:

```bash
git --version
claude --version
codex --version
```

Se um comando não existir, instale o aplicativo correspondente a partir da [documentação oficial do Claude Code](https://code.claude.com/docs/en/overview) ou do [Codex](https://developers.openai.com/codex/). **Não execute comandos do Claude dentro do Codex, nem vice-versa.**

### 2.1 Autenticar GitHub no Mac

Recomendação: instalar o [GitHub CLI](https://cli.github.com/) e autenticar por navegador:

```bash
# Se o Homebrew estiver disponível:
brew install gh

gh auth login
gh auth status
```

No assistente `gh auth login`, selecione GitHub.com, HTTPS e autenticação via navegador. Não cole seu token em chats, prompts ou arquivos do repositório.

### 2.2 Clonar o repositório da Exia

```bash
mkdir -p ~/Exia
cd ~/Exia
git clone https://github.com/comprasexiatecnologia-business/agentes-conversa-N8n.git
cd agentes-conversa-N8n
git status
```

Se a pasta já existir, **não clone por cima**. Em vez disso:

```bash
cd ~/Exia/agentes-conversa-N8n
git pull --ff-only
```

Se aparecer `Repository not found`, confira `gh auth status` e confirme que sua conta possui acesso ao repositório privado.

---

## 3. Instalar e configurar no Claude Code (passo a passo)

**Objetivo:** carregar as regras da Exia ao trabalhar nesta pasta e ativar o plugin oficial de skills do n8n, com autenticação MCP.

### Etapa 3.1 — Entrar no projeto e abrir o Claude

No **Terminal do Mac**:

```bash
cd ~/Exia/agentes-conversa-N8n
claude
```

O Claude Code deve ser aberto **dentro dessa pasta**; assim poderá encontrar `CLAUDE.md` e `.claude/skills/exia-agentes-n8n/SKILL.md` quando esses arquivos já estiverem versionados no repositório.

### Etapa 3.2 — Instalar o marketplace oficial n8n

Os próximos comandos são digitados **dentro da sessão do Claude Code**, um por vez — **não são comandos do shell**:

```text
/plugin marketplace add n8n-io/skills
```

Depois:

```text
/plugin install n8n-skills@n8n-io
```

Quando solicitar a URL da instância n8n, informe **somente a URL-base**:

```text
https://workflow.exiadigital.shop
```

**Não adicione** `/mcp-server/http`: o plugin oficial já acrescenta esse caminho no Claude Code.

### Etapa 3.3 — Recarregar o plugin

Ainda no Claude Code:

```text
/reload-plugins
```

Se o plugin solicitar autorização de execução de hooks, leia a solicitação e autorize apenas se corresponder ao plugin oficial `n8n-io/skills`.

### Etapa 3.4 — Conectar o MCP

Ainda no Claude Code:

```text
/mcp
```

Selecione **n8n-mcp → Authenticate** e conclua o OAuth no navegador. Confira se o MCP está conectado. Se já existir outra conexão do mesmo servidor, mantenha **somente uma ativa** para evitar duplicar ferramentas e consumir contexto desnecessário.

Se a URL não tiver sido solicitada durante a instalação, o projeto oficial orienta configurar com:

```text
/plugin configure n8n-skills@n8n-io
```

Depois recarregue novamente.

### Etapa 3.5 — Validar sem modificar o n8n

Peça ao Claude:

> Leia o CLAUDE.md e a skill exia-agentes-n8n deste repositório. Confirme que as skills oficiais n8n-io/skills estão instaladas, que o MCP n8n-mcp está autenticado e que você consegue listar ferramentas disponíveis. Faça **somente consultas**, sem alterar, ativar, publicar ou testar envios reais. Diga quais verificações foram confirmadas e quais ficaram pendentes.

Só considere a instalação validada quando o Claude mostrar evidência de acesso às instruções e ao MCP.

---

## 4. Instalar e configurar no Codex (passo a passo)

**Objetivo:** usar as mesmas bases e regras da Exia, com o plugin oficial do n8n e conexão MCP própria do Codex.

### Etapa 4.1 — Conferir versão

No **Terminal do Mac**, fora de qualquer sessão do Codex:

```bash
codex --version
```

O plugin oficial exige **Codex >= 0.142.0**. Se a versão for anterior, atualize o Codex por seu método oficial de instalação antes de prosseguir.

### Etapa 4.2 — Registrar e instalar o plugin oficial

Execute no **Terminal do Mac**, um comando por vez:

```bash
codex plugin marketplace add n8n-io/skills
codex plugin add n8n-skills@n8n-io
```

Reinicie o Codex depois da instalação. Se surgir a confirmação de confiança dos hooks (`SessionStart`, `PreToolUse`, `PostToolUse`), confira a origem e aprove o plugin oficial.

### Etapa 4.3 — Configurar o MCP no Codex

Ao contrário do Claude, o plugin oficial **não configura automaticamente o MCP no Codex**. No Terminal:

```bash
codex mcp add n8n-mcp --url https://workflow.exiadigital.shop/mcp-server/http
```

Se o servidor `n8n-mcp` já estiver configurado, **não o duplique**. Antes, consulte:

```bash
codex mcp list
```

### Etapa 4.4 — Autenticar o MCP

No Terminal, se ainda não estiver autenticado:

```bash
codex mcp login n8n-mcp
```

Conclua a autenticação OAuth no navegador e confirme o acesso.

### Etapa 4.5 — Iniciar o Codex no repositório

```bash
cd ~/Exia/agentes-conversa-N8n
codex
```

O Codex deverá carregar `AGENTS.md` e localizar `.agents/skills/exia-agentes-n8n/SKILL.md` quando a skill estiver presente no projeto.

Peça:

> Leia AGENTS.md e use a skill privada exia-agentes-n8n. Verifique as skills oficiais do n8n e a conexão n8n-mcp. Identifique as duas bases por segmento disponíveis neste repositório. Apenas leitura; não modifique workflows nem realize envios reais. Entregue um checklist curto com evidências.

---

## 5. Como iniciar um novo projeto de agente

1. **Briefing:** identifique o segmento do cliente e os objetivos do agente WhatsApp.
2. **Escolha da base:** para varejo/distribuição, use `bases/varejo/`; para serviços, use `bases/servicos/`. Não misture regras de empresas distintas sem documentação.
3. **Preserve o original:** crie uma versão derivada do workflow e prompt; nunca sobrescreva o material-base.
4. **Configuração própria:** substitua credenciais, IDs, URLs, nomes, horários e regras de cada cliente. Nunca copie segredos.
5. **Extensão:** adicione CRM, ERP, API, MCP, agendamento, envio de imagens ou subagentes apenas quando forem necessários.
6. **BSPA:** Brainstorm → Spec → Plano → Auditoria, incluindo revisão de requisitos e code review.
7. **Testes:** execute regressão local, teste os casos de erro e valide a integração em ambiente controlado.
8. **Publicação:** só depois de autorização explícita, com backup e rollback documentados.

### Exemplo: envio de imagens de horários

O segundo workflow fornecido tem rotas para enviar imagens de horários de aulas. No novo cliente, esse mecanismo deve virar um **módulo opcional**, não uma regra de todos os projetos. Configure a unidade e a imagem corretas, envie **somente quando solicitado**, valide o retorno da API e impeça duplicações.

**Os dois workflows e os dois prompts recebidos são referências candidatas, não homologações técnicas concluídas.**

---

## 6. Economia de tokens — regra obrigatória

**Claude Code e Codex devem cumprir esta política em qualquer tarefa n8n:**

| Faça | Evite |
|---|---|
| Salve um snapshot local por versão | Reler o workflow inteiro a cada mudança |
| Edite nodes/conexões por patches | Reenviar JSON completo para alterações pequenas |
| Execute testes locais primeiro | Rodar dezenas de chamadas MCP redundantes |
| Peça só dados necessários | Listar todas as execuções e logs completos |
| Mostre diffs e erros resumidos | Colar centenas de linhas no chat |
| Carregue skills específicas sob demanda | Recarregar todas as referências técnicas |
| Registre checkpoints de sessão | Refazer diagnóstico já concluído |
| Verifique concorrência antes de persistir | Atualizar um workflow remoto com base antiga |

O objetivo é reduzir consumo de contexto, **não enfraquecer validações**. Autenticação, bloqueio humano, deduplicação, segurança, testes e comparação de versão continuam obrigatórios.

---

## 7. Solução de problemas

### `claude: command not found` ou `codex: command not found`
O aplicativo correspondente não está instalado ou não está no PATH. Consulte o site oficial e reinicie o Terminal após instalar.

### `git clone` diz `Repository not found`
Confirme se o usuário autenticado tem acesso ao repositório privado; revise `gh auth status`.

### O Claude não encontra as instruções Exia
Confira se abriu o Claude na **raiz do repositório** e se `CLAUDE.md` e `.claude/skills/exia-agentes-n8n/SKILL.md` existem. Faça `git pull --ff-only` e reinicie a sessão.

### O Codex não encontra a skill Exia
Confira se `AGENTS.md` e `.agents/skills/exia-agentes-n8n/SKILL.md` existem na cópia local. Reinicie o Codex na raiz da pasta.

### MCP não conecta / erro 401 ou 403
Verifique Instance-level MCP no n8n, URL-base/caminho corretos, permissão do usuário e autenticação OAuth. Não presuma que um MCP configurado está autenticado.

### Ferramentas do n8n aparecem duas vezes
Verifique se existem duas conexões para o mesmo MCP. Desative a duplicata, evitando uso desnecessário de contexto.

### Plugin oficial não instala no Codex
Verifique `codex --version` (>= 0.142.0), conectividade com GitHub e comandos da versão atual em [n8n-io/skills](https://github.com/n8n-io/skills).

### Antes de usar em produção
Não publique workflows, não faça envios de WhatsApp e não modifique credenciais reais sem autorização. Instalar a skill ou validar o JSON **não significa que o fluxo foi homologado**.

---

## 8. Referências oficiais

- [n8n — Skills oficiais, instalação para Claude Code e Codex](https://github.com/n8n-io/skills)
- [n8n — Documentação](https://docs.n8n.io/)
- [Claude Code — Documentação](https://code.claude.com/docs/en/overview)
- [Codex — Documentação](https://developers.openai.com/codex/)
- [GitHub CLI](https://cli.github.com/)
- [POP 005 — Exia (Google Docs)](https://docs.google.com/document/d/1it3FQwCw9aZP7e32jzaxiRgjyP8xvo-BIYo7tE-VT40/edit)

**Estado:** este README documenta instalação e uso. A presença real dos arquivos de bases e skills privadas deve ser conferida no repositório; não se deve declarar instalação ou homologação concluída antes das verificações.
