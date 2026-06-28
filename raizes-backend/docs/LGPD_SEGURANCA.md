# LGPD, privacidade e segurança

## Dados pessoais coletados

| Dado | Finalidade | Base legal/justificativa | Observação |
|---|---|---|---|
| Nome | Identificar o usuário no pedido | Execução do serviço | Necessário para atendimento |
| E-mail | Login e identificação | Execução do serviço | Único no sistema |
| Telefone | Contato opcional | Consentimento/legítimo interesse | Não é obrigatório |
| Consentimento de fidelidade | Controle do programa de pontos | Consentimento | Pontos só são gerados se for verdadeiro |

## Controles técnicos

- Hash de senha usando o mecanismo padrão do Django.
- Autenticação JWT para endpoints privados.
- Autorização por perfil: CLIENTE, ATENDENTE, COZINHA, GERENTE, ADMIN.
- Respostas não retornam senha ou hash.
- Logs de ações sensíveis em `LogAuditoria`.
- Pagamento é mock e não armazena dados reais de cartão.

## Retenção e minimização

O projeto mantém apenas os dados necessários para login, pedidos e fidelidade. Em uma versão produtiva, o sistema deveria incluir rotina de anonimização de usuários inativos e política de retenção para logs antigos.
