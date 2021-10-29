# DANNY MA 8 WEEKS SQL Challange


## WEEK 1 - Danny's Dinner

/* --------------------
   Case Study Questions
   --------------------*/

1. What is the total amount each customer spent at the restaurant?
2. How many days has each customer visited the restaurant?
3. What was the first item from the menu purchased by each customer?
4. What is the most purchased item on the menu and how many times was it purchased by all customers?
5. Which item was the most popular for each customer?
6. Which item was purchased first by the customer after they became a member?
7. Which item was purchased just before the customer became a member?
8. What is the total items and amount spent for each member before they became a member?
9.  If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?
10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customer A and B have at the end of January?



-- Question 1 : What is the total amount each customer spent at the restaurant?
``` sql
SELECT customer_id, sum(price) AS money_spent FROM sales 
	JOIN menu ON menu.product_id = sales.product_id
	GROUP BY customer_id
```


-- 2. How many days has each customer visited the restaurant?
``` sql
SELECT customer_id, COUNT(DISTINCT(order_date)) FROM sales
	GROUP BY customer_id
```

-- 3. What was the first item from the menu purchased by each customer?
```sql
SELECT * FROM sales s
	WHERE s.order_date = ANY (SELECT MIN(order_date) FROM sales GROUP BY customer_id)
```


-- 4. What is the most purchased item on the menu and how many times was it purchased by all customers?
```sql
SELECT  COUNT(product_name) AS count, product_name FROM sales s 
	JOIN menu m ON s.product_id = m.product_id
	GROUP BY product_name ORDER BY count DESC LIMIT 1
```

