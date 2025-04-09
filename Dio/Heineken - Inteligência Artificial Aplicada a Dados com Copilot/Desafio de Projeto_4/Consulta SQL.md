# 💡 Consultas SQL para o Banco da Oficina Mecânica

## 1. Quais clientes possuem mais de um veículo cadastrado na oficina?
```SQL
SELECT c.Nome, COUNT(v.VeiculoID) AS QuantidadeVeiculos
FROM Clientes c
JOIN Veiculos v ON c.ClienteID = v.ClienteID
GROUP BY c.ClienteID, c.Nome
HAVING COUNT(v.VeiculoID) > 1
ORDER BY QuantidadeVeiculos DESC;
```
## 2. Quais ordens de serviço estão em andamento ou aguardando peças?
```SQL
SELECT os.OSID, v.Modelo AS Veiculo, c.Nome AS Cliente, m.Nome AS Mecanico, os.Status
FROM OrdensServico os
JOIN Veiculos v ON os.VeiculoID = v.VeiculoID
JOIN Clientes c ON v.ClienteID = c.ClienteID
JOIN Mecanicos m ON os.MecanicoID = m.MecanicoID
WHERE os.Status IN ('Em andamento', 'Aguardando peças')
ORDER BY os.DataAbertura;
```
## 3. Qual o valor total gasto por cada cliente na oficina?
```SQL
SELECT c.Nome AS Cliente, SUM(p.ValorTotal) AS TotalGasto
FROM Clientes c
JOIN Veiculos v ON c.ClienteID = v.ClienteID
JOIN OrdensServico os ON v.VeiculoID = os.VeiculoID
JOIN Pagamentos p ON os.OSID = p.OSID
GROUP BY c.ClienteID, c.Nome
HAVING SUM(p.ValorTotal) > 0
ORDER BY TotalGasto DESC;
```
## 4. Quais são os serviços mais realizados na oficina?
```SQL
SELECT s.Nome AS Servico, COUNT(iso.ItemServicoID) AS Quantidade
FROM Servicos s
JOIN ItensServicoOS iso ON s.ServicoID = iso.ServicoID
GROUP BY s.ServicoID, s.Nome
HAVING COUNT(iso.ItemServicoID) > 0
ORDER BY Quantidade DESC;
```
## 5. Quais mecânicos realizaram mais ordens de serviço?
```SQL
SELECT m.Nome AS Mecanico, COUNT(os.OSID) AS OrdensRealizadas
FROM Mecanicos m
JOIN OrdensServico os ON m.MecanicoID = os.MecanicoID
GROUP BY m.MecanicoID, m.Nome
HAVING COUNT(os.OSID) > 0
ORDER BY OrdensRealizadas DESC;
```
## 6. Quais peças estão com estoque abaixo de 15 unidades?
```SQL
SELECT Nome, QuantidadeEstoque
FROM Pecas
WHERE QuantidadeEstoque < 15
ORDER BY QuantidadeEstoque ASC;
```
## 7. Qual o faturamento mensal da oficina?
```SQL
SELECT 
    MONTH(DataPagamento) AS Mes,
    SUM(ValorTotal) AS Faturamento
FROM Pagamentos
WHERE YEAR(DataPagamento) = YEAR(CURRENT_DATE)
GROUP BY MONTH(DataPagamento)
HAVING SUM(ValorTotal) > 0
ORDER BY Mes;
```
## 8. Quais veículos têm agendamentos confirmados para os próximos dias?
```SQL
SELECT 
    v.Marca, 
    v.Modelo, 
    v.Placa, 
    c.Nome AS Cliente, 
    a.DataHora, 
    a.ServicoSolicitado
FROM Agendamentos a
JOIN Veiculos v ON a.VeiculoID = v.VeiculoID
JOIN Clientes c ON a.ClienteID = c.ClienteID
WHERE a.Status = 'Confirmado'
AND a.DataHora BETWEEN CURRENT_DATE AND DATE_ADD(CURRENT_DATE, INTERVAL 7 DAY)
ORDER BY a.DataHora;
```
## 9. Quais serviços demoram mais de 1 hora para serem realizados?
```SQL
SELECT Nome, TempoEstimado
FROM Servicos
WHERE TempoEstimado > '01:00:00'
ORDER BY TempoEstimado DESC;
```
## 10. Quais clientes têm pagamentos pendentes (ordens concluídas sem pagamento registrado)?
```SQL
SELECT c.Nome AS Cliente, os.OSID, os.DataConclusao
FROM Clientes c
JOIN Veiculos v ON c.ClienteID = v.ClienteID
JOIN OrdensServico os ON v.VeiculoID = os.VeiculoID
LEFT JOIN Pagamentos p ON os.OSID = p.OSID
WHERE os.Status = 'Concluído'
AND p.PagamentoID IS NULL
ORDER BY os.DataConclusao;
```
## 11. Qual a média de valor das ordens de serviço por mecânico?
```SQL
SELECT 
    m.Nome AS Mecanico,
    AVG(p.ValorTotal) AS MediaValorOS
FROM Mecanicos m
JOIN OrdensServico os ON m.MecanicoID = os.MecanicoID
JOIN Pagamentos p ON os.OSID = p.OSID
GROUP BY m.MecanicoID, m.Nome
HAVING COUNT(os.OSID) > 0
ORDER BY MediaValorOS DESC;
```
## 12. Quais peças foram mais utilizadas nas ordens de serviço?
```SQL
SELECT 
    p.Nome AS Peca,
    SUM(ipo.Quantidade) AS QuantidadeUtilizada,
    SUM(ipo.Quantidade * ipo.PrecoUnitario) AS ValorTotal
FROM Pecas p
JOIN ItensPecaOS ipo ON p.PecaID = ipo.PecaID
GROUP BY p.PecaID, p.Nome
HAVING SUM(ipo.Quantidade) > 0
ORDER BY QuantidadeUtilizada DESC;
```
