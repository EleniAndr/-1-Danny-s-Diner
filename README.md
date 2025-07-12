# Case Study #1 - Danny's Diner

<table>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/90492d3d-f48d-4868-b81c-09e5fc742c5e"></td>
    <td>
      <p><strong>Case - Problem Statement</strong></p>
      <p>Danny loves Japanese food, so he opens up a cute little restaurant serving his three favorite dishes: sushi, curry, and ramen. After a few months of running Danny’s Diner, he collects some basic data but isn’t sure how to use it. He’s looking for help to answer a few simple questions that will allow him to improve the experience for his loyal customers. Due to privacy concerns, he shares only a sample of the data — but hopes it’s enough to write fully functioning SQL queries to help him answer his questions!</p>
    </td>
  </tr>
</table>

- There are 3 key datasets for this case study: **sales**, **menu**, **members**. The entity relationship diagram and example data can be inspected below.

<table>
  <tr>
    <th>Entity Relationship Diagram</th>
    <th>Table 1: sales (preview)</th>
    <th>Table 2: menu</th>
    <th>Table 3: members</th>
  </tr>
  <tr>
    <td><img src="https://github.com/user-attachments/assets/246ce3f6-b9bd-43ea-bf19-641a0e2ffc3d" width="350"/></td>
    <td><img src="https://github.com/user-attachments/assets/9254d11a-572b-4c2e-9113-b38ab40fda4c" width="200"/></td>
    <td><img src="https://github.com/user-attachments/assets/43d07543-5d5d-4f38-9835-29a2147308bc" width="200"/></td>
    <td><img src="https://github.com/user-attachments/assets/493768cb-a4bd-4625-b458-030145d6d3ad" width="150"/></td>

  </tr>
</table>

## Case Study Questions & Answers
 Press this [link](https://www.db-fiddle.com/f/2rM8RAnq7h5LLDTzZiRWcd/138), where a fully functioning SQL editor is available to easily access these example datasets.
### 1. What is the total amount each customer spent at the restaurant?

#### 💻 SQL Query
```sql
    SELECT customer_id, SUM(price) as total_amount
    FROM dannys_diner.sales as ds
    JOIN dannys_diner.menu as dm 
    	ON ds.product_id=dm.product_id
    GROUP BY customer_id
    ORDER BY customer_id;
```
#### 🖊 Result

| customer_id | total_amount |
| ----------- | ----------- |
| A           | 76          |
| B           | 74          |
| C           | 36          |

#### 📜 Explanation 
- Inner join the `sales` and `menu` tables on customer_id.
- Calculate the total amount spent by each customer with `SUM(price)` and rename the column to total_amount.
- Group and order by `customer_id` to display each customer's total spending at the restaurant.

### Answer

Total Amount Spent per Customer 
- Customer A spent 76$.
- Customer B spent 74$.
- Customer C spent 36$.
---

### 2. How many days has each customer visited the restaurant?

#### 💻 SQL Query
```sql
SELECT customer_id, COUNT(DISTINCT(order_date)) as days
FROM dannys_diner.sales
GROUP BY customer_id
ORDER BY customer_id;
```
#### 🖊 Result
| customer_id | days |
| ----------- | ---- |
| A           | 4    |
| B           | 6    |
| C           | 3    |
#### 📜 Explanation
- Count the days with `COUNT(DISTINCT(order_date))` so as not to count the same day multiple times.
- Group and order by `customer_id`.
### Answer
Number of Visits per Customer
- Customer A has visited the restaurant 4 times.
- Customer B has visited the restaurant 6 times.
- Customer C has visited the restaurant 3 times.
---
### 3. What was the first item from the menu purchased by each customer?

#### 💻 SQL Query
```sql
WITH first_item AS (
  SELECT customer_id, MIN(order_date) AS first_day
  FROM dannys_diner.sales
  GROUP BY customer_id
)

SELECT fi.customer_id, fi.first_day, dm.product_name
FROM first_item as fi
JOIN dannys_diner.sales as ds
  ON fi.customer_id = ds.customer_id AND fi.first_day = ds.order_date
JOIN dannys_diner.menu dm
  ON ds.product_id = dm.product_id
ORDER BY customer_id;
```
#### 🖊 Result
| customer_id | first_day  | product_name |
| ----------- | ---------- | ------------ |
| A           | 2021-01-01 | sushi        |
| A           | 2021-01-01 | curry        |
| B           | 2021-01-01 | curry        |
| C           | 2021-01-01 | ramen        |
| C           | 2021-01-01 | ramen        |
#### 📜 Explanation
- Find the earliest order date for each customer using the temporary table `first_item`.
- Join the tables `first_item` and `sales` to retrieve the corresponding `product_id` for each customer's first order.
- Join the tables `sales` and `menu` to get the `product_name` for each product_id. 
### Answer
Customer A's first purchase from the menu was sushi and curry.
Customer B's first purchase from the menu was curry.
Customer C's first purchase from the menu was ramen twice.

For customers A and C, it's unclear whether their orders were placed simultaneously or during separate visits on the same day. To determine this with certainty, the exact time of each order would need to be provided.

---
### 4. What is the most purchased item on the menu and how many times was it purchased by all customers?

#### 💻 SQL Query
```sql

```
#### 🖊 Result
#### 📜 Explanation
### Answer
---
### 5. Which item was the most popular for each customer?

#### 💻 SQL Query
```sql

```
#### 🖊 Result
#### 📜 Explanation
### Answer
---
### 6. Which item was purchased first by the customer after they became a member?

#### 💻 SQL Query
```sql

```
#### 🖊 Result
#### 📜 Explanation
### Answer
---
### 7. Which item was purchased just before the customer became a member?

#### 💻 SQL Query
```sql

```
#### 🖊 Result
#### 📜 Explanation
### Answer
---
### 8. What is the total items and amount spent for each member before they became a member?

#### 💻 SQL Query
```sql

```
#### 🖊 Result
#### 📜 Explanation
### Answer
---
### 9. If each $1 spent equates to 10 points and sushi has a 2x points multiplier - how many points would each customer have?

#### 💻 SQL Query
```sql

```
#### 🖊 Result
#### 📜 Explanation
### Answer
---
### 10. In the first week after a customer joins the program (including their join date) they earn 2x points on all items, not just sushi - how many points do customers A and B have at the end of January?

#### 💻 SQL Query
```sql

```
#### 🖊 Result
#### 📜 Explanation
### Answer
