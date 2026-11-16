# Segurança Exia — agentes n8n

- GitHub é repositório de referências e código, não repositório de segredos.
- Não usar IDs de credenciais exportados como credenciais confiáveis do cliente novo.
- Nunca executar envios externos reais, ativar workflows, criar contratos ou alterar produção sem autorização explícita.
- Validar assinatura/origem do webhook por dado independente. Nunca comparar um campo consigo mesmo como se fosse autenticação.
- Distinguir mensagem de bot e intervenção humana de acordo com contrato da API de WhatsApp.
- Proteger dados por cliente/lead; não ligar modelos a ferramentas MCP amplas sem isolamento.
- Implementar deduplicação, idempotência e controle de concorrência atômico.
- Preservar pausa humana persistente e retomada humana explícita.
- Sanitizar exports para GitHub: remover credenciais, tokens, parâmetros secretos e links autenticados.
- Homologação exige testes de execução; validação de schema é insuficiente.
- Não alegar ser uma pessoa real quando questionado; humanização é tom, não dissimulação.
