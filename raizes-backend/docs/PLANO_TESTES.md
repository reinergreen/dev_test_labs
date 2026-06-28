# Plano de testes da API

| ID | Cenário | Endpoint | Pré-condição | Entrada | Esperado | Evidência na coleção |
|---|---|---|---|---|---|---|
| T01 | Login válido | POST /api/auth/login/ | Seed aplicado | email/senha válidos | 200 + access token | Auth/Login cliente |
| T02 | Login inválido | POST /api/auth/login/ | Seed aplicado | senha errada | 401 + erro padrão | Auth/Login inválido |
| T03 | Listar cardápio | GET /api/cardapio/?unidade_id=1 | Token válido | query unidade | 200 + itens | Cardápio/Listar por unidade |
| T04 | Criar pedido válido | POST /api/pedidos/ | Cliente logado e estoque | canalPedido + itens | 201 + status AGUARDANDO_PAGAMENTO | Pedidos/Criar pedido válido |
| T05 | Criar pedido sem token | POST /api/pedidos/ | Sem autenticação | body válido | 401 + erro padrão | Erros/Criar pedido sem token |
| T06 | Canal inválido | POST /api/pedidos/ | Cliente logado | canalPedido inválido | 422/400 + erro padrão | Erros/Canal inválido |
| T07 | Produto inexistente | POST /api/pedidos/ | Cliente logado | produtoId 9999 | 404 + erro padrão | Erros/Produto inexistente |
| T08 | Estoque insuficiente | POST /api/pedidos/ | Cliente logado | quantidade muito alta | 409 + ESTOQUE_INSUFICIENTE | Erros/Estoque insuficiente |
| T09 | Pagamento aprovado | POST /api/pagamentos/mock/ | Pedido criado | forcarStatus APROVADO | 201 + pagamento aprovado | Pagamentos/Mock aprovado |
| T10 | Pagamento recusado | POST /api/pagamentos/mock/ | Pedido criado | forcarStatus RECUSADO | 201 + status recusado | Pagamentos/Mock recusado |
| T11 | Atualizar status sem permissão | PATCH /api/pedidos/{id}/status/ | Cliente logado | status EM_PREPARO | 403 + erro padrão | Erros/Cliente atualiza status |
| T12 | Listar auditoria | GET /api/auditoria/logs/ | Gerente logado | sem body | 200 + logs | Auditoria/Listar logs |
