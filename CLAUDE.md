# Exia | Constituição operacional de agentes conversacionais no n8n

**Escopo exclusivo:** agentes de atendimento, pré-venda, vendas, qualificação, agendamento e suporte conversacional **implementados no n8n**, principalmente por WhatsApp. Não use este repositório como boilerplate genérico de software.

## Antes de qualquer projeto
1. Ler este arquivo e `standards/metodologia-bspa.md`, `standards/seguranca.md` e `standards/economia-tokens.md`.
2. Invocar a skill privada **exia-agentes-n8n** disponível neste projeto.
3. Conferir a disponibilidade das [skills oficiais n8n](https://github.com/n8n-io/skills). Usar as relevantes. Se não instaladas, orientar ou realizar instalação somente quando permitida; nunca fingir que estão instaladas.
4. Conferir conexão MCP do n8n, apenas se a tarefa exigir acesso remoto. Não confundir configuração com autenticação.
5. Identificar segmento: **varejo/distribuição** ou **serviços**. Ler as referências correspondentes de `bases/`. Nunca trocar modelos por artefatos de outros chats.
6. Abrir briefing BSPA e levantar lacunas antes de implementar. Selecionar a base por segmento e criar derivado, sem editar os arquivos originais.

## Regras de arquitetura
- Core reutilizável: webhook, normalização de evento, identificação de contato, deduplicação, tratamento multimodal, memória/buffer, agente, roteamento, proteção de atendimento humano, saída e observabilidade.
- A funcionalidade comprovada deve ser preservada; **bugs e vulnerabilidades não**. Corrigir mediante auditoria e regressão.
- Novas integrações (MCP, CRM, ERP, agenda, mídias, pagamentos, subagentes) são extensões modulares, não justificativa para reescrever a base.
- Prompts separados por segmento, com humanização, contexto e variáveis específicas do cliente; nunca copiar regras comerciais, nomes, contatos ou conhecimento de um cliente para outro.
- A base de serviços demonstra envio de imagens de horários das aulas, reutilizável como extensão **opcional e sob demanda**.
- Credenciais, IDs, webhooks, domínios, APIs e URLs de mídia são próprios de cada cliente. Nunca comitar segredos.
- Os originais fornecidos são **referências candidatas**, não bases homologadas em produção. Não afirmar que passaram testes sem evidências.

## Segurança e execução
- Por padrão: apenas leitura, análise e simulações locais. Não alterar produção, ativar/publish workflows, disparar WhatsApp real ou mudar credenciais sem autorização.
- Validar contratos reais de API e MCP antes de usar; rejeitar comportamentos inseguros de fallback.
- Segurança do workflow precisa existir em nodes determinísticos; não confiar exclusivamente no prompt.
- Qualquer atualização remota requer confirmação de versão/estado, backup, diff e verificação pós-gravação.

## Eficiência
- Snapshot uma vez por versão; patches/diffs; testes locais antes dos remotos.
- Não despejar JSONs, logs ou históricos no contexto. Guardar arquivos locais e mostrar resumos.
- Skills específicas sob demanda e MCP apenas quando necessário.
- Manter checkpoint de decisões, alterações, pendências, testes e próxima etapa para retomar sem refazer trabalho.
- Economia nunca dispensa autenticação, isolamento, idempotência, concorrência, pausa humana ou testes essenciais.

## Entregáveis
Briefing; spec; plano; relatório de auditoria; derivação versionada; diffs; testes e evidências; documentação de credenciais pendentes; rollback.
\n## Aplicação no Claude Code\nExecute no diretório raiz deste repositório, verifique a skill `.claude/skills/exia-agentes-n8n/SKILL.md` e mantenha o plugin oficial `n8n-skills@n8n-io` ativo quando necessário.\n