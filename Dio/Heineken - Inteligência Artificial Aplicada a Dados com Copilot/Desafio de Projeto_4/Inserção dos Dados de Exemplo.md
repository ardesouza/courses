## 💡 Dados de Exemplo Utilizado para o Banco de Dados da Oficina Mecânica
```SQL
-- Inserindo clientes
INSERT INTO Clientes (Nome, Telefone, Email, Endereco, DataCadastro) VALUES
('João Silva', '(11) 9999-8888', 'joao.silva@email.com', 'Rua das Flores, 123 - São Paulo/SP', '2023-01-15'),
('Maria Oliveira', '(11) 7777-6666', 'maria.oliveira@email.com', 'Av. Paulista, 1000 - São Paulo/SP', '2023-02-20'),
('Carlos Souza', '(11) 5555-4444', 'carlos.souza@email.com', 'Rua Augusta, 500 - São Paulo/SP', '2023-03-10'),
('Ana Costa', '(11) 3333-2222', 'ana.costa@email.com', 'Alameda Santos, 200 - São Paulo/SP', '2023-04-05'),
('Pedro Santos', '(11) 1111-0000', 'pedro.santos@email.com', 'Rua Oscar Freire, 300 - São Paulo/SP', '2023-05-12');

-- Inserindo veículos
INSERT INTO Veiculos (ClienteID, Marca, Modelo, Ano, Placa, Chassi) VALUES
(1, 'Volkswagen', 'Gol', 2018, 'ABC1D23', '9BWZZZ377VT004251'),
(1, 'Fiat', 'Uno', 2015, 'DEF4G56', '9BFZZZ377VT004252'),
(2, 'Chevrolet', 'Onix', 2020, 'GHI7J89', '9BGZZZ377VT004253'),
(3, 'Ford', 'Ka', 2019, 'KLM1N23', '9BHZZZ377VT004254'),
(4, 'Hyundai', 'HB20', 2021, 'OPQ4R56', '9BJZZZ377VT004255'),
(5, 'Toyota', 'Corolla', 2022, 'STU7V89', '9BKZZZ377VT004256');

-- Inserindo mecânicos
INSERT INTO Mecanicos (Nome, Especialidade, Telefone, Email, DataContratacao) VALUES
('Roberto Alves', 'Motor e Transmissão', '(11) 98888-7777', 'roberto.alves@oficina.com', '2022-01-10'),
('Fernanda Lima', 'Suspensão e Freios', '(11) 97777-6666', 'fernanda.lima@oficina.com', '2022-03-15'),
('Marcos Ribeiro', 'Elétrica Automotiva', '(11) 96666-5555', 'marcos.ribeiro@oficina.com', '2022-05-20'),
('Patricia Gomes', 'Injeção Eletrônica', '(11) 95555-4444', 'patricia.gomes@oficina.com', '2022-07-25');

-- Inserindo serviços
INSERT INTO Servicos (Nome, Descricao, TempoEstimado, Categoria) VALUES
('Troca de óleo', 'Troca de óleo do motor e filtro', '00:45:00', 'Preventiva'),
('Alinhamento', 'Alinhamento de direção', '01:00:00', 'Suspensão'),
('Balanceamento', 'Balanceamento de rodas', '00:30:00', 'Suspensão'),
('Troca de pastilhas', 'Troca de pastilhas de freio dianteiras', '01:30:00', 'Freios'),
('Diagnóstico elétrico', 'Verificação de problemas no sistema elétrico', '02:00:00', 'Elétrica'),
('Limpeza de bicos', 'Limpeza de bicos injetores', '02:30:00', 'Injeção'),
('Troca de correia dentada', 'Substituição da correia dentada e tensor', '03:00:00', 'Motor');

-- Inserindo peças
INSERT INTO Pecas (Nome, Descricao, PrecoUnitario, QuantidadeEstoque, Fornecedor) VALUES
('Óleo 10W40', 'Óleo sintético 10W40 1L', 25.90, 50, 'Lubrificantes Brasil'),
('Filtro de óleo', 'Filtro de óleo para VW Gol 1.0', 18.50, 30, 'Filtros Autoparts'),
('Pastilhas de freio', 'Pastilhas dianteiras para Fiat Uno', 89.90, 20, 'Freios Master'),
('Correia dentada', 'Correia dentada para Ford Ka 1.0', 120.00, 15, 'Correias Auto'),
('Bico injetor', 'Bico injetor para Chevrolet Onix 1.4', 185.00, 10, 'Injeção Total'),
('Amortecedor', 'Amortecedor dianteiro para Hyundai HB20', 220.00, 12, 'Suspensão Premium'),
('Vela de ignição', 'Vela de ignição iridium', 35.00, 40, 'Elétrica Auto');

-- Inserindo ordens de serviço
INSERT INTO OrdensServico (VeiculoID, MecanicoID, DataAbertura, DataConclusao, Status, DescricaoProblema) VALUES
(1, 1, '2023-06-01 09:00:00', '2023-06-01 10:30:00', 'Concluído', 'Troca de óleo e filtro conforme manual'),
(3, 2, '2023-06-02 10:00:00', '2023-06-02 12:00:00', 'Concluído', 'Alinhamento e balanceamento após troca de pneus'),
(2, 3, '2023-06-03 14:00:00', NULL, 'Em andamento', 'Problemas no sistema elétrico - faróis não acendem'),
(4, 4, '2023-06-04 08:30:00', '2023-06-04 11:00:00', 'Concluído', 'Limpeza de bicos injetores e diagnóstico completo'),
(5, 1, '2023-06-05 13:00:00', NULL, 'Aguardando peças', 'Troca de correia dentada - aguardando chegada da peça');

-- Inserindo itens de serviço nas OS
INSERT INTO ItensServicoOS (OSID, ServicoID, Quantidade, PrecoUnitario, Observacoes) VALUES
(1, 1, 1, 80.00, 'Óleo sintético premium'),
(2, 2, 1, 120.00, 'Alinhamento computadorizado'),
(2, 3, 1, 80.00, 'Balanceamento com pesos novos'),
(4, 6, 1, 200.00, 'Limpeza ultrassônica dos bicos'),
(5, 7, 1, 350.00, 'Troca completa da correia dentada');

-- Inserindo itens de peças nas OS
INSERT INTO ItensPecaOS (OSID, PecaID, Quantidade, PrecoUnitario) VALUES
(1, 1, 4, 25.90),
(1, 2, 1, 18.50),
(4, 5, 4, 185.00),
(5, 4, 1, 120.00);

-- Inserindo pagamentos
INSERT INTO Pagamentos (OSID, DataPagamento, ValorTotal, FormaPagamento, Status) VALUES
(1, '2023-06-01 10:35:00', 221.10, 'Cartão de crédito', 'Pago'),
(2, '2023-06-02 12:05:00', 200.00, 'Dinheiro', 'Pago'),
(4, '2023-06-04 11:10:00', 940.00, 'PIX', 'Pago');

-- Inserindo agendamentos
INSERT INTO Agendamentos (ClienteID, VeiculoID, DataHora, ServicoSolicitado, Status) VALUES
(2, 3, '2023-06-10 09:00:00', 'Troca de pastilhas de freio', 'Confirmado'),
(3, 4, '2023-06-11 14:00:00', 'Diagnóstico elétrico', 'Pendente'),
(5, 6, '2023-06-12 10:30:00', 'Revisão 30.000 km', 'Confirmado');
