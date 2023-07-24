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


