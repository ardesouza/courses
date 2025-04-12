# Refinamento do Modelo Conceitual de Banco de Dados

## 🎯 Objetivo
Refinar o modelo de banco de dados para implementar as seguintes funcionalidades:

## Escopo do Refinamento

### 1. Clientes PJ e PF
- **Regra**: Cada conta deve ser exclusivamente **Pessoa Física (PF)** ou **Pessoa Jurídica (PJ)**
- **Características**:
  - Dados específicos para PF (ex: CPF, data nascimento)
  - Dados específicos para PJ (ex: CNPJ, razão social)
  - Impossibilidade de uma conta ter ambos os tipos simultaneamente

### 2. Formas de Pagamento
- **Regra**: Um cliente pode cadastrar múltiplos métodos de pagamento
- **Tipos suportados**:
  - Cartão de crédito/débito
  - PIX
  - Boleto bancário
 
### 3. Gestão de Entregas
- **Componentes principais**:
  - Código de rastreio único
  - Status da entrega (com fluxo definido)
  - Histórico de atualizações
- **Estados possíveis**:
  - Em preparação
  - Enviado
  - Em trânsito
  - Entregue
  - Problema na entrega

## Benefícios Esperados
- Maior flexibilidade no cadastro de clientes
- Experiência de pagamento mais completa
- Melhor visibilidade do processo de entrega
- Adequação a requisitos legais (PF/PJ)
