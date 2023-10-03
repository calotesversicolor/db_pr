Первичный ключ (primary key) — особенное поле в SQL-таблице, которое позволяет однозначно идентифицировать каждую запись в ней. Хранит в себе уникальные идентификаторы
Внешний ключ (foreign key) обеспечивает целостную связь между таблицами  и ссылается на первичный ключ другой таблицы 

## 12.09.2023

## 1

```sql
insert into person values (10, 'Zhenia', 18, 'male', 'Saint-Petersburg');
insert into person values (11, 'Olga', 35, 'female', 'Kemerovo');
insert into person values (12, 'Lisa', 19, 'female', 'Kazan');
insert into person values (13, 'Oleg', 29, 'male', 'Kemerovo');
insert into person values (14, 'Pavel', 38, 'male', 'Saint-Petersburg');
insert into person values (15, 'Viktor', 56, 'male', 'Kazan');
insert into person values (16, 'John', 23, 'male', 'Novosinirsk');
insert into person values (17, 'James', 47, 'male', 'Samara');
insert into person values (18, 'Frank', 39, 'male', 'Saint-Petersburg');
insert into person values (19, 'Diane', 15, 'female', 'Kemerovo');
insert into person values (20, 'Carol', 22, 'female', 'Samara');
```

```sql
insert into pizzeria values (7,'Pizzeria Stokey', 3.9);
insert into pizzeria values (8,'Voodoo Rays', 4.4);
insert into pizzeria values (9,'Zia Lucia', 5.0);
insert into pizzeria values (10,'Hai Cenato', 2.3);
insert into pizzeria values (11,'Princi', 4.0);
insert into pizzeria values (12,'Four Hundred Rabbits', 4.9);
insert into pizzeria values (13,'50 Kalo di Ciro Salvo', 3.7);
insert into pizzeria values (14,'Pizza Castle', 1.9);
insert into pizzeria values (15,'Quattro Pizza', 1.2);
insert into pizzeria values (16,'Ragazza', 3.2);
insert into pizzeria values (17,'Pizza Planet', 4.7);
```

```sql
insert into person_visits values (20, 17, 10, '2022-01-11');
insert into person_visits values (21, 17, 9, '2022-01-11');
insert into person_visits values (22, 12, 11, '2022-01-13');
insert into person_visits values (23, 11, 11, '2022-01-12');
insert into person_visits values (24, 17, 7, '2022-01-20');
insert into person_visits values (25, 15, 12, '2022-02-01');
insert into person_visits values (26, 12, 12, '2022-02-01');
insert into person_visits values (27, 17, 15, '2022-01-21');
insert into person_visits values (28, 9, 13, '2022-01-30');
insert into person_visits values (29, 8, 15, '2022-01-29');
insert into person_visits values (30, 7, 16, '2022-01-25');
```

```sql
insert into menu values (19,6,'cheese pizza', 700);
insert into menu values (20,6,'pepperoni pizza', 800);

insert into menu values (21,7,'cheese pizza', 700);
insert into menu values (23,7,'pepperoni pizza', 800);
insert into menu values (24,7,'sausage pizza', 950);

insert into menu values (25,8,'cheese pizza', 700);
insert into menu values (26,8,'mushroom pizza', 950);
insert into menu values (27,8,'sausage pizza', 950);

insert into menu values (28,9,'cheese pizza', 700);
insert into menu values (29,9,'supreme pizza', 1200);
```

```sql
insert into person_order values (21,10, 2, '2022-01-11');

insert into person_order values (22,11, 19, '2022-01-16');
insert into person_order values (23,11, 2, '2022-01-12');
insert into person_order values (24,11, 7, '2022-01-18');

insert into person_order values (25,12, 10, '2022-01-21');
insert into person_order values (26,12, 17, '2022-01-09');

insert into person_order values (27,13, 10, '2022-01-24');

insert into person_order values (28,14, 7, '2022-01-12');
insert into person_order values (29,14, 5, '2022-01-20');
insert into person_order values (30,14, 1, '2022-01-02');

insert into person_order values (31,15, 9, '2022-01-23');
```

insert into * values - отвечает за добавление в столбец нового значения

## 2 

```sql
SELECT name, age, address
FROM person
WHERE address = 'Kemerovo';
```

SELECT * FROM - частичная или полная выборка из таблицы
WHERE - задает условие для функции и выбора значений из таблицы

## 3

```sql
SELECT  name, age, address, gender
FROM person
WHERE address = 'Kazan' AND gender = 'female'
ORDER BY name ASC;
```
ORDER BY * ASC / DESC - сортировка значений по возрастанию / убыванию


## 4

```sql
SELECT name, rating
FROM pizzeria
WHERE rating >= 3.5 AND rating <= 5.0
ORDER BY rating DESC;
```
AND - логическое умножение. В данном случае задает промежуток между числами

```sql
SELECT name, rating
FROM pizzeria
WHERE rating BETWEEN 3.5 AND 5.0
ORDER BY rating DESC;
```
BETWEEN - задает промежуток между значениями с включением начала и конца промежутка  

## 5

```sql
SELECT DISTINCT ON (person_id) person_id, visit_date
FROM person_visits
WHERE visit_date >= '2022.01.11' AND visit_date <= '2022.01.31' OR person_id = 2
ORDER BY person_id DESC;
```
OR - логический оператор "или" 




## 13.09.2023 

## 1

```sql
SELECT menu.id AS object_id, pizza_name AS object_name FROM menu
UNION
SELECT person.id, name FROM person
ORDER BY object_id ASC, object_name ASC;
```
UNION - объединение двух таблиц с тем условием, что количество столбцов будет одинаковым. Повторяющиеся строки при таком объединении опускаются

## 2

```sql
SELECT menu.id AS object_id, pizza_name AS object_name FROM menu
UNION All
SELECT person.id, name FROM person
ORDER BY object_name DESC;
```
UNION ALL - объединение двух таблиц с тем условием, что количество столбцов будет одинаковым. Повторяющиеся строки при таком объединении остаются


## 3

```sql
SELECT person_id, visit_date AS action_date FROM person_visits
INTERSECT
SELECT person_id, order_date FROM person_order ORDER BY action_date ASC, person_id DESC;
```
INTERSECT - пересечение значений из двух таблиц



## 19.09.2023 

## Exercise 01 - Did you hear about Cartesian Product?

```sql
SELECT * FROM pizzeria
CROSS JOIN person;
```
CROSS JOIN - объединение, которое отвечает за перекрестное пересечение двух таблиц

## Exercise 02 - Lets see on “Hidden” Insights

```sql
SELECT order_date AS action_date, name FROM person_order, person
WHERE order_date IN (SELECT visit_date FROM person_visits) AND person_order.person_id = person.id
ORDER BY order_date ASC, name DESC;
```
IN позволяет определить, совпадает ли значение объекта со значением в списке 
AND person_order.person_id = person.id - приравнивает значения ID, создает значение NULL для пересечения таблиц и значений


## Exercise 03 - Just make a JOIN

```sql
SELECT order_date, (name || ' (age:' || age || ')') AS person_information 
FROM person_order
JOIN person ON person.id=person_order.person_id
ORDER BY person_information ASC, order_date ASC;
```
(name || ' (age:' || age || ')') AS person_information  - объединяет несколько значений из таблицы в один столбец и называет ее
JOIN person ON person.id=person_order.person_id - оператор JOIN * ON объединяет одинаковые значения в двух таблицах по совпадающему параметру person id 
 

## Exercise 04 - Migrate JOIN to NATURAL JOIN

```sql
SELECT order_date, (name || ' (age:' || age || ')') AS person_information 
FROM person_order
NATURAL JOIN person
ORDER BY person_information ASC, order_date ASC;
```
NATURAL JOIN - работает как JOIN * ON и ссылается на все столбцы 

## Exercise 05 - IN versus EXISTS

```sql
select name, id from pizzeria 
WHERE id NOT IN (SELECT pizzeria_id FROM person_visits);
```
WHERE NOT IN - заданное проверяет условие. 
Может работать без вложенного запроса. 

```sql
SELECT name, id FROM pizzeria 
WHERE NOT EXISTS (SELECT pizzeria_id FROM person_visits WHERE pizzeria.id = pizzeria_id);
```
WHERE NOT EXISTS - функция, которая проверяет булево значение TRUE если запрос не содержит строк или FALSE, если содержит.  
Проверяет строки во вложенном подзапросе. 

## Exercise 06 - Global JOIN

```sql
SELECT person.name AS person_name, menu.pizza_name, pizzeria.name AS pizzeria_name FROM person_order
JOIN person ON person.id = person_order.person_id
LEFT JOIN menu ON menu.id = person_order.menu_id
LEFT JOIN pizzeria ON pizzeria.id = menu.pizzeria_id
ORDER BY person_name, pizza_name, pizzeria_name ASC;
```

LEFT JOIN * ON создает левое внешнее соединение. Объединяет все записи первой таблицы, включая пересечение со второй




## 20.09.2023 

## Exercise 00

```sql
SELECT name, rating
FROM  pizzeria
LEFT  JOIN person_visits ON  pizzeria.id = person_visits.pizzeria_id
WHERE person_visits.pizzeria_id IS NULL
ORDER BY rating DESC;
```
WHERE * IS NULL - булево значение, которое проверяет значение NULL на TRUE or FALSE. Удаляет все значение, которые не равны значению NULL

## Exercise 01 - Find data gaps

```sql
SELECT missing_days::date FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') as missing_days
FULL JOIN
(SELECT * FROM person_visits
WHERE person_id = 1 OR  person_id = 2) AS tab ON missing_days = tab.visit_date
WHERE person_id IS NULL;
```

SELECT missing_days::date FROM generate_series('2022-01-01', '2022-01-10', interval '1 day') as missing_days - генерирует временную таблицу, которая создает диапазон в выбранном промежутке
FULL JOIN - полное объединение двух таблиц, которое включает INNER, LEFT и RIGHT присоединения



## KR 26.09.2023

##  Вывести все записи из таблицы "Студенты"

```sql
select * from students;
```


## Вывести имена и фамилии всех студентов старше 21 года

```sql
select firstname, lastname
from students
where age > 21;
```


##  Вывести список всех курсов

```sql
select coursename from courses;
```


##  Вывести имена и фамилии студентов, которые учатся на курсе "Математика"

```sql
select firstname, lastname from students
join studentcourses on studentcourses.studentid = students.studentid
where courseid = (select courseid from courses where coursename = 'Математика');
```

## Вывести имена и фамилии студентов, возраст которых составляет 20 лет, и которые учатся на курсе "История"

```sql
select firstname, lastname from students
join studentcourses on studentcourses.studentid = students.studentid
where courseid = (select courseid from courses where coursename = 'История') and age = 20;
```


##  Вывести количество студентов на каждом курсе

```sql
select coursename, (select count(studentid) from studentcourses where c.courseid = studentcourses.courseid) from courses c;
```

##  Вывести средний возраст студентов

```sql
select avg(age) as avg_age from students;
```
avg(age) - определяет среднее значение. В данном случае средний возраст студентов


##  Вывести имена и фамилии студентов, которые не учатся ни на одном из курсов

```sql
select firstname, lastname, studentid from students
where studentid not in (select studentid from studentcourses);
```

##  Вывести список курсов и количество студентов на каждом курсе, даже если на курсе нет студентов

```sql
select coursename, (select count(studentid) from studentcourses where c.courseid = studentcourses.courseid) from courses c;
```

##  Вывести имена и фамилии студентов, которые не старше 22 лет и учатся на курсе "Биология"

```sql
select firstname, lastname from students
join studentcourses on studentcourses.studentid = students.studentid
where courseid = (select courseid from courses where coursename = 'Биология') and age >= 22;
```

##  Вывести имена и фамилии студентов, возраст которых наибольший среди всех студентов

```sql
select firstname, lastname from students
where age = (select max(age) from students);
```
max(age) - определяет самое большое значение. В данном слуае наибольший возраст студентов

##  Вывести средний возраст студентов на курсе "Биология"

```sql
SELECT avg(age) as avg_age from students
join studentcourses on studentcourses.studentid = students.studentid
where courseid = (select courseid from courses where coursename = 'Биология');
```

##  Вывести имена и фамилии студентов, которые учатся на курсах, но не на курсе "Информатика"

```sql
select firstname, lastname from students
join studentcourses on studentcourses.studentid = students.studentid
where not courseid = (select courseid from courses where coursename = 'Информатика');
```
