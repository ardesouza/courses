## Entidades e Atributos
### 1. Cliente <br>
  id_cliente (PK): INT (ou SERIAL para autoincremento) <br>
  nome: VARCHAR(100) <br>
  endereco: VARCHAR(200) <br>
  telefone: VARCHAR(15) <br>
  email: VARCHAR(100) <br>

### 2. Veículo<br>
  id_veiculo (PK): INT (ou SERIAL para autoincremento)<br>
  placa: VARCHAR(10) (ex: "ABC-1234")<br>
  marca: VARCHAR(50)<br>
  modelo: VARCHAR(50)<br>
  ano: INT<br>
  id_cliente (FK): INT (referência à tabela Cliente)<br>

### 3. Ordem de Serviço (OS)<br>
  id_os (PK): INT (ou SERIAL para autoincremento)<br>
  data_emissao: DATE<br>
  data_conclusao: DATE<br>
  valor_total: DECIMAL(10, 2) (para valores monetários)<br>
  status: VARCHAR(50) (ex: "Em andamento", "Concluído", "Aguardando aprovação")<br>
  id_veiculo (FK): INT (referência à tabela Veículo)<br>
  id_equipe (FK): INT (referência à tabela Equipe)<br>

### 4. Equipe<br>
  id_equipe (PK): INT (ou SERIAL para autoincremento)<br>
  nome_equipe: VARCHAR(100)<br>

### 5. Mecânico<br>
  id_mecanico (PK): INT (ou SERIAL para autoincremento)<br>
  nome: VARCHAR(100)<br>
  endereco: VARCHAR(200)<br>
  especialidade: VARCHAR(100)<br>
  id_equipe (FK): INT (referência à tabela Equipe)<br>

### 6. Serviço<br>
  id_servico (PK): INT (ou SERIAL para autoincremento)<br>
  descricao: VARCHAR(200)<br>
  valor_mao_de_obra: DECIMAL(10, 2)<br>

### 7. Peça<br>
  id_peca (PK): INT (ou SERIAL para autoincremento)<br>
  nome: VARCHAR(100)<br>
  valor: DECIMAL(10, 2)<br>
  
### 8. OS_Servico (Tabela associativa)<br>
  id_os (FK): INT (referência à tabela Ordem de Serviço)<br>
  id_servico (FK): INT (referência à tabela Serviço)<br>
  quantidade: INT<br>

### 9. OS_Peca (Tabela associativa)<br>
  id_os (FK): INT (referência à tabela Ordem de Serviço)<br>
  id_peca (FK): INT (referência à tabela Peça)<br>
  quantidade: INT<br>

## Relacionamentos

1. Cliente possui Veículo:<br>
  Um cliente pode ter vários veículos.<br>
  Um veículo pertence a um único cliente.<br>

2. Veículo gera Ordem de Serviço (OS):<br>
  Um veículo pode ter várias ordens de serviço.<br>
  Uma ordem de serviço pertence a um único veículo.<br>

3. Equipe executa Ordem de Serviço (OS):<br>
  Uma equipe pode executar várias ordens de serviço.<br>
  Uma ordem de serviço é executada por uma única equipe.<br>

4. Mecânico faz parte de Equipe:<br>
  Um mecânico pertence a uma única equipe.<br>
  Uma equipe pode ter vários mecânicos.<br>

5. Ordem de Serviço (OS) contém Serviços e Peças:<br>
  Uma OS pode ter vários serviços e várias peças.<br>
  Um serviço ou uma peça pode estar em várias OSs.<br>

## Descrição textual do diagrama conceitual:

Cliente (1) ---- possui ---- (N) Veículo

Veículo (1) ---- gera ---- (N) Ordem de Serviço (OS)

Equipe (1) ---- executa ---- (N) Ordem de Serviço (OS)

Equipe (1) ---- contém ---- (N) Mecânico

Ordem de Serviço (OS) (1) ---- contém ---- (N) Serviço (via tabela associativa OS_Servico)

Ordem de Serviço (OS) (1) ---- contém ---- (N) Peça (via tabela associativa OS_Peca)

## Considerações Finais
Tabelas Associativas: Foram criadas tabelas associativas (OS_Servico e OS_Peca) para lidar com os relacionamentos muitos-para-muitos entre Ordem de Serviço e Serviço, e entre Ordem de Serviço e Peça.
