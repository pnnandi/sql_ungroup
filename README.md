# sql_ungroup
--Ungroup a table with total count. 

--Code for table creation

create table items(id int, item_name varchar(30), total_count int);

insert into items(id, item_name, total_count) 
values(1, 'Mobile', 4),
values(2, 'Laptop', 1),
values(3, 'camera', 3),
values(4, 'Desktop', 2);

--solution in PostgreSQL

with recursive un_group as (
  select id, item_name, total_count from items
  
  union
  
  select id, item_name, total_count-1 from un_group where total_count>1
  )
 
 select id, item_name from un_group order by 1;
