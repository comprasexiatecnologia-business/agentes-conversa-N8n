# Matriz de regressão — agentes conversacionais no n8n

- Conversas: saudação, pedidos diretos, mensagens curtas, mudança de assunto, múltiplas mensagens consecutivas e memória sem repetição.
- Mídias: áudio, imagem recebida, documento, falha de transcrição e mídia indisponível.
- Varejo: catálogo, condições de pagamento, pedido, entrega e produto inexistente sem alucinar informações.
- Serviços: escuta, qualificação, objeções, disponibilidade de agenda e confirmação real de horário.
- Serviços com imagem: enviar a imagem correta dos horários somente quando solicitada; não duplicar; fallback se URL falhar.
- Operador humano: intervenção, pausa, renovação, controle manual e retomada explícita.
- Webhook: payload válido, inválido, evento duplicado, `fromMe`, `wasSentByApi` e concorrência.
- Integrações: 401/403, erro, timeout, paginação incompleta, resposta `isError`, status desconhecido e indisponibilidade.
- Saída: respeito a expediente, idempotência, canal e bloqueio de mensagens reais em homologação.
- Diferenciar resultado de mock, validação de schema, execução remota e homologação com APIs reais.
