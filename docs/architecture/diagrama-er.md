# Diagrama Entidade-Relacionamento

Modelo de dados do Marketplace B2B de Sobras Industriais, com empresas, lotes de resíduo, propostas, contrapropostas e transações.

````mermaid
erDiagram
    EMPRESA ||--o{ LOTE_RESIDUO : publica
    CATEGORIA ||--o{ LOTE_RESIDUO : classifica
    LOTE_RESIDUO ||--o{ PROPOSTA : recebe
    EMPRESA ||--o{ PROPOSTA : envia
    PROPOSTA ||--o{ CONTRAPROPOSTA : recebe
    PROPOSTA ||--o| TRANSACAO : gera
    EMPRESA ||--o{ TRANSACAO : participa

    EMPRESA {
        int id PK
        string nome
        string cnpj UK
        string endereco
        string perfil "COMPRADORA, VENDEDORA ou AMBAS"
    }

    CATEGORIA {
        int id PK
        string nome
        string descricao
    }

    LOTE_RESIDUO {
        int id PK
        int vendedor_id FK
        int categoria_id FK
        string titulo
        string descricao
        string tipo
        decimal quantidade
        string unidade
        decimal preco_minimo
        string status
    }

    PROPOSTA {
        int id PK
        int lote_id FK
        int comprador_id FK
        decimal quantidade
        decimal valor_ofertado
        date prazo_validade
        string status
    }

    CONTRAPROPOSTA {
        int id PK
        int proposta_id FK
        decimal valor_contraproposto
        string status
        datetime criada_em
    }

    TRANSACAO {
        int id PK
        int proposta_id FK
        int comprador_id FK
        int vendedor_id FK
        decimal valor
        string escrow_id
        string status
        datetime confirmada_em
    }
````