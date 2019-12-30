# SHIP TICKET BOOKING
http://lakport.nic.in/Home.aspx

## feature;
*ship ticket booking layout page

###feature1;
*source place to destination place



create table home
(
source_place varchar2(50)not null,
destination_place varchar2(50)not null,
security_code varchar2(10)not null,
constraint source_place_ck check(source_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea'),
constraint destination_place_ck check(destination_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea'),
constraint security_code_uk unique(security_code)
);

