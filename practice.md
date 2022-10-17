[1](#1)  
[2](#2)  
[3](#3)  
[4](#4)  
[5](#5)  
[6](#6)  
[7](#7)  
[8](#8)  
[9](#9)  
[10](#10)  
[11](#11)  
[12](#12)  
[13](#13)  
[14](#14)  
[15](#15)  
[16](#16)  
[17](#17)  
[18](#18)  
[19](#19)  
[20](#20)


## 1

https://sql-ex.ru/learn_exercises.php?LN=1  
Find the model number, speed and hard drive capacity for all the PCs with prices below $500.

```sql
SELECT model, speed, hd
FROM PC
WHERE price < 500
```

## 2

https://sql-ex.ru/learn_exercises.php?LN=2  
List all printer makers.

```sql
SELECT maker  
FROM  product 
WHERE type = 'printer' 
GROUP by maker
```

## 3

https://sql-ex.ru/learn_exercises.php?LN=3  
Find the model number, RAM and screen size of the laptops with prices over $1000.

```sql
SELECT model, ram, screen
FROM Laptop
WHERE price > 1000
```

## 4

https://sql-ex.ru/learn_exercises.php?LN=4  
Find all records from the Printer table containing data about color printers.

```sql
SELECT *
FROM Printer
WHERE color = 'y'
```

## 5

https://sql-ex.ru/learn_exercises.php?LN=5  
Find the model number, speed and hard drive capacity of PCs cheaper than $600 having a 12x or a 24x CD drive.

```sql
SELECT model, speed, hd FROM PC 
WHERE (cd = '12x' OR cd ='24x') AND price < 600
```

## 6

https://sql-ex.ru/learn_exercises.php?LN=6  
For each maker producing laptops with a hard drive capacity of 10 Gb or higher, find the speed of such laptops.

```sql
SELECT DISTINCT Product.maker, Laptop.speed FROM Product
INNER JOIN Laptop 
ON Product.model=Laptop.model 
WHERE Laptop.hd >= 10
```

## 7

https://sql-ex.ru/learn_exercises.php?LN=7  
Get the models and prices for all commercially available products (of any type) produced by maker B.

```sql
SELECT Product.model, Laptop.price 
FROM Product 
INNER JOIN Laptop 
ON Laptop.model=Product.model 
WHERE maker = 'B' 
UNION 
SELECT Product.model, PC.price 
FROM Product 
INNER JOIN PC 
ON PC.model=Product.model 
WHERE maker = 'B' 
UNION 
SELECT Product.model, Printer.price 
FROM Product 
INNER JOIN Printer 
ON Printer.model=Product.model 
WHERE maker = 'B'
```

## 8 

https://sql-ex.ru/learn_exercises.php?LN=8  
Find the makers producing PCs but not laptops.  

```sql
SELECT maker FROM Product 
WHERE type = 'PC' 
EXCEPT 
SELECT maker FROM Product 
WHERE type = 'Laptop'
```

## 9

https://sql-ex.ru/learn_exercises.php?LN=9  
Find the makers of PCs with a processor speed of 450 MHz or more.

```sql
SELECT DISTINCT maker FROM Product 
INNER JOIN PC 
ON Product.model = PC.model 
WHERE speed >= 450
```

## 10

https://sql-ex.ru/learn_exercises.php?LN=10  
Find the printer models having the highest price.

```sql
SELECT model, price FROM Printer 
WHERE price = (SELECT MAX(Printer.price) FROM Printer)
```

## 11

https://sql-ex.ru/learn_exercises.php?LN=11  
Find out the average speed of PCs

```sql
SELECT AVG(speed) 
FROM PC
```

## 12

https://sql-ex.ru/learn_exercises.php?LN=12  
Find out the average speed of the laptops priced over $1000.

```sql
SELECT AVG(speed) FROM Laptop 
WHERE price > 1000
```

## 13

https://sql-ex.ru/learn_exercises.php?LN=13  
Find out the average speed of the PCs produced by maker A.

```sql
SELECT AVG(speed) FROM Product 
INNER JOIN PC 
ON Product.model = PC.model 
WHERE maker = 'A'
```

## 14

https://sql-ex.ru/learn_exercises.php?LN=14  
For the ships in the Ships table that have at least 10 guns, get the class, name, and country.

```sql
SELECT Ships.class, Ships.name, Classes.country FROM Ships 
INNER JOIN Classes 
ON Ships.class = Classes.class 
WHERE numGuns >= 10
```

## 15

https://sql-ex.ru/learn_exercises.php?LN=15  
Get hard drive capacities that are identical for two or more PCs.

```sql
SELECT hd from (SELECT hd, COUNT(*) as count FROM pc 
GROUP BY hd) as a 
WHERE count >= 2
```

## 16

https://sql-ex.ru/learn_exercises.php?LN=16  
Get pairs of PC models with identical speeds and the same RAM capacity. Each resulting pair should be displayed only once, i.e. (i, j) but not (j, i).

```sql
SELECT DISTINCT B.model AS model, A.model AS model, A.speed, A.ram 
FROM PC AS A, PC B 
WHERE A.speed = B.speed AND A.ram = B.ram and A.model < B.model
```

## 17

https://sql-ex.ru/learn_exercises.php?LN=17  
Get the laptop models that have a speed smaller than the speed of any PC. 

```sql
SELECT DISTINCT type,laptop.model,speed FROM laptop INNER JOIN product on laptop.model= product.model  
WHERE speed < (select MIN(speed) FROM pc)
```

## 18

https://sql-ex.ru/learn_exercises.php?LN=18  
Find the makers of the cheapest color printers.

```sql
SELECT DISTINCT maker,price  FROM printer inner JOIN product ON printer.model= product.model  
WHERE price = (SELECT min(price)FROM printer WHERE color = 'y' ) and color = 'y'
```

## 19

https://sql-ex.ru/learn_exercises.php?LN=19  
For each maker having models in the Laptop table, find out the average screen size of the laptops he produces. 

```sql
SELECT maker ,avg(screen)as Avg_screen
FROM laptop INNER JOIN product on laptop.model =  product.model GROUP by maker
```

## 20

https://sql-ex.ru/learn_exercises.php?LN=20  
Find the makers producing at least three distinct models of PCs.

```sql
SELECT maker , count(model) as Count_Model FROM product WHERE type = 'pc' GROUP by maker 
HAVING count(model) >= 3
```












