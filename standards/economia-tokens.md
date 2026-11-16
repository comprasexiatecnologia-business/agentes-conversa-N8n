# Exia — política obrigatória de economia de tokens

1. Primeiro snapshot do workflow por versão (JSON e hash SHA-256), nunca recarregue o mesmo conteúdo completo sem motivo.
2. Trabalhe nos arquivos locais: diff, patch, lint, testes unitários e de regressão.
3. Use MCP somente quando a atividade depender de dados atuais ou operações remotas.
4. Solicite a menor resposta de ferramenta viável; resuma erros por node, sem imprimir todos os logs.
5. Skills oficiais n8n sob demanda: descubra e carregue somente referências úteis à tarefa.
6. Mantenha `STATUS.md`: estado, próximo passo, versão, arquivos, bloqueios e evidências.
7. Não faça leitura integral das duas bases se o projeto usa apenas um segmento.
8. Separe diagnóstico, implementação e homologação, evitando repetir raciocínio e consultas já registrados.
9. Antes de update remoto, verifique se a versão mudou; se mudou, compare diferenças concorrentes.
10. Teste localmente primeiro. Pin data, mocks e schema não equivalem a homologação de integração.
11. Nunca economize tokens removendo autenticação, verificação do operador humano, travas Redis atômicas, idempotência, validação de saída ou auditoria de credenciais.
12. Registre métricas reais quando disponíveis, sem prometer porcentagem de economia.

**Fluxo preferencial:** descobrir → snapshot → especificar → patches locais → testes locais → validação remota pontual → atualização autorizada → conferir persistência → documentar.
