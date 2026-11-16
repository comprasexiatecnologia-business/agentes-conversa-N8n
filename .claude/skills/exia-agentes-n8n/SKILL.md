---
name: exia-agentes-n8n
description: "Metodologia Exia para criar, derivar, auditar, evoluir e testar agentes conversacionais no n8n, reutilizando bases de varejo/distribuição e serviços, prompts humanizados, extensões e skills oficiais n8n."
---

# Skill Exia — Agentes Conversacionais n8n

## Quando usar
Use para qualquer tarefa de criação, manutenção, engenharia reversa, refatoração, suporte e testes de agentes conversacionais da Exia no n8n. Esta skill não substitui as skills oficiais n8n.

## Protocolo obrigatório
1. Leia as instruções de projeto (`CLAUDE.md` ou `AGENTS.md`).
2. Verifique se as skills oficiais [n8n-io/skills](https://github.com/n8n-io/skills) estão disponíveis no ambiente. Se faltarem, instale pelo procedimento oficial e com autorização, ou reporte a pendência.
3. Determine o segmento de negócio e abra somente a referência relevante:
   - Varejo/distribuição: `bases/varejo/workflow.json` e `bases/varejo/prompt.md`.
   - Serviços: `bases/servicos/workflow.json` e `bases/servicos/prompt.md`.
   - Híbrido: crie uma especificação de combinação; não misture automaticamente políticas dos clientes.
4. Documente as partes reutilizáveis, módulos específicos, riscos e faltas de integração.
5. Siga BSPA, conforme `standards/metodologia-bspa.md`, com code review pré e pós-implementação.
6. Faça cópia versionada da base e personalize dados, identidade, prompts e integrações do novo cliente.
7. Incorpore recursos extras por módulos separados (MCP/CRM/ERP/agenda/envio-imagens), preservando comportamento correto já existente.
8. Faça testes locais antes de consultar/atualizar o n8n remoto; use `standards/testes.md`.
9. Respeite `standards/economia-tokens.md`: não recarregar workflow integral em loop nem despejar dados completos no contexto.
10. Para escrita remota: confirmar workflow autorizado e inativo, backup e versão atual, validar, salvar apenas após autorização, conferir persistência e nunca enviar mensagens reais em homologação.

## Especializações de prompt
**Distribuição e varejo:** conversa objetiva, produtos, categorias, preços configurados, condições comerciais, pedidos e logística.
**Serviços:** escuta ativa, qualificação, empatia contextual, objeções e agendamento quando houver disponibilidade confirmada.
O comportamento humanizado é compartilhado, mas nem toda regra do prompt é universal. Evite repetir perguntas já respondidas, inventar informações ou alegar falsamente ser humano quando questionado.

## Módulo de envio de imagens de horários
Referência em serviços: roteamento para imagens de aulas (Coletivas e Sobral Box). Generalize somente quando requisitado: identificação de unidade, mapa de mídias do cliente, URL confiável, envio por API com sucesso confirmado, bloqueio de duplicatas e fallback sem inventar resultado.

## Segurança de arquivos de referência
As cópias disponibilizadas em `bases/` devem estar saneadas; credenciais reais ficam nos vaults/credenciais do n8n. Nunca usar uma cópia GitHub como prova de que conexão ou workflow está funcionando na instância atual.

## Encerramento da tarefa
Relate arquivos criados, diffs relevantes, testes feitos, resultados comprovados, riscos pendentes e passo seguinte, separando simulações de testes de integração reais.
