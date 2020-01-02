# SHIP TICKET BOOKING:

http://lakport.nic.in/Home.aspx

## feature:

*ship ticket booking layout page

### feature1:

*layout for user

### table:

| user_name | user_id | date_of_birth | contact number | gender | pass |
|-----------|---------|---------------|----------------|--------|------|
| siva      | 12345   | 01-nov-98     | 9876543210     | M      | xyx  |
| sumen     | 13345   | 10-dec-98     | 9876643210     | M      | aaa  |
| bala      | 14545   | 21-jan-98     | 9870043210     | M      | lll  |


``` sql
drop table user_s;
drop table ship;
drop table journey;
drop table booking;


create table user_s
(
user_name varchar2(20) not null,
user_id number,
date_of_birth date not null,
contact_number number not null,
gender varchar2(2) not null,
pass varchar2(20) not null,
constraint gender_ck check (gender in ('M','F')),
constraint contact_number_cs check(contact_number between 1111111111 and 9999999999 ),
constraint user_id_pk primary key(user_id),
constraint user_name_uk unique(user_name,pass)
);
insert into user_s values('siva',12345,to_date('01-11-1998','dd-MM-yyyy'),9876543210,'M','xyx');
insert into user_s values('sumen',13345,to_date('10-12-1998','dd-MM-yyyy'),9876643210,'M','aaa');
insert into user_s values('bala',14545,to_date('21-01-1998','dd-MM-yyyy'),9870043210,'M','lll');
select*from user_s;


`````


### feature2:

*layout of ship schedule

### table:

| user_id | ship_id | ship_type      | source_place | destination_place | total_no_of_seats | classes      |
|---------|---------|----------------|--------------|-------------------|-------------------|--------------|
| 12345   | 767676  | all_passengers | amindivi     | lagoons           | 100               | first_class  |
| 13345   | 764376  | all_hr_vessels | kaavaratti   | minicoy           | 50                | owners       |
| 14545   | 987676  | all_cargo_ship | corals       | arabiansea        | 150               | second_class |

~~~sql:

create table ship
(
user_id number,
ship_id number not null,
ship_type varchar2(20) not null,
source_place varchar2(50)not null,
destination_place varchar2(50)not null,
no_of_seats number not null,
classes varchar2(20) not null,

constraint user_id_fk foreign key(user_id) references user_s(user_id),
constraint class_cc check(classes in('ladies','first class','second class','bunk','owners','vip')),
constraint ship_type_ck check(ship_type in('all_passengers','all_hs_vessels','all_cargo_ship','amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint source_place_cp check(source_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint destination_place_cp check(destination_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint ship_id_un primary key(ship_id)
);



insert into ship values(12345,767676,'all_passengers','amindivi','lagoons',5,'first class');
insert into ship values(13345,764376,'all_hs_vessels','kaavaratti','minicoy',2,'owners');
insert into ship values(14545,987676,'all_cargo_ship','corals','arabiansea',1,'second class');
select * from ship where(source_place<>destination_place);

~~~~

### feature3;
*journey

### table:

| journey_id | journey_date | ship_id | no_of_seats |
|------------|--------------|---------|-------------|
| 1611566    | 01-jan-20    | 767676  | 5           |
| 1611876    | 02-jan-20    | 764376  | 3           |
| 1611436    | 03-jan-20    | 987676  | 1           |

~~~sql
create table journey
(
journey_id number,
journey_date date,
ship_id number,
total_no_of_seats number not null,
constraint journey_id_pk primary key(journey_id),
constraint ship_id_fr foreign key(ship_id) references ship(ship_id)
);
insert into journey values(1611566,to_date('01-01-2020','dd-MM-yyyy'),767676,100);
insert into journey values(1611876,to_date('02-01-2020','dd-MM-yyyy'),764376,100);
insert into journey values(1611436,to_date('03-01-2020','dd-MM-yyyy'),987676,100);
select*from journey;



~~~~

### table:


### feature4:
*seat booking

### table:


| booking_id | user_id | journey_id | booking_seats | ship_id | date_of_booking    | status       |
|------------|---------|------------|---------------|---------|--------------------|--------------|
| 11111      | 12345   | 1611566    | 5             | 767676  | 02-jan-20 06:40:36 | ordered      |
| 11441      | 13345   | 1611876    | 3             | 764376  | 02-jan-20 06:40:36 | waiting_list |
| 11131      | 14545   | 1611436    | 1             | 987676  | 02-jan-20 06:40:36 | ordered      |

~~~sql

create table booking
(
booking_id number not null, 
user_id number,
journey_id number,
booking_seats number not null,
ship_id number,
date_of_booking timestamp,
status varchar(20) not null,
constraint sship_id_fk foreign key(ship_id) references ship(ship_id),
constraint user_id_fa foreign key(user_id) references user_s(user_id),
constraint journey_id_fz foreign key(journey_id) references journey(journey_id),
constraint status_ck check(status in('ordered','waiting_list','cancelled')),
constraint booking_id_pk unique(booking_id)
);
insert into booking values(11111,12345,1611566,5,767676,SYSTIMESTAMP,'ordered');
insert into booking values(11441,13345,1611876,2,764376,SYSTIMESTAMP,'waiting_list');
insert into booking values(11131,14545,1611436,1,987676,SYSTIMESTAMP,'ordered');

select*from booking ;

