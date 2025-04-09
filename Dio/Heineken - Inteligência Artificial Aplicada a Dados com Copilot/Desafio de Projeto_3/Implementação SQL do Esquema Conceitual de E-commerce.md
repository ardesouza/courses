## 💡 Script SQL de Criação do Bancos e das Tabelas
```sql
-- Criação do banco de dados
CREATE DATABASE ecommerce;
USE ecommerce;

-- Tabela Cliente
CREATE TABLE Cliente (
    idCliente INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(45) NOT NULL,
    Tipo ENUM('PF', 'PJ') NOT NULL,
    Endereco VARCHAR(45),
    Telefone VARCHAR(15),  -- Alterado para VARCHAR para formatos internacionais
    CPF_CNPJ VARCHAR(14),  -- Adicionado para armazenar documento
    Email VARCHAR(45),
    DataCadastro DATETIME DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT unique_cpf_cnpj UNIQUE (CPF_CNPJ)
);

-- Tabela Fornecedor
CREATE TABLE Fornecedor (
    idFornecedor INT AUTO_INCREMENT PRIMARY KEY,
    RazaoSocial VARCHAR(45) NOT NULL,
    CNPJ VARCHAR(14) NOT NULL,
    Endereco VARCHAR(45),
    Contato VARCHAR(45),
    CONSTRAINT unique_cnpj UNIQUE (CNPJ)
);

-- Tabela Produto
CREATE TABLE Produto (
    idProduto INT AUTO_INCREMENT PRIMARY KEY,
    Nome VARCHAR(45) NOT NULL,
    Categoria VARCHAR(45),
    Descricao TEXT,
    Valor DECIMAL(10,2) NOT NULL,  -- Alterado para DECIMAL para valores monetários
    Dimensoes VARCHAR(45),
    Peso DECIMAL(10,2)
);

-- Tabela Estoque
CREATE TABLE Estoque (
    idEstoque INT AUTO_INCREMENT PRIMARY KEY,
    Local VARCHAR(45) NOT NULL,
    Responsavel VARCHAR(45),
    TelefoneContato VARCHAR(15)
);

-- Tabela Pedido
CREATE TABLE Pedido (
    idPedido INT AUTO_INCREMENT PRIMARY KEY,
    idCliente INT NOT NULL,
    StatusPedido VARCHAR(45) NOT NULL,
    Descricao VARCHAR(100),
    DataPedido DATETIME DEFAULT CURRENT_TIMESTAMP,
    DataEnvio DATETIME,
    DataEntrega DATETIME,
    Frete DECIMAL(10,2),
    FOREIGN KEY (idCliente) REFERENCES Cliente(idCliente)
);

-- Tabela VendedorTerceirizado
CREATE TABLE VendedorTerceirizado (
    idVendedor INT AUTO_INCREMENT PRIMARY KEY,
    RazaoSocial VARCHAR(45) NOT NULL,
    Local VARCHAR(45),
    CNPJ VARCHAR(14),
    Contato VARCHAR(45),
    CONSTRAINT unique_cnpj_vendedor UNIQUE (CNPJ)
);

-- Tabela Pagamento
CREATE TABLE Pagamento (
    idPagamento INT AUTO_INCREMENT PRIMARY KEY,
    idPedido INT NOT NULL,
    Metodo ENUM('Cartão', 'PIX', 'Boleto') NOT NULL,
    ValorTotal DECIMAL(10,2) NOT NULL,
    Status VARCHAR(45) NOT NULL,
    DataPagamento DATETIME,
    FOREIGN KEY (idPedido) REFERENCES Pedido(idPedido)
);

-- Tabela CartaoCredito
CREATE TABLE CartaoCredito (
    idCartao INT AUTO_INCREMENT PRIMARY KEY,
    idPagamento INT,
    NumeroCartao VARCHAR(16) NOT NULL,
    NomeTitular VARCHAR(45) NOT NULL,
    DataValidade DATE NOT NULL,
    CodSeguranca VARCHAR(3) NOT NULL,
    Bandeira VARCHAR(20),
    FOREIGN KEY (idPagamento) REFERENCES Pagamento(idPagamento)
);

-- Tabela PIX
CREATE TABLE PIX (
    idPIX INT AUTO_INCREMENT PRIMARY KEY,
    idPagamento INT,
    ChavePIX VARCHAR(45) NOT NULL,
    TipoChave ENUM('CPF/CNPJ', 'Email', 'Telefone', 'Aleatória'),
    DataGeracao DATETIME DEFAULT CURRENT_TIMESTAMP,
    FOREIGN KEY (idPagamento) REFERENCES Pagamento(idPagamento)
);

-- Tabela Entrega
CREATE TABLE Entrega (
    idEntrega INT AUTO_INCREMENT PRIMARY KEY,
    idPedido INT NOT NULL,
    Status VARCHAR(45) NOT NULL,
    CodigoRastreio VARCHAR(45),
    Transportadora VARCHAR(45),
    DataEnvio DATETIME,
    DataPrevisaoEntrega DATETIME,
    FOREIGN KEY (idPedido) REFERENCES Pedido(idPedido)
);

-- Tabelas de relacionamento muitos-para-muitos

-- Produto por Fornecedor
CREATE TABLE ProdutoFornecedor (
    idFornecedor INT,
    idProduto INT,
    PRIMARY KEY (idFornecedor, idProduto),
    FOREIGN KEY (idFornecedor) REFERENCES Fornecedor(idFornecedor),
    FOREIGN KEY (idProduto) REFERENCES Produto(idProduto)
);

-- Produto em Estoque
CREATE TABLE ProdutoEstoque (
    idProduto INT,
    idEstoque INT,
    Quantidade INT NOT NULL DEFAULT 0,
    PRIMARY KEY (idProduto, idEstoque),
    FOREIGN KEY (idProduto) REFERENCES Produto(idProduto),
    FOREIGN KEY (idEstoque) REFERENCES Estoque(idEstoque)
);

-- Produto por Pedido
CREATE TABLE ProdutoPedido (
    idProduto INT,
    idPedido INT,
    Quantidade INT NOT NULL DEFAULT 1,
    PrecoUnitario DECIMAL(10,2) NOT NULL,
    PRIMARY KEY (idProduto, idPedido),
    FOREIGN KEY (idProduto) REFERENCES Produto(idProduto),
    FOREIGN KEY (idPedido) REFERENCES Pedido(idPedido)
);

-- Produto por Vendedor Terceirizado
CREATE TABLE ProdutoVendedor (
    idVendedor INT,
    idProduto INT,
    Quantidade INT NOT NULL DEFAULT 0,
    PRIMARY KEY (idVendedor, idProduto),
    FOREIGN KEY (idVendedor) REFERENCES VendedorTerceirizado(idVendedor),
    FOREIGN KEY (idProduto) REFERENCES Produto(idProduto)
);

-- Índices para melhorar performance
CREATE INDEX idx_produto_categoria ON Produto(Categoria);
CREATE INDEX idx_pedido_cliente ON Pedido(idCliente);
CREATE INDEX idx_pedido_status ON Pedido(StatusPedido);
CREATE INDEX idx_entrega_rastreio ON Entrega(CodigoRastreio);
