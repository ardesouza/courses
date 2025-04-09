# 💡 Consultas SQL para o Banco de Dados de E-commerce

## 1. Consultas Básicas com WHERE e ORDER BY
### 1.1 Listar todos os produtos da categoria 'Eletrônicos' ordenados por valor decrescente
```SQL
SELECT Nome, Descricao, Valor 
FROM Produto 
WHERE Categoria = 'Eletrônicos' 
ORDER BY Valor DESC;
```
### 1.2 Pedidos feitos em janeiro de 2023 com status 'Entregue'
```SQL
SELECT p.idPedido, c.Nome AS Cliente, p.DataPedido, p.DataEntrega
FROM Pedido p
JOIN Cliente c ON p.idCliente = c.idCliente
WHERE p.StatusPedido = 'Entregue' 
  AND p.DataPedido BETWEEN '2023-01-01' AND '2023-01-31'
ORDER BY p.DataEntrega;
```
## 2. Consultas com Agregação e GROUP BY
### 2.1 Valor total de vendas por categoria de produto
```SQL
SELECT pr.Categoria, SUM(pp.Quantidade * pp.PrecoUnitario) AS TotalVendas
FROM ProdutoPedido pp
JOIN Produto pr ON pp.idProduto = pr.idProduto
GROUP BY pr.Categoria
ORDER BY TotalVendas DESC;
```
### 2.2 Quantidade de pedidos por status
```SQL
SELECT StatusPedido, COUNT(*) AS QuantidadePedidos
FROM Pedido
GROUP BY StatusPedido
ORDER BY QuantidadePedidos DESC;
```
## 3. Consultas com HAVING
### 3.1 Clientes que fizeram mais de 1 pedido
```SQL
SELECT c.Nome, COUNT(p.idPedido) AS TotalPedidos
FROM Cliente c
JOIN Pedido p ON c.idCliente = p.idCliente
GROUP BY c.idCliente, c.Nome
HAVING COUNT(p.idPedido) > 1
ORDER BY TotalPedidos DESC;
```
### 3.2 Categorias com valor médio de produtos acima de R$ 500
```SQL
SELECT Categoria, AVG(Valor) AS ValorMedio
FROM Produto
GROUP BY Categoria
HAVING AVG(Valor) > 500
ORDER BY ValorMedio DESC;
```
## 4. Consultas com Subconsultas
### 4.1 Clientes que nunca fizeram pedidos
```SQL
SELECT c.Nome, c.Email
FROM Cliente c
WHERE c.idCliente NOT IN (
    SELECT DISTINCT idCliente 
    FROM Pedido
);
```
### 4.2 Produtos que nunca foram vendidos
```SQL
SELECT p.Nome, p.Valor
FROM Produto p
WHERE p.idProduto NOT IN (
    SELECT DISTINCT idProduto 
    FROM ProdutoPedido
);
```
## 5 Consultas com JOINs Complexos
### 5.1 Detalhes completos dos pedidos (com produtos, cliente e pagamento)
```SQL
SELECT 
    p.idPedido,
    c.Nome AS Cliente,
    pr.Nome AS Produto,
    pp.Quantidade,
    pp.PrecoUnitario,
    (pp.Quantidade * pp.PrecoUnitario) AS Subtotal,
    pa.Metodo AS MetodoPagamento,
    pa.Status AS StatusPagamento,
    p.StatusPedido
FROM Pedido p
JOIN Cliente c ON p.idCliente = c.idCliente
JOIN ProdutoPedido pp ON p.idPedido = pp.idPedido
JOIN Produto pr ON pp.idProduto = pr.idProduto
LEFT JOIN Pagamento pa ON p.idPedido = pa.idPedido
ORDER BY p.idPedido;
```
### 5.2 Estoque crítico (produtos com menos de 10 unidades no estoque principal)
```SQL
SELECT 
    p.Nome,
    pe.Quantidade,
    e.Local AS LocalEstoque
FROM ProdutoEstoque pe
JOIN Produto p ON pe.idProduto = p.idProduto
JOIN Estoque e ON pe.idEstoque = e.idEstoque
WHERE pe.Quantidade < 10 AND e.Local = 'Centro de Distribuição SP'
ORDER BY pe.Quantidade ASC;
```
## 6. Consultas com Funções de Data
### 6.1 Vendas por dia da semana
```SQL
SELECT 
    DAYNAME(DataPedido) AS DiaSemana,
    COUNT(*) AS TotalPedidos,
    SUM(ValorTotal) AS ValorTotal
FROM Pedido p
JOIN Pagamento pa ON p.idPedido = pa.idPedido
GROUP BY DiaSemana, DAYOFWEEK(DataPedido)
ORDER BY DAYOFWEEK(DataPedido);
```



