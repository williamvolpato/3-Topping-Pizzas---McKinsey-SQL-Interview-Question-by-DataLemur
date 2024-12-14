
# Pizza Topping Cost Calculation

This project is based on the DataLemur challenge: [Link to the problem](https://datalemur.com/questions/pizzas-topping-cost)

## Problem Overview
The task is to calculate the total cost of 3-topping pizzas. Given a list of pizza toppings and their respective costs, we need to:
- Generate all possible 3-topping pizza combinations.
- Calculate the total cost for each combination.
- Sort the results by the highest total cost, followed by alphabetical order of the toppings.

## SQL Query Solution
The SQL solution calculates all possible combinations of three toppings, sums their costs, and orders the results as specified.

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

## Example Input & Output
### Input
| topping_name | ingredient_cost |
|--------------|-----------------|
| Pepperoni    | 0.50            |
| Sausage      | 0.70            |
| Chicken      | 0.55            |
| Extra Cheese | 0.40            |

### Output
| pizza                           | total_cost |
|---------------------------------|------------|
| Chicken,Pepperoni,Sausage       | 1.75       |
| Chicken,Extra Cheese,Sausage   | 1.65       |
| Extra Cheese,Pepperoni,Pepperoni| 1.60       |
| Extra Cheese,Extra Cheese,Pepperoni| 1.45    |

## Conclusion
This project demonstrates the application of SQL in solving real-world problems like cost calculation and optimization, providing a valuable example for database and query management techniques.
