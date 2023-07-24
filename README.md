# SQL-Queries
## SQL-запросы, выполненные в ходе прохождения курса "Функциональное тестирование ПО" в QA Life  

Для выполнения SQL-запросов использовались MySQL Server и MySQL Workbench.  
Требования и описание заданий доступны по ссылке:  [Требования и задания](https://drive.google.com/drive/u/3/folders/1Lt7CY69nR5awNs_9q0XJOHRti4vJj3Qa)

## SQL Academy   
В данном репозитории представлены мои решения задач из SQL Academy.  
SQL Academy по ссылке: [SQL Academy](https://sql-academy.org/ru/trainer)
- Задание 1 Вывести имена всех людей, которые есть в базе данных авиакомпаний
```
SELECT name
FROM passenger
```
- Задание 2 Вывести названия всеx авиакомпаний
```
SELECT name
FROM Company
```
- Задание 3 Вывести все рейсы, совершенные из Москвы
```
SELECT * FROM Trip
WHERE town_from = "Moscow"
```
- Задание 4 Вывести имена людей, которые заканчиваются на "man"
```
SELECT name
FROM Passenger
WHERE name LIKE '%man'
 ```
- Задание 5 Вывести количество рейсов, совершенных на TU-134
```
SELECT COUNT(plane) as count
FROM trip
WHERE plane = 'TU-134'
```
- Задание 6 Какие компании совершали перелеты на Boeing
```
SELECT DISTINCT name
FROM Company
INNER JOIN Trip on Company.id = Trip.Company
WHERE plane = 'Boeing'
```
- Задание 7 Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
```
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```
- Задание 8 В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
```
SELECT town_to,
TIMEDIFF(time_in, time_out) as flight_time
FROM Trip
WHERE town_from = 'Paris'
```
- Задание 9 Какие компании организуют перелеты из Владивостока (Vladivostok)?
```
SELECT name
FROM Company
INNER JOIN Trip on Trip.company = Company.id
WHERE town_to = 'Vladivostok
```
- Задание 10 Вывести вылеты, совершенные с 10 ч. по 14 ч. 1 января 1900 г.
```
SELECT * FROM Trip
WHERE time_out BETWEEN '1900.01.01 10:00:00' AND '1900.01.01 14:00:00'
```
- Задание 11 Выведите пассажиров с самым длинным ФИО. Пробелы, дефисы и точки считаются частью имени.
```
SELECT name
FROM passenger
ORDER BY LENGTH(name) DESC
LIMIT 1
```
- Задание 12 Вывести id и количество пассажиров для всех прошедших полётов
```
SELECT trip,
COUNT(trip) as count
FROM Pass_in_trip
GROUP BY trip
```
- Задание 13 Вывести имена людей, у которых есть полный тёзка среди пассажиров
```
SELECT name
FROM Passenger
GROUP BY name
HAVING COUNT(name) > 1
```
- Задание 14 В какие города летал Bruce Willis
```
SELECT town_to
FROM Trip,
Pass_in_trip,
Passenger
WHERE Trip.id = Pass_in_trip.trip
AND passenger = passenger.id
AND name = 'Bruce Willis'
```
- Задание 15 Выведите дату и время прилёта пассажира Стив Мартин (Steve Martin) в Лондон (London)
```
SELECT time_in
FROM Pass_in_trip
INNER JOIN Trip on Pass_in_trip.trip = Trip.id
JOIN Passenger on Pass_in_trip.passenger = Passenger.id
WHERE name = 'Steve Martin'
AND town_to = 'London'
```
- Задание 16 Вывести отсортированный по количеству перелетов (по убыванию) и имени (по возрастанию) список пассажиров, совершивших хотя бы 1 полет.
```
SELECT name, COUNT(*) as count
FROM Passenger
INNER JOIN Pass_in_trip ON Passenger.id = Pass_in_trip.passenger
GROUP BY passenger
HAVING COUNT(*) > 0
ORDER by COUNT(COUNT) DESC, name
```
- Задание 17 В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
```
SELECT town_to,
TIMEDIFF(time_in, time_out) as flight_time
FROM Trip
WHERE town_from = 'Paris'
```
- Задание 18 Узнать, кто старше всех в семьe
```
SELECT member_name
FROM FamilyMembers
WHERE DATE(birthday)
LIMIT 1
```
- Задание 19 Определить, кто из членов семьи покупал картошку (potato)
```
SELECT DISTINCT FamilyMembers.status
FROM FamilyMembers
INNER JOIN Payments ON FamilyMembers.member_id = Payments.family_member
JOIN Goods ON Payments.good = Goods.good_id
WHERE Goods.good_name = 'potato'
```
- Задание 20 Сколько и кто из семьи потратил на развлечения (entertainment). Вывести статус в семье, имя, сумму
```
SELECT FamilyMembers.status, FamilyMembers.member_name, SUM(Payments.unit_price * amount) AS costs
FROM FamilyMembers
JOIN Payments ON FamilyMembers.member_id = Payments.family_member
JOIN Goods ON Payments.good = Goods.good_id
JOIN GoodTypes ON Goods.type = GoodTypes.good_type_id
WHERE GoodTypes.good_type_name = 'entertainment'
GROUP BY FamilyMembers.status, FamilyMembers.member_name;
```
- Задание 21 Определить товары, которые покупали более 1 раза
```
SELECT Goods.good_name
FROM Goods
JOIN Payments ON Payments.good = Goods.good_id
GROUP BY Goods.good_name
HAVING COUNT(*) > 1;
```
- Задание 22 Найти имена всех матерей (mother)
```
SELECT member_name
FROM FamilyMembers
WHERE status = 'mother'
```
- Задание 23 Найдите самый дорогой деликатес (delicacies) и выведите его цену
```
SELECT Goods.good_name, unit_price
FROM Goods
JOIN Payments ON Goods.good_id = Payments.good
JOIN GoodTypes ON GoodTypes.good_type_id = Goods.type
WHERE Payments.unit_price =(
   SELECT MAX(Payments.unit_price)
   FROM Goods
			JOIN Payments ON Goods.good_id = Payments.good
			JOIN GoodTypes ON GoodTypes.good_type_id = Goods.type
		WHERE GoodTypes.good_type_name = 'delicacies'	)
```
- Задание 24 Определить кто и сколько потратил в июне 2005
```
SELECT FamilyMembers.member_name, SUM(Payments.amount * Payments.unit_price) AS costs
FROM FamilyMembers
JOIN Payments ON FamilyMembers.member_id = Payments.family_member
WHERE Payments.date >= '2005-06-01'
AND Payments.date < '2005-07-01'
GROUP BY FamilyMembers.member_name;
```
- Задание 25 Определить, какие товары не покупались в 2005 году
```
SELECT Goods.good_name
FROM Goods
LEFT JOIN Payments ON Payments.good = Goods.good_id
AND YEAR(Payments.date) = 2005
WHERE Payments.good IS NULL;
```
- Задание 26 Определить группы товаров, которые не приобретались в 2005 году
```
SELECT good_type_name
FROM GoodTypes
WHERE good_type_id not IN (
  SELECT good_type_id
  FROM GoodTypes
  JOIN Goods ON Goods.type = GoodTypes.good_type_id
  JOIN Payments ON Payments.good = Goods.good_id
  WHERE YEAR(date) = 2005 )
```





