# Diagrama de Contexto (C4 Nível 1)

```mermaid
C4Context
    title Contexto - Marketplace B2B de Sobras Industriais

    Person(comprador, "Empresa Compradora", "Consulta anúncios, envia propostas e paga")
    Person(vendedor, "Empresa Vendedora", "Cadastra sobras, publica anúncios e responde propostas")

    System(marketplace, "Marketplace", "Gerencia anúncios, propostas e negociações")
    System_Ext(escrow, "Gateway de Escrow", "Retém os fundos em custódia")

    Rel(vendedor, marketplace, "Publica anúncio e aceita ou recusa proposta")
    Rel(comprador, marketplace, "Envia proposta")
    Rel(marketplace, vendedor, "Notifica nova proposta")
    Rel(marketplace, escrow, "Abre transação")
    Rel(comprador, escrow, "Deposita fundos")
    Rel(escrow, marketplace, "Confirma ou falha o pagamento")

    UpdateLayoutConfig($c4ShapeInRow="2", $c4BoundaryInRow="1")
```