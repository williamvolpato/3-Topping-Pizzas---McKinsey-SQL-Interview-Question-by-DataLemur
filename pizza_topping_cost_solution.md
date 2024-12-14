# Pizza Topping Cost Calculation
### English Version

# Pizza Topping Cost Calculation

This problem is from DataLemur: [Link to the problem](https://datalemur.com/questions/pizzas-topping-cost)

### Problem Statement:
You are a consultant for a major pizza chain that will be running a promotion where all 3-topping pizzas will be sold for a fixed price, and are trying to understand the costs involved.

Given a list of pizza toppings, consider all the possible 3-topping pizzas, and print out the total cost of those 3 toppings. Sort the results with the highest total cost on the top followed by pizza toppings in ascending order.

Break ties by listing the ingredients in alphabetical order, starting from the first ingredient, followed by the second and third.

### Example Input:
| topping_name | ingredient_cost |
|--------------|-----------------|
| Pepperoni    | 0.50            |
| Sausage      | 0.70            |
| Chicken      | 0.55            |
| Extra Cheese | 0.40            |

### Example Output:
| pizza                           | total_cost |
|---------------------------------|------------|
| Chicken,Pepperoni,Sausage       | 1.75       |
| Chicken,Extra Cheese,Sausage   | 1.65       |
| Extra Cheese,Pepperoni,Pepperoni| 1.60       |
| Extra Cheese,Extra Cheese,Pepperoni| 1.45    |

### SQL Query Solution:

```sql
WITH pizza_combinations AS (
  SELECT 
    t1.topping_name AS topping_1, 
    t2.topping_name AS topping_2, 
    t3.topping_name AS topping_3,
    (t1.ingredient_cost + t2.ingredient_cost + t3.ingredient_cost) AS total_cost
  FROM pizza_toppings t1
  JOIN pizza_toppings t2 ON t1.topping_name < t2.topping_name
  JOIN pizza_toppings t3 ON t2.topping_name < t3.topping_name
)
SELECT 
  CONCAT(pizza_combinations.topping_1, ',', pizza_combinations.topping_2, ',', pizza_combinations.topping_3) AS pizza,
  pizza_combinations.total_cost
FROM pizza_combinations
ORDER BY pizza_combinations.total_cost DESC, pizza_combinations.topping_1, pizza_combinations.topping_2, pizza_combinations.topping_3;
```

### Explanation:

- **CTE (Common Table Expression) `pizza_combinations`**: Generates all the possible combinations of three toppings using `JOIN` with the table itself. The condition `t1.topping_name < t2.topping_name` and `t2.topping_name < t3.topping_name` ensures there are no repeated toppings in the combinations and that the toppings are listed alphabetically.
- **Total Cost Calculation**: For each combination, the cost of the three toppings is summed up.
- **Ordering**: The result is ordered by total cost in descending order, and in case of ties, the toppings are ordered alphabetically.

### Example in Action:

For the given input, the SQL query will return the combinations of toppings sorted by their total cost and alphabetical order.


### Versão em Português

# Cálculo de Custo de Toppings para Pizza

Este problema é do DataLemur: [Link para o problema](https://datalemur.com/questions/pizzas-topping-cost)

### Enunciado do Problema:
Você é um consultor para uma grande rede de pizzarias que estará realizando uma promoção onde todas as pizzas de 3 toppings serão vendidas por um preço fixo, e está tentando entender os custos envolvidos.

Dada uma lista de toppings de pizza, considere todas as pizzas possíveis com 3 toppings e imprima o custo total desses 3 toppings. Ordene os resultados com o maior custo total no topo, seguido pelos toppings em ordem crescente.

Em caso de empate, liste os ingredientes em ordem alfabética, começando pelo primeiro ingrediente, seguido do segundo e do terceiro.

### Exemplo de Entrada:
| topping_name | ingredient_cost |
|--------------|-----------------|
| Pepperoni    | 0.50            |
| Sausage      | 0.70            |
| Chicken      | 0.55            |
| Extra Cheese | 0.40            |

### Exemplo de Saída:
| pizza                           | total_cost |
|---------------------------------|------------|
| Chicken,Pepperoni,Sausage       | 1.75       |
| Chicken,Extra Cheese,Sausage   | 1.65       |
| Extra Cheese,Pepperoni,Pepperoni| 1.60       |
| Extra Cheese,Extra Cheese,Pepperoni| 1.45    |

### Solução SQL:

```sql
WITH pizza_combinations AS (
  SELECT 
    t1.topping_name AS topping_1, 
    t2.topping_name AS topping_2, 
    t3.topping_name AS topping_3,
    (t1.ingredient_cost + t2.ingredient_cost + t3.ingredient_cost) AS total_cost
  FROM pizza_toppings t1
  JOIN pizza_toppings t2 ON t1.topping_name < t2.topping_name
  JOIN pizza_toppings t3 ON t2.topping_name < t3.topping_name
)
SELECT 
  CONCAT(pizza_combinations.topping_1, ',', pizza_combinations.topping_2, ',', pizza_combinations.topping_3) AS pizza,
  pizza_combinations.total_cost
FROM pizza_combinations
ORDER BY pizza_combinations.total_cost DESC, pizza_combinations.topping_1, pizza_combinations.topping_2, pizza_combinations.topping_3;
```

### Explicação:

- **CTE (Expressão de Tabela Comum) `pizza_combinations`**: Gera todas as combinações possíveis de três toppings utilizando o `JOIN` da tabela consigo mesma. A condição `t1.topping_name < t2.topping_name` e `t2.topping_name < t3.topping_name` garante que não haja toppings repetidos nas combinações e que eles sejam listados em ordem alfabética.
- **Cálculo do Custo Total**: Para cada combinação, o custo dos três toppings é somado.
- **Ordenação**: O resultado é ordenado pelo custo total de forma decrescente e, em caso de empate, os toppings são ordenados alfabeticamente.

### Exemplo em Ação:

Com a entrada fornecida, a consulta SQL irá retornar as combinações de toppings ordenadas por seu custo total e ordem alfabética.

