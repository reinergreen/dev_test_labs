# Contratos principais da API

## /auth - Login

Finalidade: autenticar usuário e retornar token JWT.

Método/Rota: `POST /api/auth/login/`

Auth/Permissão: público

Request:

```json
{
  "email": "cliente@exemplo.com",
  "password": "Cliente@123"
}
```

Response 200:

```json
{
  "refresh": "jwt-refresh",
  "access": "jwt-access",
  "tokenType": "Bearer",
  "expiresIn": 3600,
  "user": {
    "id": 1,
    "nome": "Maria Cliente",
    "email": "cliente@exemplo.com",
    "perfil": "CLIENTE"
  }
}
```

## /pedidos - Criar pedido

Finalidade: criar pedido multicanal validando cardápio e estoque.

Método/Rota: `POST /api/pedidos/`

Auth/Permissão: JWT, perfil CLIENTE.

Request:

```json
{
  "unidadeId": 1,
  "canalPedido": "TOTEM",
  "itens": [
    { "produtoId": 1, "quantidade": 2 }
  ],
  "formaPagamento": "MOCK"
}
```

Response 201:

```json
{
  "id": 1,
  "clienteId": 5,
  "unidadeId": 1,
  "canalPedido": "TOTEM",
  "status": "AGUARDANDO_PAGAMENTO",
  "total": "37.80",
  "itens": [
    {
      "produtoId": 1,
      "produtoNome": "Cuscuz Nordestino",
      "quantidade": 2,
      "precoUnitario": "18.90"
    }
  ]
}
```

Erros esperados: 401, 404, 409, 422.

## /pagamentos/mock - Pagamento simulado

Finalidade: simular retorno de gateway de pagamento.

Método/Rota: `POST /api/pagamentos/mock/`

Auth/Permissão: JWT.

Request aprovado:

```json
{
  "pedidoId": 1,
  "formaPagamento": "MOCK",
  "forcarStatus": "APROVADO"
}
```

Request recusado:

```json
{
  "pedidoId": 1,
  "formaPagamento": "MOCK",
  "forcarStatus": "RECUSADO"
}
```

Response 201:

```json
{
  "id": 1,
  "pedidoId": 1,
  "forma": "MOCK",
  "status": "APROVADO",
  "transacaoId": "uuid",
  "payloadRetorno": {
    "gateway": "mock-raizes",
    "mensagem": "Pagamento aprovado no ambiente simulado.",
    "valor": "37.80"
  }
}
```

## /pedidos/{id}/status - Atualizar status

Finalidade: permitir que cozinha/gerência atualize o andamento do pedido.

Método/Rota: `PATCH /api/pedidos/{id}/status/`

Auth/Permissão: JWT, perfis COZINHA, GERENTE ou ADMIN.

Request:

```json
{
  "status": "EM_PREPARO"
}
```

Response 200: retorna o pedido atualizado.

Erros esperados: 401, 403, 404, 409, 422.
