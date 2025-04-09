## 💡 Dados de Exemplo Utilizado para o Banco de Dados de E-commerce
```SQL
-- Inserção de Clientes
INSERT INTO Cliente (Nome, Tipo, Endereco, Telefone, CPF_CNPJ, Email) VALUES
('João Silva', 'PF', 'Rua das Flores, 123 - São Paulo/SP', '11987654321', '12345678901', 'joao.silva@email.com'),
('Maria Oliveira', 'PF', 'Av. Paulista, 1000 - São Paulo/SP', '11912345678', '98765432109', 'maria.oliveira@email.com'),
('Tech Solutions Ltda', 'PJ', 'Rua da Tecnologia, 456 - Campinas/SP', '1933334444', '12345678000199', 'contato@techsolutions.com'),
('Fashion Store', 'PJ', 'Alameda Santos, 789 - São Paulo/SP', '1122223333', '98765432000188', 'vendas@fashionstore.com.br');

-- Inserção de Fornecedores
INSERT INTO Fornecedor (RazaoSocial, CNPJ, Endereco, Contato) VALUES
('Eletrônicos Brasil Ltda', '11222333000144', 'Av. Industrial, 500 - São Paulo/SP', 'Carlos Mendes - (11) 4444-5555'),
('Moda Fashion S/A', '99888777000166', 'Rua das Confecções, 200 - Americana/SP', 'Fernanda Costa - (19) 3333-2222'),
('Alimentos Premium', '55444666000177', 'Rodovia dos Alimentos, km 10 - Campinas/SP', 'Roberto Almeida - (19) 7777-8888');

-- Inserção de Produtos
INSERT INTO Produto (Nome, Categoria, Descricao, Valor, Dimensoes, Peso) VALUES
('Smartphone X9', 'Eletrônicos', 'Smartphone com tela de 6.5 polegadas, 128GB', 2499.90, '15x7x0.8 cm', 0.18),
('Notebook Ultra Slim', 'Eletrônicos', 'Notebook 14 polegadas, 16GB RAM, SSD 512GB', 4299.00, '32x22x1.5 cm', 1.2),
('Camisa Social Branca', 'Vestuário', 'Camisa social 100% algodão, tamanho M', 129.90, NULL, 0.3),
('Tênis Esportivo', 'Calçados', 'Tênis para corrida, amortecimento premium', 299.90, NULL, 0.4),
('Cesta de Café da Manhã', 'Alimentos', 'Cesta com 10 itens selecionados', 89.90, '30x20x15 cm', 2.5);

-- Inserção de Estoques
INSERT INTO Estoque (Local, Responsavel, TelefoneContato) VALUES
('Centro de Distribuição SP', 'Marcos Oliveira', '1123456789'),
('Armazém Campinas', 'Ana Santos', '1933339999'),
('Depósito Zona Leste', 'Ricardo Pereira', '11988887777');

-- Inserção de Vendedores Terceirizados
INSERT INTO VendedorTerceirizado (RazaoSocial, Local, CNPJ, Contato) VALUES
('Marketplace Express', 'São Paulo/SP', '11222333444455', 'Patricia Lima - (11) 9999-8888'),
('Vendas Online Brasil', 'Rio de Janeiro/RJ', '99888777666644', 'Rodrigo Fernandes - (21) 7777-6666');

-- Inserção de Pedidos
INSERT INTO Pedido (idCliente, StatusPedido, Descricao, DataPedido, DataEnvio, DataEntrega, Frete) VALUES
(1, 'Entregue', 'Compra de smartphone', '2023-01-10 14:30:00', '2023-01-11 09:15:00', '2023-01-13 16:20:00', 15.90),
(2, 'Processando', 'Itens de vestuário', '2023-01-15 10:45:00', NULL, NULL, 12.50),
(3, 'Enviado', 'Pedido corporativo', '2023-01-12 16:20:00', '2023-01-13 14:00:00', NULL, 0.00),
(1, 'Cancelado', 'Pedido duplicado', '2023-01-05 11:30:00', NULL, NULL, 10.00),
(4, 'Entregue', 'Revenda loja física', '2023-01-08 09:15:00', '2023-01-09 08:30:00', '2023-01-11 10:45:00', 0.00);

-- Inserção de Pagamentos
INSERT INTO Pagamento (idPedido, Metodo, ValorTotal, Status, DataPagamento) VALUES
(1, 'Cartão', 2515.80, 'Aprovado', '2023-01-10 14:35:00'),
(2, 'PIX', 142.40, 'Pendente', NULL),
(3, 'Cartão', 4299.00, 'Aprovado', '2023-01-12 16:25:00'),
(5, 'PIX', 89.90, 'Aprovado', '2023-01-08 09:20:00');

-- Inserção de Cartões de Crédito
INSERT INTO CartaoCredito (idPagamento, NumeroCartao, NomeTitular, DataValidade, CodSeguranca, Bandeira) VALUES
(1, '4111111111111111', 'JOAO S SILVA', '2025-12-01', '123', 'Visa'),
(3, '5555555555554444', 'TECH SOLUTIONS LTDA', '2026-10-01', '456', 'Mastercard');

-- Inserção de PIX
INSERT INTO PIX (idPagamento, ChavePIX, TipoChave) VALUES
(2, 'maria.oliveira@email.com', 'Email'),
(4, '12345678901', 'CPF/CNPJ');

-- Inserção de Entregas
INSERT INTO Entrega (idPedido, Status, CodigoRastreio, Transportadora, DataEnvio, DataPrevisaoEntrega) VALUES
(1, 'Entregue', 'BR123456789SP', 'Correios', '2023-01-11 09:15:00', '2023-01-13 18:00:00'),
(3, 'Em trânsito', 'BR987654321SP', 'Transportadora Fast', '2023-01-13 14:00:00', '2023-01-16 18:00:00'),
(5, 'Entregue', 'BR456789123SP', 'Loggi', '2023-01-09 08:30:00', '2023-01-11 12:00:00');

-- Inserção de Produtos por Fornecedor
INSERT INTO ProdutoFornecedor (idFornecedor, idProduto) VALUES
(1, 1),
(1, 2),
(2, 3),
(2, 4),
(3, 5);

-- Inserção de Produtos em Estoque
INSERT INTO ProdutoEstoque (idProduto, idEstoque, Quantidade) VALUES
(1, 1, 50),
(1, 2, 20),
(2, 1, 30),
(3, 3, 100),
(4, 3, 75),
(5, 2, 40);

-- Inserção de Produtos por Pedido
INSERT INTO ProdutoPedido (idProduto, idPedido, Quantidade, PrecoUnitario) VALUES
(1, 1, 1, 2499.90),
(3, 2, 1, 129.90),
(4, 2, 1, 299.90),
(2, 3, 1, 4299.00),
(5, 5, 1, 89.90),
(1, 4, 1, 2499.90);

-- Inserção de Produtos por Vendedor Terceirizado
INSERT INTO ProdutoVendedor (idVendedor, idProduto, Quantidade) VALUES
(1, 1, 15),
(1, 2, 10),
(2, 3, 25),
(2, 4, 20),
(1, 5, 30);
