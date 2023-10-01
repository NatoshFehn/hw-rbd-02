# Домашнее задание к занятию «SQL. Часть 2» - Наталья Мартынова (Пономарева)

### Задание 1

```sql
SELECT
	staff.first_name,
	staff.last_name,
	city.city,
	customers.cnt
FROM 
	sakila.store AS store
RIGHT JOIN (
	SELECT
		store_id,
		count(*) as cnt
	from
		sakila.customer
	group by
		store_id
	having
 		count(*) > 300) as customers on
 	customers.store_id = store.store_id
JOIN sakila.staff AS staff ON
 	store.manager_staff_id = staff.staff_id
JOIN sakila.address AS addr ON
 	store.address_id = addr.address_id
JOIN sakila.city city ON
 	addr.city_id = city.city_id
```
![Снимок1](https://github.com/NatoshFehn/hw-rbd-02/blob/main/Снимок1.png)  

### Задание 2

```sql
select
	count(1)
from
	sakila.film f
where
	f.length > (
	select
		AVG(f.length)
	from
		sakila.film f )
```  
![Снимок2](https://github.com/NatoshFehn/hw-rbd-02/blob/main/Снимок2.png)  


### Задание 3

Группировать просто по MONTH() не получится, т.к. при выборке за несколько лет получим искаженные данные. Поэтому:
```sql
select
	date_format(p.payment_date,'%Y-%m') month, count(*) payment_cnt
from
	sakila.payment p 
group by date_format(p.payment_date,'%Y-%m')
order by count(*) desc
LIMIT 1
```  
![Снимок3](https://github.com/NatoshFehn/hw-rbd-02/blob/main/Снимок3.png)  
