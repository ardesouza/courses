## 💡 Script SQL de Criação do Banco e das Tabelas
```sql
-- Criação do banco de dados
CREATE DATABASE OficinaMecanica;
USE OficinaMecanica;

-- Tabela de Clientes
CREATE TABLE Clientes (
    ClienteID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Telefone VARCHAR(20),
    Email VARCHAR(100),
    Endereco VARCHAR(200),
    DataCadastro DATE NOT NULL
);

-- Tabela de Veículos
CREATE TABLE Veiculos (
    VeiculoID INT PRIMARY KEY AUTO_INCREMENT,
    ClienteID INT NOT NULL,
    Marca VARCHAR(50) NOT NULL,
    Modelo VARCHAR(50) NOT NULL,
    Ano INT,
    Placa VARCHAR(15) UNIQUE,
    Chassi VARCHAR(50) UNIQUE,
    FOREIGN KEY (ClienteID) REFERENCES Clientes(ClienteID)
);

-- Tabela de Serviços
CREATE TABLE Servicos (
    ServicoID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Descricao TEXT,
    TempoEstimado TIME,
    Categoria VARCHAR(50)
);

-- Tabela de Peças/Produtos
CREATE TABLE Pecas (
    PecaID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Descricao TEXT,
    PrecoUnitario DECIMAL(10,2) NOT NULL,
    QuantidadeEstoque INT NOT NULL,
    Fornecedor VARCHAR(100)
);

-- Tabela de Funcionários/Mecânicos
CREATE TABLE Mecanicos (
    MecanicoID INT PRIMARY KEY AUTO_INCREMENT,
    Nome VARCHAR(100) NOT NULL,
    Especialidade VARCHAR(100),
    Telefone VARCHAR(20),
    Email VARCHAR(100),
    DataContratacao DATE NOT NULL
);

-- Tabela de Ordens de Serviço (OS)
CREATE TABLE OrdensServico (
    OSID INT PRIMARY KEY AUTO_INCREMENT,
    VeiculoID INT NOT NULL,
    MecanicoID INT NOT NULL,
    DataAbertura DATETIME NOT NULL,
    DataConclusao DATETIME,
    Status VARCHAR(20) NOT NULL,
    DescricaoProblema TEXT,
    FOREIGN KEY (VeiculoID) REFERENCES Veiculos(VeiculoID),
    FOREIGN KEY (MecanicoID) REFERENCES Mecanicos(MecanicoID)
);

-- Tabela de Itens da OS (Serviços realizados)
CREATE TABLE ItensServicoOS (
    ItemServicoID INT PRIMARY KEY AUTO_INCREMENT,
    OSID INT NOT NULL,
    ServicoID INT NOT NULL,
    Quantidade INT DEFAULT 1,
    PrecoUnitario DECIMAL(10,2) NOT NULL,
    Observacoes TEXT,
    FOREIGN KEY (OSID) REFERENCES OrdensServico(OSID),
    FOREIGN KEY (ServicoID) REFERENCES Servicos(ServicoID)
);

-- Tabela de Itens da OS (Peças utilizadas)
CREATE TABLE ItensPecaOS (
    ItemPecaID INT PRIMARY KEY AUTO_INCREMENT,
    OSID INT NOT NULL,
    PecaID INT NOT NULL,
    Quantidade INT NOT NULL,
    PrecoUnitario DECIMAL(10,2) NOT NULL,
    FOREIGN KEY (OSID) REFERENCES OrdensServico(OSID),
    FOREIGN KEY (PecaID) REFERENCES Pecas(PecaID)
);

-- Tabela de Pagamentos
CREATE TABLE Pagamentos (
    PagamentoID INT PRIMARY KEY AUTO_INCREMENT,
    OSID INT NOT NULL,
    DataPagamento DATETIME NOT NULL,
    ValorTotal DECIMAL(10,2) NOT NULL,
    FormaPagamento VARCHAR(50) NOT NULL,
    Status VARCHAR(20) NOT NULL,
    FOREIGN KEY (OSID) REFERENCES OrdensServico(OSID)
);

-- Tabela de Agendamentos
CREATE TABLE Agendamentos (
    AgendamentoID INT PRIMARY KEY AUTO_INCREMENT,
    ClienteID INT NOT NULL,
    VeiculoID INT NOT NULL,
    DataHora DATETIME NOT NULL,
    ServicoSolicitado VARCHAR(200),
    Status VARCHAR(20) NOT NULL,
    FOREIGN KEY (ClienteID) REFERENCES Clientes(ClienteID),
    FOREIGN KEY (VeiculoID) REFERENCES Veiculos(VeiculoID)
);
