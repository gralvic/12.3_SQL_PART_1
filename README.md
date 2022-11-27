# Домашнее задание к занятию 12.3 "Реляционные базы данных: SQL. Часть 1" - Алексей Григорьев

### Задание 1.

Получите уникальные названия районов из таблицы с адресами, которые начинаются на “K” и заканчиваются на “a”, и не содержат пробелов.


```sql
SELECT DISTINCT district
FROM address
WHERE district LIKE "K%a" AND district NOT LIKE "% %";
```

![image](https://github.com/gralvic/12.3_SQL_PART_1/blob/main/SQL_PART_1_TASK_01.png)

### Задание 2.

Получите из таблицы платежей за прокат фильмов информацию по платежам, которые выполнялись в промежуток с 15 июня 2005 года по 18 июня 2005 года **включительно**, 
и стоимость которых превышает 10.00.

```sql
SELECT payment_id, payment_date, amount
FROM payment
WHERE payment_date BETWEEN '2005-06-15' AND '2005-06-19' AND amount > 10.00
ORDER BY payment_date ASC;
```

![image](https://github.com/gralvic/12.3_SQL_PART_1/blob/main/SQL_PART_1_TASK_02.png)

### Задание 3.

Получите последние 5 аренд фильмов.

```sql
SELECT rental_id, payment_id, payment_date
FROM payment
ORDER BY payment_date DESC
LIMIT 5;
```

![image](https://github.com/gralvic/12.3_SQL_PART_1/blob/main/SQL_PART_1_TASK_03.png)

### Задание 4.

Одним запросом получите активных покупателей, имена которых Kelly или Willie. 

Сформируйте вывод в результат таким образом:
- все буквы в фамилии и имени из верхнего регистра переведите в нижний регистр,
- замените буквы 'll' в именах на 'pp'

```sql
SELECT LOWER (last_name) AS last_name, LOWER (first_name) AS first_name, REPLACE (LOWER (first_name), 'll', 'pp') AS replaced_first_name
FROM customer
WHERE first_name = 'Kelly' OR first_name = 'Willie' AND active = 1;
```

![image](https://github.com/gralvic/12.3_SQL_PART_1/blob/main/SQL_PART_1_TASK_04.png)

## Дополнительные задания (со звездочкой*)

### Задание 5*.

Выведите Email каждого покупателя, разделив значение Email на 2 отдельных колонки: в первой колонке должно быть значение, указанное до @, во второй значение, указанное после @.

```sql
SELECT 	email, 
	SUBSTRING_INDEX(email, '@', 1) AS username,
	SUBSTRING_INDEX(email, '@', -1) AS domain_name
FROM customer;
```

![image](https://github.com/gralvic/12.3_SQL_PART_1/blob/main/SQL_PART_1_TASK_05.png)

### Задание 6.*

Доработайте запрос из предыдущего задания, скорректируйте значения в новых колонках: первая буква должна быть заглавной, остальные строчными.

```sql
SELECT 	a.email,
	CONCAT(UPPER(LEFT(SUBSTRING_INDEX(a.email, '@', 1), 1)), LOWER(SUBSTRING(SUBSTRING_INDEX(a.email, '@', 1), 2))) AS username,	
	CONCAT(UPPER(LEFT(SUBSTRING_INDEX(a.email, '@', -1), 1)), LOWER(SUBSTRING(SUBSTRING_INDEX(a.email, '@', -1), 2))) AS domain_name
FROM customer a;
```

![image](https://github.com/gralvic/12.3_SQL_PART_1/blob/main/SQL_PART_1_TASK_06.png)
