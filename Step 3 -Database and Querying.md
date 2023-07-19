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

### 2. Find the number of copies sold for each game and order them from most to least number of copies sold.
```sql
SELECT games.name AS game_name, COUNT(*) AS '# of Copies Sold'
FROM transactions
INNER JOIN games
ON transactions.product_id = games.product_id
GROUP BY games.name
ORDER BY popularity DESC;
```
105 rows will be returned, but I will show the top 5 and bottom 5 games.

top 5 games sold:
| game_name | # of Copies Sold
|-----------|-----------------
|Metal Gear Solid HD Collection	| 26
|The Legend of Zelda: A Link to the Past |	18
|Super Mario 64	| 17
|Sonic & Knuckles	| 16
|Pokemon Ruby	| 14

bottom 5 games sold:
| game_name | # of Copies Sold
|-----------|-----------------
|Super Bomberman|	2
|Super Smash Bros.|	2
|GoldenEye 007|	2
|Super Mario Bros. 3|	1
|Final Fantasy X	|1

### 3. Find the total number of transactions for each payment type (cash, credit, debit, mobile) and put them in order from most to least used payment types.
```sql
SELECT payment_method,COUNT(payment_method) AS '# of Transactions' FROM transactions
GROUP BY payment_method
ORDER BY COUNT(payment_method) DESC;
```

|payment_method|# of transactions
|--------------|-----------------
|mobile payment|	408
|debit	|372
|credit	|369
|cash	|351

### 4. Rank the top selling video game genres in the store from highest to lowest units sold.
```sql
SELECT games.genre, COUNT(games.genre) AS '# units sold' FROM transactions
INNER JOIN games
ON transactions.product_id = games.product_id
GROUP BY genre
ORDER BY COUNT(games.genre) DESC;
```

Top 5 Genres:
 genre | # units sold
-------|-------------
|Platformer	|168
|Role-playing game (RPG)	|148
|Action-Adventure|	88
|Stealth action|	50
|Survival horror|	37

Bottom 5 Genres:
genre | # units sold
------|-------------
Run and gun|	6
Simulation|	6
First-person shooter|	6
Maze|	4
Fighting/Party|	2

### 5. In Question 5, we see that Sierra Acevedo is the top customer of Nostalgia Cave. Find a list of games that they have purchased from the store. What games do they seem to purchase the most?
```sql
SELECT customers.full_name, games.name FROM transactions
INNER JOIN customers ON transactions.customer_id = customers.customer_id
INNER JOIN games ON transactions.product_id = games.product_id
HAVING customers.full_name = 'Sierra Acevedo';
```
full_name |	name
----------|------
Sierra Acevedo|	Star Wars: Knights of the Old Republic
Sierra Acevedo|	Mega Man X4
Sierra Acevedo|	Pokemon Yellow
Sierra Acevedo|	Pokemon FireRed
Sierra Acevedo|	Mega Man 2
Sierra Acevedo|	Final Fight
Sierra Acevedo|	Pokemon Red
Sierra Acevedo|	Pokemon Ruby

Based on this query, Sierra's favorite games are Pokemon and Mega Man.

### 6. Find the highest selling console brand.
```sql
SELECT consoles.brand, COUNT(consoles.brand) AS '# units sold' FROM transactions
INNER JOIN consoles ON transactions.product_id = consoles.product_id
GROUP BY consoles.brand
ORDER BY COUNT(consoles.brand) DESC
LIMIT 1;
```

brand | # units sold
------|-------------
Nintendo | 97

### 7. Suppose there is a 25% discount on all accessories that are $80 or more. Create a new column with the discounted prices.
```sql
SELECT name, price, price*.75 AS 'discounted price' FROM accessories
WHERE price >= 80;
```

name | price | discounted_price
-----|-------|-----------------
Xbox Elite Wireless Controller Series 2 (Black)	|180|	135
Xbox 360 Wireless Speed Wheel|	80|	60
Xbox 360 Wireless Racing Wheel	|100|	75
Xbox 360 Kinect Sensor	|80|	60
Sega Saturn Arcade Racer Joystick|	80|	60

### 8. Count the number of distinct customers that came to the store each month.
```sql
SELECT DATE_FORMAT(date, '%m') AS 'month', COUNT(DISTINCT customer_id) AS '# of customers'
FROM transactions
GROUP BY DATE_FORMAT(date, '%m');
```

month | # of customers
------|---------------
01	|213
02	|207
03	|207
04	|219
05	|227
06 |212

### 9. Suppose that there was an event throughout the month of June where people who purchased a video game from the store would be entered into a raffle on July 1st for a PS5. Query a list of all distinct customers who purchased a game in June to add them into the raffle.
```sql
SELECT DISTINCT customers.full_name, transactions.date, products.category FROM transactions
LEFT JOIN customers ON transactions.customer_id = customers.customer_id
LEFT JOIN products ON transactions.product_id = products.product_id
WHERE category = 'Game' AND (date BETWEEN '2023-06-01' AND '2023-06-30');
```
full_name | date | category
----------|------|---------
Shaine Olson	|2023-06-17	|Game
Lavinia Powell|	2023-06-14	|Game
Vivien Roman	|2023-06-12	|Game
India Roberts	|2023-06-05	|Game
Naomi Compton	|2023-06-24	|Game

### 10. Suppose a customer is looking for any Playstation 2 games. Query a catalog of Playstation 2 games that are in stock.
```sql
SELECT name, console, genre FROM games
WHERE console = 'Playstation 2';
```

name | console | genre |price
-----|---------|-------|-----
Metal Gear Solid 3: Snake Eater	|PlayStation 2|	Stealth action|	30
Final Fantasy X	|PlayStation 2	|Role-playing game (RPG)	|35
Metal Gear Solid 2: Sons of Liberty	|PlayStation 2|	Stealth action	|30
Kingdom Hearts	|PlayStation 2	|Action role-playing game (ARPG)	|40
Silent Hill 3	|PlayStation 2|	Survival horror|	30
Silent Hill 2	|PlayStation 2|	Survival horror	|30
Final Fantasy X-2	|PlayStation 2|	Role-playing game (RPG)|	30
Silent Hill 2: Director's Cut	|PlayStation 2	|Survival horror	|35
Silent Hill 2	|PlayStation 2	|Survival horror	|35
