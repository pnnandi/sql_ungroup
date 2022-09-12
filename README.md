# sql_ungroup
--Ungroup a table with total count. 

--Code for table creation

create table product_sold(id int, item_name varchar(30), total_count int);

insert into product_sold(id, item_name, total_count) values(1, 'Mobile', 4), 
(2, 'Laptop', 1), 
(3, 'camera', 3), 
(4, 'Desktop', 2);

--solution in PostgreSQL

with recursive un_group as ( select id, item_name, total_count from product_sold

union

select id, item_name, total_count-1 from un_group where total_count>1 )

select id, item_name from un_group order by 1;
