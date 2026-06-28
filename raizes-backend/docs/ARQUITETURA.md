# Arquitetura do projeto

O projeto usa uma organização em camadas simples, próxima de MVC com separação de responsabilidades:

- **API/Controllers:** `views.py`, rotas, autenticação e permissões.
- **Application:** `services.py`, orquestração dos fluxos de pedido, estoque, pagamento, fidelidade e auditoria.
- **Domain:** `models.py`, entidades, enums e relacionamentos.
- **Infrastructure:** ORM do Django, migrations, seed, integração mock de pagamento e documentação Swagger.

Essa separação evita concentrar regra de negócio diretamente nas views e deixa o fluxo principal mais fácil de testar.
