# SHIP TICKET BOOKING:

http://lakport.nic.in/Home.aspx

## feature:

*ship ticket booking layout page

### feature1:

*source place to destination place

### table:
| source_place | destination_place | ship_id | enroll_id | terms_and_condition | refund_or_cancellation | contact_number | about_us |
|--------------|-------------------|---------|-----------|---------------------|------------------------|----------------|----------|
| minicoy      | lagoons           | 1324    | 16159     | null                | no                     | 9876543210     | null     |
| amindivi     | lagooons          | 1524    | 13259     | null                | yes                    | 9875643210     | null     |
| corals       | arabiansea        | 1894    | 23456     | null                | no                     | 8776532100     | null     |


``` sql
drop table home;
drop table ship_schedule;
drop table fare_table;
drop table seat_availability;


create table home
(
source_place varchar2(50)not null,
destination_place varchar2(50)not null,
ship_id number not null,
enroll_id number,
terms_and_conditions varchar2(200),
refund_or_cancellation varchar2(20),
contact_number varchar(11) not null,
about_us varchar2(200),
constraint contact_number_cs check(contact_number between 1111111111 and 9999999999 ),
constraint refund_or_cancellation_cs check(refund_or_cancellation in('yes','no')),

constraint enroll_id_pk primary key(enroll_id),
constraint source_place_cp check(source_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint destination_place_cp check(destination_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea'))
);
insert into home values('minicoy','lagoons',1324,16159,'null','no','9876543210','null');
insert into home values('amindivi','lagoons',1524,13259,'null','yes','9875643210','null');
insert into home values('corals','arabiansea',1894,23456,'null','no','8776543210','null');
select*from home;
`````


### feature2:

*layout of ship schedule

~~~sql:

create table ship_schedule
(
ship_detail varchar2(20) not null,
arr_date date not null,
destination_date date,
constraint ship_detail_ck check(ship_detail in('all_passengers','all_hs_vessels','all_cargo_ship','amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea'))
);

insert into ship_schedule(ship_detail,arr_date,destination_date) values('all_passengers',to_date('01.01.2020','dd.MM.yyyy'),to_date('05.01.2020','dd.MM.yyyy'));
insert into ship_schedule(ship_detail,arr_date,destination_date) values('all_hs_vessels',to_date('06.01.2020','dd.MM.yyyy'),to_date('10.01.2020','dd.MM.yyyy'));
insert into ship_schedule(ship_detail,arr_date,destination_date) values('all_cargo_ship',to_date('08.01.2020','dd.MM.yyyy'),to_date('12.01.2020','dd.MM.yyyy'));
--desc ship_schedule;
~~~~

### feature3;
*fare table

~~~sql

create table fare_table(
ship_detail varchar2(20) not null,
constraint ship_detail_co check(ship_detail in('all_passengers','all_hs_vessels','all_cargo_ship','amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
classes varchar2(20) not null,
constraint class_ck check(classes in('ladies','first class','second class','bunk','owners','vip')),
price number,
freight_name varchar2(20) not null,
fare number not null,
constraint name_cz check(freight_name in('AC CONDITIONERS','BABYCYCLE','COMPUTER_TABLE','CAR')),
constraint fare_cz check(fare in(1000,100,50,2000))

);
insert into fare_table values('all_passengers','first class',7000,'AC CONDITIONERS',1000);
insert into fare_table values('all_hs_vessels','owners',10000,'COMPUTER_TABLE',50);
insert into fare_table values('all_cargo_ship','second class',5000,'BABYCYCLE',100);

select s.ship_detail,s.arr_date,s.destination_date,fa.classes,fa.price,fa.freight_name,fa.fare from ship_schedule s inner join fare_table fa on s.ship_detail = fa.ship_detail;
~~~~

### table:

| ship_detail    | arr_date  | destination_date | class        | price | freight_name    | fare |
|----------------|-----------|------------------|--------------|-------|-----------------|------|
| all_passengers | 01-jan-20 | 05-jan-20        | first class  | 7000  | AC CONDITIONERS | 1000 |
| all_hs_vessels | 06-jan-20 | 10-jan-20        | owners       | 10000 | COMPUTER_TABLE  | 50   |
| all_cargo_ship | 08-jan-20 | 12-jan-20        | second class | 5000  | BABYCYCLE       | 100  |


### feature4:
*seat availability

### table:

| seat_pp | categories | route_view | source_place | destination_place | ticket_number | available_status |
|---------|------------|------------|--------------|-------------------|---------------|------------------|
| yes     | all        | yes        | minicoy      | lagoons           | 12345         | available        |
| no      | direct     | no         | amindivi     | lagoons           | 14545         | waiting_list     |
| yes     | indirect   | yes        | corals       | arabiansea        | 12225         | available        |

~~~sql

create table seat_availability
(
seat_pp varchar2(10),
categories varchar2(10),
route_viewes varchar2(5),
source_place varchar2(50)not null,
destination_place varchar2(50)not null,
ticket_number number not null,
available_status varchar2(20),
constraint available_status_cu check(available_status in('waiting_list','available')),
constraint ticket_number_pu primary key(ticket_number),

constraint source_place_cu check(source_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint destination_place_cu check(destination_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint categories_cu check(categories in('all','direct','indirect')),
constraint route_viewes_cu check(route_viewes in('yes','no')),
constraint seat_pu check(seat_pp in('yes','no'))
);
insert into seat_availability values('yes','all','yes','minicoy','lagoons',12345,'available');
insert into seat_availability values('no','direct','no','kaavaratti','minicoy',14545,'waiting_list');
insert into seat_availability values('yes','indirect','yes','corals','arabiansea',12225,'available');
select*from seat_availability;


