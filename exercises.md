# SQL-exercises
## 1 задание

```sql
SELECT model, speed, hd
FROM pc
WHERE price < 500
```

## 2 задание

```sql
SELECT maker
FROM product
WHERE product.type = 'printer'
GROUP BY maker
```

## 3 задание

```sql
SELECT model, ram, screen
FROM laptop
WHERE price > 1000
```

## 4 задание

```sql
SELECT *
FROM printer
WHERE color = 'y'
```

## 5 задание

```sql
SELECT model, speed, hd
FROM pc
WHERE (cd = '24x' OR cd = '12x') AND price < 600
```

## 6 задание

```sql
SELECT maker, speed
FROM product INNER JOIN laptop ON product.model = laptop.model
WHERE hd >= 10
```

## 7 задание

```sql
SELECT DISTINCT product.model, PC.price
FROM product INNER JOIN pc ON pc.model = product.model
WHERE product.maker = 'B'
UNION
SELECT DISTINCT product.model, laptop.price
FROM product INNER JOIN laptop ON laptop.model = product.model
WHERE product.maker = 'B'
UNION
SELECT DISTINCT product.model, printer.price
FROM product INNER JOIN printer ON printer.model = product.model
WHERE product.maker = 'B'
```

## 8 задание

```sql
SELECT maker
FROM product
WHERE type = 'pc' AND maker NOT IN 
(SELECT maker FROM product WHERE type = 'laptop')
GROUP BY maker
```

## 9 задание

```sql
SELECT maker
FROM pc INNER JOIN Product ON pc.model = product.model
WHERE speed >= 450
```

## 10 задание

```sql
SELECT model, price
FROM printer
WHERE price >= (SELECT max(price) FROM printer)
```

## 11 задание

```sql
SELECT avg(speed)
FROM pc
```

## 12 задание

```sql
SELECT avg(speed)
FROM laptop
WHERE price > 1000;
```

## 13 задание

```sql
SELECT avg(speed)
FROM product INNER JOIN pc ON pc.model = product.model
WHERE maker = 'A'
GROUP BY maker
```

## 14 задание

```sql
SELECT classes.class, name, country
FROM ships INNER JOIN classes ON ships.class = classes.class
WHERE classes.numGuns >= 10
```

## 15 задание

```sql
SELECT hd
FROM pc
GROUP BY hd
HAVING count(model) > 1
```

## 16 задание

```sql
SELECT DISTINCT A.model, B.model, A.speed, A.ram
FROM pc AS A, pc AS B
WHERE A.model > B.model AND A.speed = B.speed AND A.ram = B.ram
```

## 17 задание

```sql
SELECT DISTINCT type, laptop.model, speed
FROM laptop INNER JOIN product ON product.model = laptop.model
WHERE speed < (SELECT speed FROM PC)
```

## 18 задание

```sql
SELECT DISTINCT maker, price
FROM printer INNER JOIN product ON product.model = printer.model
WHERE price = (SELECT min(price) FROM printer WHERE color = 'y') AND color = 'y'
```

## 19 задание

```sql
SELECT maker, avg(screen)
FROM laptop INNER JOIN product ON product.model = laptop.model
GROUP BY maker  
```

## 20 задание

```sql
SELECT maker, count(model)
FROM product
WHERE type = 'pc'
GROUP BY maker
HAVING count(model) >= 3
```

## 21 задание

```sql
SELECT maker, max(price)
FROM product INNER JOIN pc ON pc.model = product.model
WHERE type = 'pc'
GROUP BY maker
```

## 22 задание

```sql
SELECT speed, avg(price)
FROM pc
WHERE speed > 600
GROUP BY speed
```

## 23 задание

```sql
SELECT DISTINCT maker
FROM product INNER JOIN pc ON pc.model = product.model
WHERE pc.speed >= 750
INTERSECT
SELECT DISTINCT maker
FROM product INNER JOIN laptop ON laptop.model = product.model
WHERE laptop.speed >= 750
```

## 24 задание

```sql
SELECT model 
FROM (SELECT distinct model, price 
FROM laptop 
WHERE laptop.price = (SELECT MAX(price) FROM laptop)  
UNION 
SELECT distinct model, price 
FROM pc WHERE pc.price = (SELECT MAX(price) FROM pc)  
UNION 
SELECT distinct model, price 
FROM printer 
WHERE printer.price = (SELECT MAX(price) FROM printer) ) as t 

WHERE t.price = (SELECT max(price) FROM (SELECT DISTINCT price FROM laptop WHERE laptop.price = (SELECT max(price) FROM laptop)  
UNION 
SELECT DICTINCT price FROM pc WHERE pc.price = (SELECT max(price) FROM pc)  
UNION 
SELECT DISTINCT price FROM printer WHERE printer.price = (SELECT max(price) FROM printer)  
) as t1 )    
```

## 25 задание

```sql
SELECT DISTINCT product.maker FROM product WHERE product.type = 'printer'  
INTERSECT 
SELECT DISTINCT product.maker FROM product INNER JOIN pc ON pc.model = product.model  
WHERE product.type = 'pc' AND pc.ram = (SELECT min(ram) FROM pc)  
AND pc.speed = (SELECT max(speed) FROM (SELECT distinct speed FROM pc 
WHERE pc.ram = (SELECT min(ram) FROM pc)) as t) 
```

## 26 задание

```sql
SELECT DISTINCT product.maker FROM product WHERE product.type = 'printer'  
INTERSECT 
SELECT DISTINCT product.maker FROM product INNER JOIN pc ON pc.model = product.model  
WHERE product.type = 'pc' AND pc.ram = (SELECT min(ram) FROM pc)  
AND pc.speed = (SELECT max(speed) FROM (SELECT distinct speed FROM pc 
WHERE pc.ram = (SELECT min(ram) FROM pc)) as t) 
```

## 27 задание

```sql
SELECT maker, avg(hd)
FROM product INNER JOIN pc ON pc.model = product.model
WHERE maker IN (SELECT maker FROM product WHERE type = 'printer')
GROUP BY maker
```

## 28 задание

```sql
SELECT avg(hd)  
FROM product INNER JOIN pc on product.model = pc.model   
WHERE maker IN (SELECT maker FROM product WHERE type = 'printer') 
```

## 29 задание

```sql
SELECT t.point, t.date, sum(t.inc), sum(t.out) 
FROM (SELECT point, date, inc, NULL AS out FROM Income_o  
UNION
SELECT point, date, NULL AS inc, Outcome_o.out FROM Outcome_o) AS t 
GROUP BY t.point, t.date  
```

## 30 задание

```sql
SELECT point, date, sum(sum_out), sum(sum_inc)
FROM (
SELECT point, date, sum(inc) AS sum_inc, NULL AS sum_out
FROM Income
GROUP BY point, date
UNION
SELECT point, date, NULL AS sum_inc, SUM(out) AS sum_out
FROM Outcome
GROUP BY point, date) AS t
GROUP BY point, date
ORDER BY point
```

## 31 задание

```sql
SELECT class, country
FROM classes
WHERE bore >= 16
```

## 32 задание

```sql
SELECT country, cast(avg((power(classes.bore, 3) / 2)) AS numeric(6, 2))
FROM classes
GROUP BY classes.country
```

## 33 задание

```sql
SELECT ship
FROM Outcomes
WHERE battle = 'North Atlantic' AND result = 'sunk'
GROUP BY ship
```

## 34 задание

```sql
SELECT name
FROM classes, ships
WHERE launched >= 1922 AND displacement > 35000 AND type = 'bb' AND  ships.class = classes.class  
```

## 35 задание

```sql
SELECT model, type
FROM product
WHERE model NOT LIKE '%[^0-9]%' OR model NOT LIKE '%[^A-Z]%'
```

## 36 задание

```sql
SELECT name
FROM ships
WHERE class = name
UNION
SELECT ship AS name
FROM classes, Outcomes
WHERE classes.class = Outcomes.ship
```

## 37 задание

```sql
SELECT class
FROM (
SELECT name, class
FROM ships
UNION
SELECT class AS name, class
FROM classes, Outcomes
WHERE classes.class = Outcomes.ship) A
GROUP BY class
HAVING count(A.name) = 1
```

## 38 задание

```sql
SELECT DISTINCT country  
FROM classes  
WHERE type = 'bb'   
INTERSECT  
SELECT DISTINCT country  
FROM classes  
WHERE type = 'bc'  
```

## 39 задание

```sql
WITH temp AS (SELECT * FROM Outcomes JOIN battles ON Outcomes.battle = battles.name)
SELECT DISTINCT a.ship
FROM temp AS a
WHERE upper(a.ship) IN (SELECT upper(b.ship) FROM temp AS b WHERE b.date < a.date AND b.result = 'damaged')
```

## 40  задание

```sql
SELECT maker, max(type) AS type
FROM product
GROUP BY maker
HAVING count(model) > 1 AND max(type) = min(type)
```

## 41 задание

```sql
WITH temp AS (
SELECT product.maker, temp2.price
FROM product JOIN ( 
SELECT model, price
FROM pc
UNION
SELECT model, price
FROM laptop
UNION
SELECT model, price
FROM printer) AS temp2 ON temp2.model = product.model)
SELECT DISTINCT maker, IIF(count(*) != count(price), NULL, max(price))
FROM temp
GROUP BY maker
```

## 42 задание

```sql
SELECT ship, battle
FROM Outcomes
WHERE result = 'sunk'
```

## 43 задание

```sql
SELECT name
FROM battles
WHERE year(battles.date) NOT IN (SELECT ships.launched FROM ships WHERE ships.launched IS NOT NULL)
```

## 44 задание

```sql
SELECT name 
FROM ships 
WHERE name LIKE 'R%'   

UNION   
SELECT name
FROM battles 
WHERE name 
LIKE 'R%'   

UNION   
SELECT ship 
FROM outcomes 
WHERE ship like 'R%'  
```

## 45 задание

```sql
SELECT name 
FROM ships 
WHERE name 
LIKE '% % %'  
UNION   
SELECT ship 
FROM outcomes 
WHERE ship 
LIKE '% % %'   
```

## 46 задание

```sql
SELECT DISTINCT ship, displacement, numguns
FROM classes
LEFT JOIN ships ON classes.class = ships.class
RIGHT JOIN Outcomes ON classes.class = Outcomes.ship
OR ships.name = Outcomes.ship
WHERE battle = 'Guadalcanal'
```

## 47 задание

```sql
WITH out AS (
SELECT *
FROM Outcomes
JOIN (
SELECT ships.name, classes.class, classes.country
FROM ships FULL JOIN classes ON ships.class = classes.class) u ON outcomes.ship = u.s_class
UNION
SELECT * 
FROM Outcomes JOIN (
SELECT ships.name, classes.class, classes.country
FROM ships FULL JOIN classes ON ships.class = classes.class) u ON outcomes.ship = u.s_name)
SELECT fin.country
FROM (
SELECT DISTINCT t.country, count(t.name) AS num_ships
FROM (
SELECT DISTINCT c.country, s.name
FROM classes c INNER JOIN Ships s ON s.class = c.class
UNION
SELECT DISTINCT c.country, o.ship
FROM
classes c INNER JOIN Outcomes o ON o.ship = c.class) t
GROUP BY t.country
INTERSECT
SELECT out.s_country, count(out.ship)
FROM out
WHERE out.result = 'sunk'
GROUP BY out.s_country 
    ) fin
```

## 48 задание

```sql
SELECT DISTINCT classes.class
FROM classes LEFT JOIN Ships ON Classes.class = Ships.class RIGHT JOIN Outcomes ON classes.class = Outcomes.ship OR ships.name = Outcomes.ship
WHERE result = 'sunk' AND classes.class IS NOT NULL
```

## 49 задание

```sql
SELECT name 
FROM ships 
WHERE class IN (SELECT class FROM classes WHERE bore = 16)   
UNION
SELECT ship
FROM outcomes 
WHERE ship IN (SELECT class FROM classes WHERE bore = 16)    
```

## 50 задание

```sql
SELECT DISTINCT battle 
FROM Classes INNER JOIN ships  ON ships.class = classes.class INNER JOIN Outcomes ON classes.class = Outcomes.ship or ships.name = Outcomes.ship   
WHERE classes.class = 'Kongo'  
```

## 51 задание

```sql
SELECT name 
FROM (
SELECT name AS name, displacement, numguns  
FROM ships INNER JOIN classes on ships.class = classes.class 
UNION 
SELECT ship AS name, displacement, numguns
FROM outcomes INNER JOIN classes ON outcomes.ship = classes.class) 
AS d1 INNER JOIN (SELECT displacement, max(numGuns) AS numguns FROM (SELECT displacement, numguns FROM ships INNER JOIN classes ON ships.class = classes.class  
UNION
SELECT displacement, numguns  
FROM outcomes INNER JOIN classes ON outcomes.ship = classes.class) AS f 
GROUP BY displacement) AS d2 ON d1.displacement = d2.displacement AND d1.numguns = d2.numguns 
```



## 52 задание

```sql
SELECT DISTINCT name 
FROM ships INNER JOIN classes ON ships.class = cl.class 
WHERE (numGuns >= 9 OR numguns IS NULL) AND (bore < 19 OR bore IS NULL) AND (displacement <= 65000 OR displacement IS NULL) AND type = 'bb' AND country = 'japan' 

```


## 53 задание

```sql
SELECT cast(avg(classes.numGuns * 1.0) AS numeric(6, 2))
FROM classes
WHERE type = 'bb'
```

## 54

```sql
SELECT cast(avg(numguns*1.0) AS NUMERIC (4,2)) 
FROM (
SELECT ship, type, numguns   
FROM Outcomes LEFT JOIN Classes ON ship = class  
UNION  
SELECT name, type, numguns 
FROM ships as s INNER JOIN  classes as c ON c.class = s.class) AS t 
WHERE type = 'bb' 
```

## 55

```sql
SELECT classes.class, min(ships.launched)
FROM classes LEFT JOIN ships ON classes.class = ships.class
GROUP BY classes.class
```

## 56

```sql
SELECT c.class, count(s.ship)
FROM classes c LEFT JOIN (
SELECT o.ship, sh.class
FROM outcomes o LEFT JOIN ships sh ON sh.name = o.ship
WHERE o.result = 'sunk') AS s ON s.class = c.class OR s.ship = c.class
GROUP BY c.class
```

## 57

```sql
SELECT class AS cls, count(class) AS sunked
FROM (
SELECT c.class, o.ship
FROM classes AS c JOIN outcomes AS o ON c.class = O.ship
WHERE o.result = 'sunk'
UNION
SELECT s.class, o.ship
FROM outcomes AS o JOIN ships AS s ON s.name = o.ship
WHERE o.result = 'sunk') AS t
WHERE class IN (
SELECT DISTINCT x.class 
FROM (
SELECT c.class, o.ship
FROM classes AS c JOIN outcomes AS o ON c.class = o.ship
UNION
SELECT c.class, s.name
FROM classes AS c JOIN ships AS s ON c.class = s.class) AS x
GROUP BY x.class
HAVING count(x.class) >= 3)
GROUP BY class
```

## 58

```sql
SELECT main_maker, main_type, convert(numeric(6,2), ((sub_num * 100.00) / (total_num * 100.00) * 100.00))  
FROM (SELECT count(p5.model) total_num, p5.maker main_maker 
FROM product p5 GROUP BY p5.maker) p6 JOIN (SELECT p3.maker sub_maker, p3.type main_type, count(p4.model) sub_num 
FROM (SELECT p1.maker maker, p2.type type FROM product p1 cross JOIN product p2 GROUP BY p1.maker, p2.type) p3 LEFT JOIN product p4 ON p3.maker = p4.maker AND p3.type = p4.type GROUP BY p3.maker, p3.type) p7 ON p7.sub_maker = p6.main_maker 
```

## 59

```sql
SELECT a.point,
CASE WHEN o IS NULL THEN i
ELSE i - o
END remain
FROM (
SELECT point, sum(inc) AS i
FROM Income_o
GROUP BY point) AS a LEFT JOIN (
SELECT point, sum(out) AS o
FROM Outcome_o
GROUP BY point) AS b ON A.point = B.point
```

## 60

```sql
SELECT c1, c2 - (
CASE WHEN o2 IS NULL THEN 0
ELSE o2
END)
FROM (
SELECT point c1, sum(inc) c2
FROM Income_o
WHERE date < '2001-04-15'
GROUP BY point) AS t1 LEFT JOIN (
SELECT point o1, sum(out) o2
FROM Outcome_o
WHERE date < '2001-04-15'
GROUP BY point) AS t2 ON c1 = o1
```

## 61

```sql
SELECT (
SELECT sum(inc) 
FROM Income_o) - (
SELECT sum(out) 
FROM Outcome_o) AS remain  
```

## 62

```sql
SELECT (
SELECT sum(inc)
FROM Income_o
WHERE date < '2001-04-15') - (
SELECT sum(out)
FROM Outcome_o
WHERE date < '2001-04-15') AS remain
```

## 63

```sql
SELECT name
FROM passenger
WHERE ID_psg IN (
SELECT ID_psg
FROM Pass_in_trip
GROUP BY place, ID_psg
HAVING count(*) > 1)
```

## 64

```sql
SELECT income.point, income.date, 'inc' as operation, sum(income.inc) 
FROM income LEFT JOIN outcome ON income.point = outcome.point AND income.date = outcome.date 
WHERE outcome.date IS NULL  
GROUP BY income.point, income.date 
UNION
SELECT outcome.point, outcome.date, 'out' AS operation, sum(outcome.out) 
FROM income RIGHT JOIN outcome ON income.point = outcome.point AND income.date = outcome.date 
WHERE income.date IS NULL
GROUP BY outcome.point, outcome.date 


```

## 65

```sql
WITH pmq AS (
SELECT maker, type, CASE 
WHEN type = 'pc' THEN 0
WHEN type = 'laptop' THEN 1
ELSE 2
END AS s, CASE
WHEN type = 'laptop'
AND maker IN (
SELECT maker
FROM product
WHERE type = 'pc') THEN ''
WHEN type = 'printer'
            AND maker IN (
                SELECT
                    maker
                FROM
                    [Product]
                WHERE
                    [type] = 'PC'
                    OR [type] = 'Laptop'
            ) THEN ''
            ELSE [maker]
        END AS m
    FROM
        [dbo].[Product]
    GROUP BY
        [maker],
        [type]
)
SELECT
    row_number() over(
        ORDER BY
            [maker],
            [s]
    ) num,
    [m],
    [type]
FROM     [pmq]
ORDER BY [maker],
    [s];
```

## 66

```sql
SELECT date, max(c)
FROM (
SELECT date, count(*) AS c
FROM trip, (
SELECT trip_no, date
FROM Pass_in_trip
WHERE date >= '2003-04-01' AND date <= '2003-04-07'
GROUP BY trip_no, date) AS t1
WHERE Trip.trip_no = t1.trip_no AND town_from = 'Rostov'
GROUP BY date
UNION ALL
SELECT '2003-04-01', 0
UNION ALL
SELECT '2003-04-02', 0
UNION ALL
SELECT '2003-04-03', 0
UNION ALL
SELECT '2003-04-04', 0
UNION ALL
SELECT '2003-04-05', 0
UNION ALL
SELECT '2003-04-06', 0
UNION ALL
SELECT '2003-04-07', 0 ) AS t2
GROUP BY date
```

## 67

```sql
SELECT count(tf) AS ctf 
FROM ( 
SELECT town_from AS tf, town_to, count(plane) AS cp 
FROM Trip 
GROUP BY town_from, town_to 
HAVING count(plane) >= all (
SELECT count(plane)  
FROM Trip 
GROUP BY town_from, town_to) ) as tablo 
```

## 68

```sql
SELECT count(*)
FROM (
SELECT sum(c) cc, c1, c2
FROM (
SELECT count(*) c, town_from c1, town_to c2
FROM trip
WHERE town_from >= town_to
GROUP BY town_from, town_to
UNION ALL
SELECT count(*) c, town_to, town_from
FROM trip
WHERE town_to > town_from
GROUP BY town_from, town_to) AS t
GROUP BY c1, c2
ORDER BY cc DESC) AS tt
```

## 69

```sql
WITH t AS (
SELECT point, date, inc, 0 AS out
FROM Income
UNION ALL
SELECT point, date, 0 AS inc, out
FROM Outcome)
SELECT t.point, format(t.date, 'dd/MM/yyyy') AS day, (
SELECT sum(i.inc)
FROM t i
WHERE i.date <= t.date AND i.point = t.point) - (
SELECT sum(i.out) 
FROM t i
WHERE i.date <= t.date AND i.point = t.point) AS rem
FROM t
GROUP BY t.point, t.date
```

## 70

```sql
SELECT DISTINCT o.battle
FROM outcomes o LEFT JOIN ships s ON s.name = o.ship LEFT JOIN classes c ON o.ship = c.class OR s.class = c.class
WHERE c.country IS NOT NULL
GROUP BY c.country, o.battle
HAVING count(o.ship) >= 3
```

## 71

```sql
SELECT p.maker
FROM product p LEFT JOIN pc ON pc.model = p.model
WHERE p.type = 'pc'
GROUP BY p.maker
HAVING count(p.model) = count(pc.model)
```

## 72

```sql
SELECT name, c3
FROM passenger JOIN (
SELECT c1, max(c3) c3
FROM (
SELECT pass_in_trip.ID_psg c1, Trip.ID_comp c2, count(*) c3
FROM pass_in_trip JOIN trip ON trip.trip_no = pass_in_trip.trip_no
GROUP BY pass_in_trip.ID_psg, Trip.ID_comp) AS t
GROUP BY c1
HAVING count(*) = 1) AS tt ON ID_psg = c1
ORDER BY c3 DESC
```

## 73

```sql
SELECT DISTINCT c.country, b.name
FROM battles b, classes c
EXCEPT
SELECT c.country, o.battle
FROM outcomes o LEFT JOIN ships s ON s.name = o.ship LEFT JOIN classes c ON o.ship = c.class OR s.class = c.class
WHERE c.country IS NOT NULL
GROUP BY c.country, o.battle
```

## 74

```sql
SELECT c.country, c.class
FROM classes c
WHERE upper(c.country) = 'RUSSIA' AND EXISTS (
SELECT c.country, c.class
FROM classes c
WHERE upper(c.country) = 'RUSSIA')
UNION ALL
SELECT c.country, c.class
FROM classes c
WHERE NOT EXISTS (
SELECT c.country, c.class
FROM classes c
WHERE upper(c.country) = 'RUSSIA')
```

## 75

```sql
WITH new AS (
    SELECT
        COALESCE(xPC.maker, xPr.maker, xLa.maker) AS maker,
        xPC.price AS xPC_price,
        xPr.price AS xPr_price,
        xLa.price AS xLa_price
    FROM
        (
            SELECT
                DISTINCT maker
            FROM
                Product
        ) AS TMP
        LEFT JOIN (
            SELECT
                Product.maker,
                temp2.price
            FROM
                Product
                JOIN PC AS temp2 ON temp2.model = product.model
        ) AS xPC ON xPC.maker = TMP.maker
        LEFT JOIN (
            SELECT
                Product.maker,
                temp2.price
            FROM
                Product
                JOIN Printer AS temp2 ON temp2.model = product.model
        ) AS xPr ON xPr.maker = TMP.maker
        LEFT JOIN (
            SELECT
                Product.maker,
                temp2.price
            FROM
                Product
                JOIN Laptop AS temp2 ON temp2.model = product.model
        ) AS xLA ON xLA.maker = TMP.maker
)
SELECT
    maker,
    max(xLa_price),
    max(xPC_price),
    max(xPr_price)
FROM
    new
GROUP BY
    maker
HAVING
    COALESCE(
        max(xLa_price),
        max(xPC_price),
        max(xPr_price),
        0
    ) != 0;
```

## 76

```sql
WITH cte AS (
SELECT ROW_NUMBER() OVER (
            PARTITION BY ps.ID_psg,
            pit.place
            ORDER BY
                pit.date
        ) AS rowNumber,
        DATEDIFF (
            MINUTE,
            time_out,
            DATEADD(DAY, IIF(time_in < time_out, 1, 0), time_in)
        ) AS timeFlight,
        ps.Id_psg,
        ps.name
    FROM
        Pass_in_trip pit
        LEFT JOIN trip tr ON pit.trip_no = tr.trip_no
        LEFT JOIN Passenger ps ON ps.ID_psg = pit.ID_psg -- Все рейсы
)
SELECT
    MAX(cte.name),
    SUM(timeFlight)
FROM
    cte
GROUP BY
    cte.ID_psg
HAVING max(rowNumber) = 1
```

## 77

```sql
SELECT TOP 1 WITH TIES *
FROM (
SELECT count(DISTINCT(pt.trip_no)) qty, pt.date
FROM Trip t, Pass_in_trip pt
WHERE t.trip_no = pt.trip_no AND t.town_from = 'Rostov'
GROUP BY pt.date) t1
ORDER BY t1.qty DESC
```

## 78

```sql
SELECT name, replace(convert(char(12), dateadd(m, datediff(m, 0, date), 0), 102), '.', '-') AS first_day, replace(convert(CHAR(12), dateadd(s, -1, dateadd(m, datediff(m, 0, date) + 1, 0)), 102), '.', '-') AS last_day
FROM battles
```

## 79

```sql
WITH a AS(
SELECT id_psg, sum(datediff(mi, time_out,
                CASE
                    WHEN time_out > time_in THEN dateadd(DAY, 1, time_in)
                    ELSE time_in
                END)) mnts
FROM trip t INNER JOIN pass_in_trip pit ON t.trip_no = pit.trip_no
GROUP BY id_psg)
SELECT top(1) WITH ties name, mnts
FROM a INNER JOIN passenger p ON a.id_psg = p.id_psg
ORDER BY mnts DESC
```

## 80
```sql
SELECT DISTINCT maker
FROM product
WHERE maker NOT IN (
SELECT maker
FROM product 
WHERE type = 'pc' AND model NOT IN (
SELECT model
FROM pc))
```


## 81

```sql
SELECT o.*
FROM outcome o INNER JOIN (
SELECT TOP 1 WITH TIES year(date) AS y, month(date) AS m, sum(out) AS sumo
FROM Outcome
GROUP BY year(date), month(date)
ORDER BY sumo DESC) R ON year(o.date) = r.y AND month(o.date) = r.m
```

## 82
```sql
WITH cte(code, price, number) AS (
SELECT pc.code, pc.price, number = row_number() over (
ORDER BY pc.code)
FROM pc)
SELECT cte.code, avg(c.price)
FROM cte JOIN cte c ON (c.number - cte.number) < 6 AND (c.number - cte.number) >= 0
GROUP BY cte.number, cte.code
HAVING count(cte.number) = 6
```

## 83
```sql
SELECT s.name
FROM classes c INNER JOIN ships s ON c.class = s.class
WHERE
    CASE
        WHEN c.numGuns = 8 THEN 1
        ELSE 0
    END + CASE
        WHEN c.bore = 15 THEN 1
        ELSE 0
    END + CASE
        WHEN c.displacement = 32000 THEN 1
        ELSE 0
    END + CASE
        WHEN c.type = 'bb' THEN 1
        ELSE 0
    END + CASE
        WHEN s.launched = 1915 THEN 1
        ELSE 0
    END + CASE
        WHEN s.class = 'Kongo' THEN 1
        ELSE 0
    END + CASE
        WHEN c.country = 'USA' THEN 1
        ELSE 0
    END > = 4
```

## 84
```sql
SELECT c.name, A.N_1_10, A.N_11_21, A.N_21_30
FROM (
SELECT t.ID_comp, SUM(
                CASE
                    WHEN DAY(P.date) < 11 THEN 1
                    ELSE 0
                END) AS N_1_10,
                  SUM(
                CASE
                    WHEN (day(P.date) > 10 AND day(P.date) < 21) THEN 1
                    ELSE 0
                END) AS N_11_21,
                  SUM(
                CASE
                    WHEN DAY(P.date) > 20 THEN 1
                    ELSE 0
                END) AS N_21_30
FROM trip AS t JOIN Pass_in_trip AS p ON t.trip_no = p.trip_no AND convert(char(6), P.date, 112) = '200304'
GROUP BY T.ID_comp) AS a JOIN Company AS c ON A.ID_comp = C.ID_comp
```

## 85

```sql
SELECT maker
FROM product
GROUP BY maker
HAVING count(DISTINCT type) = 1 AND (min(type) = 'printer' OR (min(type) = 'pc' AND count(model) >= 3))
```

## 86
```sql
SELECT maker, CASE count(DISTINCT type) 
        WHEN 2 THEN min(type) + '/' + max(type)
        WHEN 1 THEN max(type)
        WHEN 3 THEN 'laptop/pc/printer'
    END
FROM product
GROUP BY maker
```

## 87
```sql
SELECT DISTINCT name, COUNT(town_to) Qty
FROM trip tr JOIN Pass_in_trip pit ON tr.trip_no = pit.trip_no JOIN Passenger psg ON pit.ID_psg = psg.ID_psg
WHERE town_to = 'Moscow' AND pit.ID_psg NOT IN(
SELECT DISTINCT ID_psg
FROM Trip tr JOIN Pass_in_trip pit ON tr.trip_no = pit.trip_no
WHERE date + time_out = (
SELECT min(date + time_out)
FROM trip tr1 JOIN Pass_in_trip pit1 ON tr1.trip_no = pit1.trip_no
WHERE pit.ID_psg = pit1.ID_psg) AND town_from = 'Moscow')
GROUP BY pit.ID_psg, name
HAVING count(town_to) > 1
```

## 88
```sql
SELECT (
SELECT name
FROM passenger
WHERE ID_psg = B.ID_psg) AS name, B.trip_Qty, (
SELECT name
FROM company
WHERE ID_comp = B.ID_comp) AS Company
FROM (
SELECT P.ID_psg, min(T.ID_comp) AS ID_comp, count(*) AS trip_Qty, max(count(*)) over() AS Max_Qty
FROM Pass_in_trip AS p JOIN Trip AS t ON P.trip_no = T.trip_no 
GROUP BY P.ID_psg
HAVING min(T.ID_comp) = max(T.ID_comp)  AS B
WHERE B.trip_Qty = B.Max_Qty
```

## 89
```sql
SELECT maker, count(DISTINCT model) Qty
FROM product
GROUP BY maker
HAVING count(DISTINCT model) >= ALL (
SELECT count(DISTINCT model)
FROM product
GROUP BY maker) OR count(DISTINCT model) <= ALL (
SELECT count(DISTINCT model)
FROM product
GROUP BY maker)
```

## 90

```sql
SELECT t1.maker, t1.model, t1.type
FROM (
SELECT row_number() over (
ORDER BY model) p1, row_number() over (
ORDER BY model DESC) p2, * 
FROM product) t1
WHERE p1 > 3 AND p2 > 3
```

## 91

```sql
SELECT CAST(1.0 * CASE
WHEN (
SELECT Sum(B_VOL)
FROM utB) IS NULL THEN 0 ELSE (
SELECT Sum(B_VOL)
FROM utB) END / (
SELECT count(*) FROM utQ) AS NUMERIC(6, 2))avg_paint
```

## 92

```sql
SELECT Q_NAME
FROM utQ
WHERE Q_ID IN (
SELECT DISTINCT B.B_Q_ID
FROM (
SELECT B_Q_ID
FROM utB
GROUP BY B_Q_ID
HAVING SUM(B_VOL) = 765) AS B
WHERE B.B_Q_ID NOT IN (
SELECT B_Q_ID
FROM utB
WHERE B_V_ID IN (
SELECT B_V_ID
FROM utB
GROUP BY B_V_ID
HAVING sum(B_VOL) < 255)))
```

## 93
```sql
SELECT c.name, sum(vr.vr)
FROM (
SELECT DISTINCT t.id_comp, pt.trip_no, pt.date, t.time_out, t.time_in, -pt.id_psg,
            CASE
                WHEN DATEDIFF(mi, t.time_out, t.time_in) > 0 THEN DATEDIFF(mi, t.time_out, t.time_in)
                WHEN DATEDIFF(mi, t.time_out, t.time_in) <= 0 THEN DATEDIFF(mi, t.time_out, t.time_in + 1)
            END vr
FROM pass_in_trip pt LEFT JOIN trip t ON pt.trip_no = t.trip_no) vr LEFT JOIN company c ON vr.id_comp = c.id_comp
GROUP BY c.name
```

## 94

```sql
SELECT dateadd(day, S.Num, D.date) AS Dt, (
SELECT count(DISTINCT P.trip_no)
FROM Pass_in_trip P JOIN Trip T ON P.trip_no = T.trip_no AND T.town_from = 'Rostov' AND P.date = DATEADD(DAY, S.Num, D.date)) AS Qty
FROM (
SELECT (3 * (x - 1) + y - 1) AS Num
FROM (
SELECT 1 AS x
UNION ALL
SELECT 2
UNION ALL
SELECT 3) AS N1 CROSS JOIN (
SELECT 1 AS y
UNION ALL
SELECT 2
UNION ALL
SELECT 3) AS N2
WHERE (3 * (x - 1) + y) < 8) AS S, (
SELECT min(A.date) AS date
FROM (
SELECT P.date, count(DISTINCT P.trip_no) AS Qty, max(count(DISTINCT P.trip_no)) over() AS M_Qty
FROM Pass_in_trip AS P JOIN Trip AS T ON P.trip_no = T.trip_no AND T.town_from = 'Rostov'
GROUP BY P.date) AS A
WHERE A.Qty = A.M_Qty) AS D
```


## 95

```sql
SELECT name, count(DISTINCT convert(char(24), date) + convert(CHAR(4), Trip.trip_no)), count(DISTINCT plane), count(DISTINCT ID_psg), count(*)
FROM company, Pass_in_trip, trip
WHERE Company.ID_comp = Trip.ID_comp AND Trip.trip_no = Pass_in_trip.trip_no
GROUP BY Company.ID_comp, name
```

## 96

```sql
WITH r AS (
SELECT v.v_name, v.v_id, count(
            CASE
                WHEN v_color = 'R' THEN 1
            END) over(PARTITION by v_id) cnt_r,
        count(
            CASE
                WHEN v_color = 'B' THEN 1
            END) over(PARTITION by b_q_id) cnt_b
FROM utV v JOIN utB b ON v.v_id = b.b_v_id)
SELECT v_name
FROM r
WHERE cnt_r > 1 AND cnt_b > 0
GROUP BY v_name
```

## 97
```sql
SELECT code, speed, ram, price, screen
FROM laptop
WHERE EXISTS (
SELECT 1 x
FROM (
SELECT v, rank() over(
ORDER BY v) rn
FROM ( 
SELECT cast(speed AS float) sp, cast(ram AS float) rm, cast(price AS float) pr, cast(screen AS float) sc) l unpivot(v FOR c IN (sp, rm, pr, sc)) u) l pivot(max(v) FOR rn IN ([1], [2], [3], [4])) p
WHERE [1] * 2 <= [2] AND [2] * 2 <= [3] AD [3] * 2 <= [4])
```
## 98

```sql
WITH CTE AS (
SELECT 1 n, cast (0 AS varchar(16)) bit_or, code, speed, ram
FROM pc
UNNION ALL
SELECT n * 2, cast (CONVERT(bit,(speed | ram) & n) AS varchar(1)) + cast(bit_or AS varchar(15)), code, speed, ram
FROM CTE 
WHERE n < 65536)
SELECT code, speed, ram
FROM CTE
WHERE n = 65536 AND CHARINDEX('1111', bit_or) > 0
```

## 99

```sql
SELECT point, "date" income_date, "date" + nvl(
min(
            CASE
                WHEN diff > cnt THEN cnt
                ELSE NULL
            END), max(cnt) + 1) incass_date
FROM (
SELECT i.point, i."date", (trunc(o."date") - trunc(i."date")) diff, count(1) over (
PARTITION by i.point, i."date"
ORDER BY o."date" ROWS BETWEEN unbounded preceding AND current ROW) -1 cnt
FROM income_o i JOIN (
SELECT point, "date", 1 disabled
FROM outcome_o
UNION 
SELECT point, trunc("date" + 7, 'DAY'), 1 disabled 
FROM income_o) o ON i.point = o.point
WHERE o."date" > = i."date")
GROUP BY point, "date"
```

## 100

```sql
SELECT
    DISTINCT A.date,
    A.R,
    B.point,
    B.inc,
    C.point,
    C.out
FROM
    (
        SELECT
            DISTINCT date,
            ROW_Number() OVER(
                PARTITION BY date
                ORDER BY
                    code ASC
            ) AS R
        FROM
            Income
        UNION
        SELECT
            DISTINCT date,
            ROW_Number() OVER(
                PARTITION BY date
                ORDER BY
                    code ASC
            )
        FROM
            Outcome
    ) A
    LEFT JOIN (
        SELECT
            date,
            point,
            inc,
            ROW_Number() OVER(
                PARTITION BY date
                ORDER BY
                    code ASC
            ) AS RI
        FROM
            Income
    ) B ON B.date = A.date
    AND B.RI = A.R
    LEFT JOIN (
        SELECT
            date,
            point,
            out,
            ROW_Number() OVER(
                PARTITION BY date
                ORDER BY
                    code ASC
            ) AS RO
        FROM
            Outcome
    ) C ON C.date = A.date
    AND C.RO = A.R;
```
