
# Task: Merge two tables(Sales and products)
### Description:
Merge two tables ( Sales and products), , group the data by month (extracting the month from the date) and by category to discover which type of products generated the most revenue

#### Solution:
```sql
SELECT p.categoria,
SUM(v.valor_total) as max_valor_total from produtos p
JOIN vendas v on p.id_produto = v.id_produto
GROUP BY p.categoria
```

#### Why this solutions work ?

When you write a SQL query, it doesn't read everything at once; it processes the instructions in a specfic order. For the example:

 -  **The collection**: (FROM and JOIN): First, it gather the information in two tables, it get one record of the sales and gather with a products sold. In this momento, it has a larget unified datasets containg all the sales.
 - **The separtion** (GROUP BY) When it read ```GROUP BY p.categoria ```, it get a lot of data and started to separate this records in smaller stacks, based on categories, it get a physical stack on the table called "eletrônico"(throw the sales of "notebook" and "mouses" ), create other stack called "Móveis" and "Papelaria" and so on.
- **The count**(SELECT and SUM): With 5 stacks ready in the table, it finaly process the ```SELECT```. It get a calculator and goes to the stack "Eletronicos", add up all the values that only are there and create final report "Eletronicos: R$ 1000". Then it repsets to zero the calculator and go to other stack, reapeating the process