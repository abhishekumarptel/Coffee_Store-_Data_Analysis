# Coffee_Store-_Data_Analysis_Insights
---CREARTING 3 TABLES---

create table cust_name
(ID	int primary key,
 First_Name varchar(50),
 Last_Name varchar(50),
 Gender varchar(10),
 Phone_Number bigint
);


create table order_time
(ID int primary key,
 PRODUCT_ID int,
 CUSTOMER_ID int,
 ORDER_TIME varchar(20)
);

create table product_name
(ID int primary key,
 Name varchar(30),
 Price varchar(30),
 Coffee_Origin varchar(30)
);

---INSERT THE VALUES IN 3 TABLES---

copy cust_name from 'D:\coffee_store_project1\Customer_name1.csv' delimiter ',' csv header

copy order_time from 'D:\coffee_store_project1\order_coffee - Copy - Copy.csv' delimiter ',' csv header

copy product_name from 'D:\coffee_store_project1\product_namee - Copy.csv' delimiter ',' csv header
select * from cust_name
select * from order_time
select * from product_name

--join tables--
select * from cust_name as c
inner join order_time as o
on c.id=o.id
inner join product_name as p
on o.id=p.id


------insights-----
---1.select product_name,coffee_origin from table product_name for which product have more demand----

select  product_name.name,count(product_name.name) as product_count,product_name.coffee_origin from product_name
group by product_name.name,coffee_origin
order by product_count desc;

---2.select gender from table cust_name and count the total male, female--- 

select cust_name.gender,count(cust_name.gender)as count_gender from cust_name 
where gender='M' OR gender='F'
group by cust_name.gender

----3.select first_name,phone_number from table cust_name and also need  product_name from product table as coffee_name between '2/1/2023' and '2/19/2023'----

select c.first_name,c.phone_number,p.name as coffee_name from cust_name as c
inner join order_time as o
on c.id=o.id
left join product_name as p
on o.id=p.id
where o.order_time  between '2/1/2023' and '2/19/2023'

---4.select fisrt_name and gender from table cust_name where name start with a word---
select first_name,gender from cust_name as c
where c.first_name ilike 'a%' 

----5.select name,coffee_origin from table product_name where name is indonesia or brazil---
select p.name ,p.coffee_origin from product_name as p
where p.coffee_origin='Indonesia' or p.coffee_origin='Brazil'

---6. select name from product name table and product_id from table order_time---
select p.name,o.product_id from order_time as o
inner join product_name as p
on o.id=p.id

---7.select last_name from table cust_name where last_name is 'sharma'----
select c.last_name from cust_name as c
where c.last_name ilike '%sharma%'


---8.select name, price from table product_name where price is greter than 3---
select p.name,p.price from product_name as p
where cast(p.price as decimal) > 3;

--9.HOW MANY MALE CUSTOMERS DON’T HAVE A PHONE NUMBER ENTERED IN THE CUSTOMERS TABLE?---

select * from cus_name
where gender ='M'  AND phone_number ISnull

---10.FROM THE PRODUCTS TABLE, SELECT THE NAME AND PRICE OF ALL PRODUCTS WITH A COFFEE ORIGIN EQUAL TO COLUMBIA OR INDONESIA. SORT THE RESULTS BY NAME A-Z-----

select name , price from product_coffee
where coffee_origin='Colombia' or  coffee_origin='Indonesia'
order by 1 asc


