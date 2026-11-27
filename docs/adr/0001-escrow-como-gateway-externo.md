# ADR 0001 — Uso de Gateway de Escrow externo

**Status:** Aceito
**Data:** 2026-11-27
**Responsável:** Luiz Angelo

## Contexto
O Marketplace precisa garantir que o pagamento só seja liberado quando
a negociação for cumprida. Processar dinheiro está fora do escopo do
sistema (Sprint 2), assim como logística e nota fiscal.

## Decisão
Delegar a custódia dos fundos a um Gateway de Escrow externo, integrado
por API REST (criação da transação) e webhooks (confirmação ou falha).

## Alternativas consideradas
1. Implementar o escrow dentro do Marketplace: descartada, pois exigiria
   processamento financeiro e traria risco regulatório.
2. Pagamento direto entre as empresas: descartada, pois não oferece
   garantia a nenhuma das partes.

## Consequências
(+) Segurança financeira para comprador e vendedor.
(+) Menor risco regulatório e escopo do projeto preservado.
(+) Marketplace desacoplado do meio de pagamento (boleto, PIX, TED).
(−) Dependência de um terceiro (disponibilidade e custo).
(−) Exige `idempotencyKey` na criação da transação.
(−) Exige validação da assinatura (`hashAssinatura`) do webhook.
(−) Exige tratar o fluxo de falha (`EXPIRADO`/`RECUSADO` → proposta `CANCELADA`).