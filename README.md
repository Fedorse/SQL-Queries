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
- Задание 16 Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
```
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```
- Задание 17 В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
```
SELECT town_to,
TIMEDIFF(time_in, time_out) as flight_time
FROM Trip
WHERE town_from = 'Paris'
```
- Задание 18 Какие компании совершали перелеты на Boeing
```
SELECT DISTINCT name
FROM Company
INNER JOIN Trip on Company.id = Trip.Company
WHERE plane = 'Boeing'
```
- Задание 19 Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
```
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```
- Задание 20 В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
```
SELECT town_to,
TIMEDIFF(time_in, time_out) as flight_time
FROM Trip
WHERE town_from = 'Paris'
```
- Задание 21 Какие компании совершали перелеты на Boeing
```
SELECT DISTINCT name
FROM Company
INNER JOIN Trip on Company.id = Trip.Company
WHERE plane = 'Boeing'
```
- Задание 22 Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
```
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```
- Задание 23 В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
```
SELECT town_to,
TIMEDIFF(time_in, time_out) as flight_time
FROM Trip
WHERE town_from = 'Paris'
```
- Задание 24 Какие компании совершали перелеты на Boeing
```
SELECT DISTINCT name
FROM Company
INNER JOIN Trip on Company.id = Trip.Company
WHERE plane = 'Boeing'
```
- Задание 25 Вывести все названия самолётов, на которых можно улететь в Москву (Moscow)
```
SELECT DISTINCT plane
FROM Trip
WHERE town_to = 'Moscow'
```
- Задание 26 В какие города можно улететь из Парижа (Paris) и сколько времени это займёт?
```
SELECT town_to,
TIMEDIFF(time_in, time_out) as flight_time
FROM Trip
WHERE town_from = 'Paris'
```





