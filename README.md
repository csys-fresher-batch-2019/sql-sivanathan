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
create table user_detail
(

user_name varchar2(20) not null,
user_id number,
date_of_birth date not null,
contact_number number not null,
gender varchar2(2) not null,
pass varchar2(20) not null,
email varchar2(50) not null,
--CONSTRAINT chk_DOB check(date_of_birth IN(ROUND((SYSDATE-date_of_birth)/365))>=18,
--constraint check_date_of_birth check (date_of_birth in (between (date('01-01-1950','dd-MM-yyyy') and ((date('01-01-2020','dd-MM-yyyy')))),
constraint user_id_aa primary key(user_id),
constraint contact_number_bb check(contact_number between 1111111111 and 9999999999 ),
constraint gender_cc check (gender in ('M','F')),
constraint unique_dd unique(contact_number,email)

);

insert into user_detail values('siva',11111,to_date('01-11-1998','dd-MM-yyyy'),9999999999,'M','eeeee','siva@gmail.com');
insert into user_detail values('sumen',22222,to_date('10-12-1998','dd-MM-yyyy'),8888888888,'M','aaaaa','sumen@yahoo.com');
insert into user_detail values('bala',33333,to_date('21-01-1998','dd-MM-yyyy'),7777777777,'M','lllll','bala@chainsys.com');
insert into user_detail values('sathish',44444,to_date('21-11-1998','dd-MM-yyyy'),6666666666,'M','bbbbb','sathish@live.com');
insert into user_detail values('vicky',55555,to_date('21-05-1998','dd-MM-yyyy'),9090909090,'M','uuuuu','vicky@chainsys.com');
insert into user_detail values('thiru',66666,to_date('01-05-1998','dd-MM-yyyy'),8080808080,'M','vvvvv','thiru@live.com');

select*from user_detail;   --it is used the display the table content

commit;


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

create table ship_detail
(
--user_id number,
ship_id number not null,
ship_name varchar2(20),
--ship_type varchar2(20) not null,
source_place varchar2(50)not null,
destination_place varchar2(50)not null,
total_no_of_seats number not null,
--no_of_seats number not null,
classes varchar2(20) not null,
amount number not null,

--constraint user_id_fk foreign key(user_id) references user_s(user_id),
constraint ship_id_ee primary key(ship_id),
--constraint ship_type_ck check(ship_type in('all_passengers','all_hs_vessels','all_cargo_ship','amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint source_place_ff check(source_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint destination_place_gg check(destination_place in('amindivi','lagoons','kaavaratti','minicoy','corals','arabiansea','lakshadeepsea')),
constraint class_hh check(classes in('first_class','second_class','vip')),
constraint ii check(source_place<>destination_place)

);

insert into ship_detail values(112233,'aaa ship','amindivi','lagoons',200,'first_class',5000);
insert into ship_detail values(114455,'bbb ship','kaavaratti','minicoy',100,'vip',6000);
insert into ship_detail values(116677,'ccc ship','corals','arabiansea',150,'second_class',4000);
insert into ship_detail values(117788,'ddd ship','amindivi','arabiansea',200,'second_class',3000);
--insert into ship values(0909,0808,'all_passengers','amindivi','lagoons',8,'first class');
select*from ship_detail;

commit;~~~~

### feature3;
*journey

### table:

| journey_id | journey_date | ship_id | no_of_seats |
|------------|--------------|---------|-------------|
| 1611566    | 01-jan-20    | 767676  | 5           |
| 1611876    | 02-jan-20    | 764376  | 3           |
| 1611436    | 03-jan-20    | 987676  | 1           |

~~~sql
create table journey_detail
(

journey_id number,
source_date date,
destination_date date,
ship_id number,

constraint journey_id_jj primary key(journey_id),
constraint ship_id_kk foreign key(ship_id) references ship_detail(ship_id)
);

insert into journey_detail values(10202,to_date('01-01-2020','dd-MM-yyyy'),to_date('02-01-2020','dd-MM-yyyy'),112233);
insert into journey_detail values(10303,to_date('02-01-2020','dd-MM-yyyy'),to_date('03-01-2020','dd-MM-yyyy'),114455);
insert into journey_detail values(10404,to_date('03-01-2020','dd-MM-yyyy'),to_date('04-01-2020','dd-MM-yyyy'),116677);
insert into journey_detail values(10505,to_date('04-01-2020','dd-MM-yyyy'),to_date('05-01-2020','dd-MM-yyyy'),117788);
insert into journey_detail values(10606,to_date('05-01-2020','dd-MM-yyyy'),to_date('06-01-2020','dd-MM-yyyy'),117788);
select*from journey_detail;
commit;

~~~~

### table:


### feature4:
*seat booking

### table:

| booking_id | user_id | journey_id | booking_seats | ship_id | date_of_booking    | status       | cost |
|------------|---------|------------|---------------|---------|--------------------|--------------|------|
| 11111      | 12345   | 1611566    | 5             | 767676  | 02-jan-20 06:40:36 | ordered      | 7500 |
| 11441      | 13345   | 1611876    | 3             | 764376  | 02-jan-20 06:40:36 | waiting_list | null |
| 11131      | 14545   | 1611436    | 1             | 987676  | 02-jan-20 06:40:36 | ordered      | 5000 |

~~~sql

create table booking_detail
(
booking_id number not null, 
user_id number,
ship_id number,
journey_id number,
booking_seats number not null,
date_of_booking timestamp,
ticket_status varchar(20) not null,
cost number ,


constraint aaa foreign key(ship_id) references ship_detail(ship_id),
--constraint bbb unique(booking_id),
constraint qqq primary key(booking_id),
constraint ccc foreign key(user_id) references user_detail(user_id),
constraint ddd foreign key(journey_id) references journey_detail(journey_id),
constraint eee check(booking_seats>0),
constraint status_qq check(ticket_status in('pending','ordered','waiting_list'))
);
drop sequence booking_id;

create sequence booking_id start with 100 increment by 1;


insert into booking_detail values(booking_id.nextval,11111,112233,10202,5,SYSTIMESTAMP,'pending',5000);
insert into booking_detail values(booking_id.nextval,22222,114455,10303,2,SYSTIMESTAMP,'pending',6000);
insert into booking_detail values(booking_id.nextval,33333,116677,10404,8,SYSTIMESTAMP,'pending',7000);

--update booking_detail set cost=(booking_seats*(select amount from ship_detail where ship_id=767676)) where ship_id=767676 and user_id=12345; 
--update booking_detail set cost=(booking_seats*(select amount from ship_detail where ship_id=764376)) where ship_id=764376 and user_id=13345; 
--update booking_detail set cost=(booking_seats*(select amount from ship_detail where ship_id=987676)) where ship_id=987676 and user_id=14545; 

select*from booking_detail;

--create sequence booking_id start with 1000 increment by 1;

-------------------------------------------------------created procedure as seat_availabilitys--------------------------------
drop procedure ticket_booking;

create or replace procedure TICKET_BOOKING
(
user_id in number,ship_no in number,journey_id in number,booking_seats in number,ticket_status in out varchar2,cost in number
)
AS
seat_count number;
fare number;


BEGIN
 fare:=booking_seats*cost;
select available_seat into seat_count from seat_availability where ship_id=ship_no;
 if(seat_count>=booking_seats) then
   insert into booking_detail(booking_id,user_id,ship_id,journey_id,booking_seats,date_of_booking,ticket_status,cost) values (booking_id.nextval,user_id,ship_no,journey_id,booking_seats,SYSTIMESTAMP,ticket_status,fare);
   update seat_availability set available_seat=(available_seat - booking_seats) where ship_id=ship_no;
   update booking_detail set ticket_status='ordered' where ship_id=ship_no;
 else
     update booking_detail set ticket_status='waiting_list' where ship_id=ship_no;
end if;
commit;
END TICKET_BOOKING;
/
------------------------------------------------
DECLARE

user_id number:=22222;
ship_no number:= 114455;
journey_id number:=10303;
booking_seats number:=2;
ticket_status varchar2(20):='pending';
cost number:=6000;

BEGIN

TICKET_BOOKING
(
user_id,
ship_no,
journey_id,
booking_seats,
ticket_status,
cost
);
dbms_output.put_line ('ticket_status'|| ticket_status);
END;
commit;

~~~~
### feature5:
seat availability

~~~sql
drop table seat_availability;
create table seat_availability
(

ship_id number,
journey_id number,
available_seat number,


constraint ship_id_aq foreign key(ship_id) references ship_detail(ship_id),
constraint tttt foreign key(journey_id) references journey_detail(journey_id)

);

select * from seat_availability ;

insert into seat_availability values(112233,10202,100);
insert into seat_availability values(114455,10303,100);
insert into seat_availability values(116677,10404,100);
select*from seat_availability;
commit;
