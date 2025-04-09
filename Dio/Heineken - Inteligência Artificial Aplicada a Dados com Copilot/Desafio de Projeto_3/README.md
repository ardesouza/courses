# Descrição do Projeto Lógico - E-commerce

## 📌 Visão Geral
O esquema lógico implementa um banco de dados relacional para um sistema de e-commerce com as seguintes características principais:

## 📦 Módulos Principais
| Módulo       | Funcionalidades                              |
|--------------|---------------------------------------------|
| **Cadastros** | Clientes (PF/PJ), fornecedores, produtos    |
| **Vendas**    | Ciclo completo (pedido → pagamento → entrega) |
| **Estoque**   | Gestão multi-depósito com quantidades       |
| **Marketplace**| Integração com vendedores terceirizados     |

### 🏗️ Estrutura Central
- Baseado em 10 tabelas principais (`Cliente`, `Produto`, `Pedido`, etc.)
- 5 tabelas de relacionamento
- Modelo normalizado até **3FN** (Terceira Forma Normal)

## Componentes Essenciais
- **Cadastro completo** de clientes (PF/PJ) e fornecedores
- **Gestão de produtos** com categorias e múltiplos estoques
- **Processo completo de vendas** (pedido → pagamento → entrega)
- Suporte a **vendedores terceirizados** (marketplace)

## Relacionamentos Chave
- `Cliente` → `Pedido` (relação 1:N)
- `Produto` ↔ `Fornecedor` (relação N:M via `ProdutoFornecedor`)
- `Produto` ↔ `Pedido` (relação N:M via `ProdutoPedido`)
- Pagamento especializado (`Cartão`/`PIX`)

## Atributos Críticos
- Valores monetários como `DECIMAL(10,2)`
- CPF/CNPJ com constraints `UNIQUE`
- Status operacionais (pedido, pagamento, entrega)
- Datas completas do ciclo de venda

## 🔍 Consultas Principais
- Relatórios de vendas por categoria/cliente
- Controle de estoque e produtos mais vendidos
- Análise de métodos de pagamento
- Monitoramento do fluxo de entregas
