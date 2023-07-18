# Step 3 - Importing Tables into MySQL Database
## Products Table
```sql
SELECT * FROM products;
```
Shows all 250 products and their categories
![image](https://github.com/Datarianna/Video-Game-Store-Database-and-Analysis/assets/138058039/a7074e65-9687-4665-8adb-7b661077c6cf)

## Games Table
```sql
SELECT * FROM games;
```
![image](https://github.com/Datarianna/Video-Game-Store-Database-and-Analysis/assets/138058039/11d60ec3-5cf8-4d54-9cbe-1b735f9eb33a)

## Consoles Table
```sql
SELECT * FROM consoles;
```
![image](https://github.com/Datarianna/Video-Game-Store-Database-and-Analysis/assets/138058039/bf9905e0-e47b-416d-81af-400a08002ca5)

## Accessories Table
```sql
SELECT * FROM accessories;
```
![image](https://github.com/Datarianna/Video-Game-Store-Database-and-Analysis/assets/138058039/45a95c27-5084-46b2-bacf-dea80ef996cf)

# Customers Table
```sql
SELECT * FROM customers;
```
![image](https://github.com/Datarianna/Video-Game-Store-Database-and-Analysis/assets/138058039/ba035640-818f-418e-ad05-603fbfe928fa)

# Transactions Table
```sql
SELECT * FROM transactions;
```
![image](https://github.com/Datarianna/Video-Game-Store-Database-and-Analysis/assets/138058039/bd314012-5300-4240-a889-c32d0618887b)

# Querying Questions
### 1. Suppose the owner wants to give discounts to customers who have purchase 5 or more items. Select all customers who have purchased 5 or more items since the store opened and show the number of items they bought.
```sql
SELECT transactions.customer_id, COUNT(transactions.trans_id) AS '# of Items Purchased', customers.full_name
FROM transactions
LEFT JOIN customers ON transactions.customer_id = customers.customer_id
GROUP BY transactions.customer_id, customers.full_name
HAVING COUNT(transactions.trans_id) >= 5
ORDER BY COUNT(transactions.trans_id) DESC;
```

|customer_id|# of Items Purchased|full_name|
| --- | - | ---------------- |
| 255 | 9 | Sierra Acevedo   |
| 544 | 7 | Acton Adkins     |
| 422 | 7 | Tara Thompson    |
| 108 | 7 | Jack Hodges      |
| 396 | 6 | Kermit Cooper    |
| 572 | 6 | Reese Campbell   |
| 531 | 6 | Yeo Wyatt        |
| 766 | 6 | Rylee Mcintyre   |
| 652 | 5 | Sarah Washington |
| 674 | 5 | Raphael Branch   |
| 523 | 5 | TaShya Norton    |
| 161 | 5 | Clark Pope       |
| 852 | 5 | Walker Wilkins   |
| 504 | 5 | Elijah Gutierrez |
| 555 | 5 | Jason Roy        |
| 98  | 5 | Medge Dodson     |
| 855 | 5 | Maisie Lyons     |
| 619 | 5 | Laith Clemons    |
| 377 | 5 | Nigel Kinney     |
| 767 | 5 | Naomi Maxwell    |
| 408 | 5 | Iola Weeks       |
| 330 | 5 | Octavia Burke    |