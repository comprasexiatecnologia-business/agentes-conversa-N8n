# Módulo opcional — envio de imagens no WhatsApp

A referência de serviços possui nodes para enviar imagens com horários de aulas (Coletivas e Sobral Box).

**Contrato proposto:** entrada `{chatId, unidade, intencao, mediaId}`; escolha de mídia aprovada do cliente; verificação de URL; bloqueio por operador humano; deduplicação; envio UAZAPI; sucesso por retorno real; log sem segredos.

Nunca utilizar URLs, tokens, nomes de unidades ou imagens de outro cliente sem reconfiguração. O módulo somente será implementado e homologado conforme a necessidade do projeto.
