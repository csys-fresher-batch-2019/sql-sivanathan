# SHIP TICKET BOOKING:

http://lakport.nic.in/Home.aspx

## feature:

*ship ticket booking layout page

### feature1:

*source place to destination place


~~~sql
create table home
(
source_place varchar2(50)not null,
destination_place varchar2(50)not null,
ship_id number not null,
constraint ship_id primary key(ship_id),
constraint source_place_ck check(source_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea'),
constraint destination_place_ck check(destination_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')
);


