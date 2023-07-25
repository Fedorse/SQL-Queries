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
- Задание 27 Узнать, сколько потрачено на каждую из групп товаров в 2005 году. Вывести название группы и сумму
```
SELECT good_type_name, SUM(amount * unit_price) AS costs
FROM GoodTypes
JOIN Goods ON Goods.type = GoodTypes.good_type_id
JOIN Payments ON Payments.good = Goods.good_id
WHERE YEAR(date) = 2005
GROUP BY good_type_name
```
- Задание 28 Сколько рейсов совершили авиакомпании из Ростова (Rostov) в Москву (Moscow) ?
```
SELECT COUNT(company) as count
FROM Trip
WHERE town_from = 'Rostov' AND town_to = 'Moscow'
```
- Задание 29 Выведите имена пассажиров улетевших в Москву (Moscow) на самолете TU-134
```
SELECT DISTINCT name
FROM Passenger
JOIN Pass_in_trip on Passenger.id = Pass_in_trip.passenger
JOIN Trip on Pass_in_trip.trip = Trip.id
WHERE town_to = 'Moscow' AND plane = 'TU-134'
```
- Задание 30 Выведите нагруженность (число пассажиров) каждого рейса (trip). Результат вывести в отсортированном виде по убыванию нагруженности.
```
SELECT COUNT(passenger) AS count, trip
FROM Pass_in_trip
GROUP by trip
ORDER by count DESC
```
- Задание 31 Вывести всех членов семьи с фамилией Quincey.
```
SELECT * FROM FamilyMembers
WHERE member_name LIKE '%Quincey'
```
- Задание 32 Вывести средний возраст людей (в годах), хранящихся в базе данных. Результат округлите до целого в меньшую сторону.
```
SELECT FLOOR(avg(YEAR(CURRENT_DATE) - YEAR(birthday))) as age
FROM FamilyMembers
```
- Задание 33 Найдите среднюю стоимость икры. В базе данных хранятся данные о покупках красной (red caviar) и черной икры (black caviar).
```
SELECT AVG(unit_price) as cost
FROM Payments
WHERE good in (
	SELECT good_id
	FROM Goods
	WHERE good_name LIKE '%caviar')
```
- Задание 34 Сколько всего 10-ых классов
```
SELECT COUNT(*) as count
FROM Class
WHERE name = 10
```
- Задание 35 Сколько различных кабинетов школы использовались 2.09.2019 в образовательных целях ?
```
SELECT COUNT(*) as count
FROM Schedule
WHERE date = '2019-09-02'
```
- Задание 36 Выведите информацию об обучающихся живущих на улице Пушкина (ul. Pushkina)?
```
SELECT * FROM Student
WHERE address LIKE 'ul. Pushkin%'
```
- Задание 37 Сколько лет самому молодому обучающемуся ?
```
SELECT MIN(TIMESTAMPDIFF(YEAR, birthday, CURRENT_DATE)) as year
FROM Student
```
- Задание 38 Сколько Анн (Anna) учится в школе ?
```
SELECT COUNT(first_name) as count
FROM Student
WHERE first_name = 'Anna'
```
- Задание 39 Сколько обучающихся в 10 B классе ?
```
SELECT COUNT(student) as count
FROM Student_in_class
JOIN Class ON Student_in_class.class = Class.id
WHERE Class.name = '10 B'
```
- Задание 40 Выведите название предметов, которые преподает Ромашкин П.П. (Romashkin P.P.) ?
```
SELECT name as subjects
FROM Subject
JOIN Schedule ON Subject.id = Schedule.subject
JOIN Teacher ON Schedule.teacher = Teacher.id
WHERE Teacher.last_name = 'Romashkin'
AND Teacher.middle_name LIKE 'P%'
AND Teacher.first_name LIKE 'P%'
```
- Задание 41 Во сколько начинается 4-ый учебный предмет по расписанию ?
```
SELECT start_pair
FROM Timepair
WHERE id = 4
```
- Задание 42 Сколько времени обучающийся будет находиться в школе, учась со 2-го по 4-ый уч. предмет?
```
SELECT DISTINCT TIMEDIFF('11:50:00', '09:20:00') as time
FROM Timepair
```
- Задание 43 Выведите фамилии преподавателей, которые ведут физическую культуру (Physical Culture). Отcортируйте преподавателей по фамилии.
```
SELECT last_name
FROM Teacher
JOIN Schedule ON Schedule.teacher = Teacher.id
JOIN Subject ON Subject.id = Schedule.subject
WHERE Subject.name = 'Physical Culture'
ORDER by last_name asc
```
- Задание 44 Найдите максимальный возраст (колич. лет) среди обучающихся 10 классов ?
```
SELECT MAX(TIMESTAMPDIFF(YEAR, birthday, CURRENT_DATE)) as max_year
FROM Student
JOIN Student_in_class ON Student.id = Student_in_class.student
JOIN Class ON Student_in_class.class = Class.id
WHERE Class.name LIKE '10%'
```
- Задание 45 Какие кабинеты чаще всего использовались для проведения занятий? Выведите те, которые использовались максимальное количество раз.
```
SELECT Schedule.classroom
FROM Schedule
GROUP BY classroom
HAVING COUNT(*) =(
	SELECT MAX(count)
	FROM (SELECT COUNT(*) AS count
		FROM Schedule
		GROUP BY classroom) AS A)
```
- Задание 46 В каких классах введет занятия преподаватель "Krauze" ?
```
SELECT DISTINCT Class.name
FROM Class
JOIN Schedule ON Schedule.class = Class.id
JOIN Teacher ON Teacher.id = Schedule.teacher
WHERE last_name = 'Krauze'
```
- Задание 47 Сколько занятий провел Krauze 30 августа 2019 г.?
```
SELECT COUNT(teacher) as count
FROM Schedule
WHERE date = '2019-08-30' AND teacher = (
	SELECT id
	FROM Teacher
	WHERE last_name = 'Krauze'
	)
```
- Задание 48 Выведите заполненность классов в порядке убывания
```
SELECT name, COUNT(*) AS count
FROM Student_in_class
JOIN Class ON Class.id = class
GROUP BY Class.name
ORDER BY count DESC
```
- Задание 49 Какой процент обучающихся учится в 10 A классе ?
```
SELECT (
SELECT COUNT(*)
FROM Student_in_class
JOIN Class ON class = Class.id
WHERE Class.name = '10 A') / (
	SELECT COUNT(*)
	FROM Student_in_class ) * 100 AS percent
```
- Задание 50 Какой процент обучающихся родился в 2000 году? Результат округлить до целого в меньшую сторону.
```
SELECT FLOOR(
	(SELECT COUNT(*)
	FROM Student
	WHERE YEAR(birthday) = 2000) / (
		SELECT COUNT(*)FROM Student) * 100) AS percent
```
- Задание 51 Добавьте товар с именем "Cheese" и типом "food" в список товаров (Goods).
```
INSERT INTO Goods (SELECT COUNT(*) + 1,'Cheese',
	(SELECT good_type_id
	FROM GoodTypes
	WHERE good_type_name = 'food' limit 1
		)
		FROM Goods
		)
```
- Задание 52 Добавьте в список типов товаров (GoodTypes) новый тип "auto".
```
INSERT INTO GoodTypes (
	SELECT COUNT(*) + 1,'auto'
	FROM GoodTypes)
```
- Задание 53 Измените имя "Andie Quincey" на новое "Andie Anthony".
```
UPDATE FamilyMembers
SET member_name = 'Andie Anthony'
WHERE member_name = 'Andie Quincey';
```
- Задание 56 Удалить все перелеты, совершенные из Москвы (Moscow).
```
DELETE FROM Trip
WHERE town_from = 'Moscow'
```
- Задание 57 Перенести расписание всех занятий на 30 мин. вперед.
```
UPDATE Timepair
SET start_pair = DATE_ADD(start_pair, INTERVAL 30 MINUTE),
	end_pair = DATE_ADD(end_pair, INTERVAL 30 MINUTE);
```
- Задание 59 Вывести пользователей,указавших Белорусский номер телефона ? Телефонный код Белоруссии +375.
```
SELECT *
FROM Users
WHERE phone_number LIKE '+375%'
```
- Задание 60 Выведите идентификаторы преподавателей, которые хотя бы один раз за всё время преподавали в каждом из одиннадцатых классов.
```
SELECT teacher
FROM Schedule
JOIN Class on Schedule.class = Class.id
WHERE name like '11%'
GROUP by teacher
HAVING COUNT(DISTINCT name) = 2
```








