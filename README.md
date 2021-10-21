# Data Analyst Portfolio Project – Vendor and Employers purchase

![imagem_dados](https://github.com/djalmarodriguess/Data_Analystic_Project/blob/main/Imagem_informa%C3%A7%C3%B5es.png)

## Objetivo da Análise

O objetivo de negócio para este projeto de análise de dados foi um relatório simplorio de vendas dos vendedores terceirizados e empregados contratados.
Com base na solicitação feita à empresa(de forma fictícia), foi implementado um esboço do projeto, com metas e detalhes para melhor acompanhamento 
e diretriz no trabalho,vide tabela abaixo.


|Dados | Objetivo | Análise | Critérios de aceitação|
| :--: |     :--: |    :--: |                  :--: |
|Empregados|Uma visão geral detalhada das vendas de cada um.|Acompanhamento dos produtos que mais venderam.|Um painel do Power BI que me permite filtrar os dados de cada empregado.
|Vendedor(Terceirizado)|Uma visão geral detalhada das vendas de cada um.|Acompanhamento dos produtos que mais venderam.|Um painel do Power BI que me permite filtrar os dados de cada vendedor|

## Limpeza e transformação de dados (SQL)
Para criar o modelo de dados necessário para fazer análises e 
atender às necessidades de negócios definidas na história dos usuários, 
as querys a seguir foram extraídas usando SQL.

Uma fonte de dados (ordens de compra dos clientes) foi fornecida  
e conectada ao modelo de dados em uma etapa posterior do processo.

### Abaixo estão as instruções SQL para limpar e transformar os dados necessários.

#### Número de vendas por vendedor terceirizado.
```
    --Número de vendas por vendedor terceirizados.
    --ID dos vendedores (Não tem os nomes na tabela)
    --Valor total vendido por cada um.
    --Número de vendas.
select ph.VendorID as "ID do Vendedor", 
sum(pd.LineTotal) as "Valor total vendido",
count(ph.VendorID) as "Número de vendas"
from Purchasing.PurchaseOrderDetail pd 
    join Purchasing.PurchaseOrderHeader ph
      on pd.PurchaseOrderID = PurchaseOrderDetailID
    --Agupados pela Id do vendedor.
    group by ph.VendorID 
    --Query Ordenada de acordo com o número de vendas.
    ORDER by count(ph.VendorID);
```

#### Número de vendas dos empregados da empresa
```
  --Número de vendas dos empregados da empresa.
	--ID dos empregados (Não tem os nomes na tabela)
	--Valor total vendido por cada um.
	--Número de vendas.
select ph.EmployeeID as "ID do Empregado", 
sum(pd.LineTotal) as "Valor total vendido",
count(ph.VendorID) as "Número de vendas"
from Purchasing.PurchaseOrderDetail pd 
	join Purchasing.PurchaseOrderHeader ph
	  on pd.PurchaseOrderID = PurchaseOrderDetailID
	--Agrupados pelo Id do vendedor.
	group by ph.EmployeeID 
	--Query Ordenada de acordo com o número de vendas.
	ORDER by ph.EmployeeID;
```

#### Quais produtos cada vendedos vendeu mais
```
  --Quais produtos cada vendedos vendeu mais
	--ID dos vendedores
	--Valor do item mais caro.
	--Nome do produto.
SELECT ph.VendorID as "Id Vendedor",
max(p.StandardCost) as "Valor do produto mais caro",
max(p.Name) as "Nome do Produto"
from Production.Product p 
	join Purchasing.PurchaseOrderDetail pd
	  on p.ProductID = pd.PurchaseOrderDetailID 
	join Purchasing.PurchaseOrderHeader ph
	  on pd.PurchaseOrderID = ph.PurchaseOrderID
	group by ph.VendorID
	--Query ordenada pelo valor do item mais caro
	order by max(p.StandardCost) desc;
```

#### Quais produtos cada empregado vendeu mais
```
  --Quais produtos cada empregado vendeu mais.
	--ID dos empregados
	--Valor do item mais caro.
	--Nome do produto.
SELECT ph.EmployeeID as "Id Empregado",
max(p.StandardCost) as "Valor do produto mais caro",
max(p.Name) as "Nome do Produto"
from Production.Product p 
	join Purchasing.PurchaseOrderDetail pd
		on p.ProductID = pd.PurchaseOrderDetailID 
	join Purchasing.PurchaseOrderHeader ph
		on pd.PurchaseOrderID = ph.PurchaseOrderID
	group by ph.EmployeeID 
	--Query ordenada pelo valor do item mais caro
	order by max(p.StandardCost) desc;
```

## Modelo de dados

Abaixo está uma captura de tela do modelo de dados e as conecções das tabelas.

![tabela_conectada](https://github.com/djalmarodriguess/Data_Analystic_Project/blob/main/tabelas_conectadas.png)

## Painel de gerenciamento das vendas

Os gráficos não mostram somente os valores que cada vendedor terceirizado ou empregado vendeu, 
mas também valores totais de vendas, valores por categorias, porcentagem dos produtos por venda e 
o período de cada venda(podendo ser ajustado para qualquer data no período de venda).
Tendo assim de forma mais clara e fácil de identificação os dados necessários para as devidas tomadas de ação.

![](https://app.powerbi.com/view?r=eyJrIjoiZGI2MjExZTgtMDBmYy00NWIzLWIzZmUtYmQ5NGM5YTBkMzIyIiwidCI6IjQzZDMwZGIxLThkNGItNDA5Yi04ZWYzLWVlODRmZDRjZGIzOSJ9)











