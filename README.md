# SHIP TICKET BOOKING:

http://lakport.nic.in/Home.aspx

## feature:

*ship ticket booking layout page

### feature1:

*layout for user

### table:
| USER_NAME | USER_ID | DATE_OF_BIRTH | CONTACT_NUMBER | GENDER | PASS  | EMAIL                   |
|-----------|---------|---------------|----------------|--------|-------|-------------------------|
| siva      | 11111   | 01-11-1998    | 9999999999     | M      | eeeee | sivanatha1998@gmail.com |
| sumen     | 22222   | 10-12-1998    | 8888888888     | M      | aaaaa | sumen@yahoo.com         |
| bala      | 33333   | 21-01-1998    | 7777777777     | M      | lllll | bala@chainsys.com       |
| sathish   | 44444   | 21-11-1998    | 6666666666     | M      | bbbbb | sathish@live.com        |
| vicky     | 55555   | 21-05-1998    | 9090909090     | M      | uuuuu | vicky@chainsys.com      |
| muthu     | 66666   | 01-05-1998    | 8080808080     | M      | muthu | muthu9825@gmail.com     |


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

insert into user_detail(user_name,user_id,date_of_birth,contact_number,gender,pass,email)
values('siva',11111,to_date('01-11-1998','dd-MM-yyyy'),9999999999,'M','eeeee','sivanatha1998@gmail.com');
insert into user_detail(user_name,user_id,date_of_birth,contact_number,gender,pass,email) 
values('sumen',22222,to_date('10-12-1998','dd-MM-yyyy'),8888888888,'M','aaaaa','sumen@yahoo.com');
insert into user_detail(user_name,user_id,date_of_birth,contact_number,gender,pass,email) 
values('bala',33333,to_date('21-01-1998','dd-MM-yyyy'),7777777777,'M','lllll','bala@chainsys.com');
insert into user_detail(user_name,user_id,date_of_birth,contact_number,gender,pass,email) 
values('sathish',44444,to_date('21-11-1998','dd-MM-yyyy'),6666666666,'M','bbbbb','sathish@live.com');
insert into user_detail(user_name,user_id,date_of_birth,contact_number,gender,pass,email) 
values('vicky',55555,to_date('21-05-1998','dd-MM-yyyy'),9090909090,'M','uuuuu','vicky@chainsys.com');
insert into user_detail(user_name,user_id,date_of_birth,contact_number,gender,pass,email) 
values('muthu',66666,to_date('01-05-1998','dd-MM-yyyy'),8080808080,'M','muthu','muthu9825@gmail.com');

select*from user_detail;   --it is used the display the table content
commit;


`````


### feature2:

*layout of ship schedule

### table:
| SHIP_NAME | SOURCE_PLACE | TOTAL_NO_OF_SEATS | CLASSES      | AMOUNT |
|-----------|--------------|-------------------|--------------|--------|
| aaa ship  | amindivi     | 200               | first_class  | 5000   |
| bbb ship  | kaavaratti   | 100               | vip          | 6000   |
| ccc ship  | corals       | 150               | second_class | 4000   |
| ddd ship  | amindivi     | 200               | second_class | 3000   |

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

insert into ship_detail(ship_id,ship_name,source_place,destination_place,total_no_of_seats,classes,amount)
values(112233,'aaa ship','amindivi','lagoons',200,'first_class',5000);
insert into ship_detail(ship_id,ship_name,source_place,destination_place,total_no_of_seats,classes,amount)
values(114455,'bbb ship','kaavaratti','minicoy',100,'vip',6000);
insert into ship_detail(ship_id,ship_name,source_place,destination_place,total_no_of_seats,classes,amount) 
values(116677,'ccc ship','corals','arabiansea',150,'second_class',4000);
insert into ship_detail(ship_id,ship_name,source_place,destination_place,total_no_of_seats,classes,amount) 
values(117788,'ddd ship','amindivi','arabiansea',200,'second_class',3000);
--insert into ship values(0909,0808,'all_passengers','amindivi','lagoons',8,'first class');
select*from ship_detail;
commit;


~~~~

### feature2:

*layout of journey schedule

### table:
| JOURNEY_ID | SOURCE_DATE | DESTINATION_DATE | SHIP_ID |
|------------|-------------|------------------|---------|
| 10202      | 01-01-20    | 02-01-20         | 112233  |
| 10707      | 11-01-20    | 12-01-20         | 112233  |
| 10303      | 02-01-20    | 03-01-20         | 114455  |
| 10808      | 12-01-20    | 13-01-20         | 114455  |
| 10404      | 03-01-20    | 04-01-20         | 116677  |
| 10909      | 13-01-20    | 14-01-20         | 116677  |
| 10505      | 04-01-20    | 05-01-20         | 117788  |
| 10606      | 14-01-20    | 15-01-20         | 117788  |

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

insert into journey_detail(journey_id,source_date,destination_date,ship_id) 
values(10202,to_date('01-01-2020','dd-MM-yyyy'),to_date('02-01-2020','dd-MM-yyyy'),112233);
insert into journey_detail(journey_id,source_date,destination_date,ship_id)
values(10707,to_date('11-01-2020','dd-MM-yyyy'),to_date('12-01-2020','dd-MM-yyyy'),112233);
insert into journey_detail(journey_id,source_date,destination_date,ship_id)
values(10303,to_date('02-01-2020','dd-MM-yyyy'),to_date('03-01-2020','dd-MM-yyyy'),114455);
insert into journey_detail(journey_id,source_date,destination_date,ship_id)
values(10808,to_date('12-01-2020','dd-MM-yyyy'),to_date('13-01-2020','dd-MM-yyyy'),114455);
insert into journey_detail(journey_id,source_date,destination_date,ship_id)
values(10404,to_date('03-01-2020','dd-MM-yyyy'),to_date('04-01-2020','dd-MM-yyyy'),116677);
insert into journey_detail(journey_id,source_date,destination_date,ship_id)
values(10909,to_date('13-01-2020','dd-MM-yyyy'),to_date('14-01-2020','dd-MM-yyyy'),116677);
insert into journey_detail(journey_id,source_date,destination_date,ship_id) 
values(10505,to_date('04-01-2020','dd-MM-yyyy'),to_date('05-01-2020','dd-MM-yyyy'),117788);
insert into journey_detail(journey_id,source_date,destination_date,ship_id)
values(10606,to_date('14-01-2020','dd-MM-yyyy'),to_date('15-01-2020','dd-MM-yyyy'),117788);
select*from journey_detail;
commit;

~~~~




### feature4:
*seat booking

### table:

| BOOKING_ID | USER_ID | SHIP_ID | JOURNEY_ID | BOOKING_SEATS | DATE_OF_BOOKING | TICKET_STATUS | COST |
|------------|---------|---------|------------|---------------|-----------------|---------------|------|
| 100        | 11111   | 112233  | 10202      | 5             |                 | pending       | 5000 |
| 101        | 22222   | 114455  | 10303      | 2             |                 | pending       | 6000 |
| 102        | 33333   | 116677  | 10404      | 8             |                 | pending       | 7000 |
| 103        | 11111   | 112233  | 10202      | 5             |                 | pending       | 5000 |

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
--CONSTRAINT fk_column FOREIGN KEY(user_id) REFERENCES user_detail(user_id) ON DELETE CASCADE
);


create sequence booking_id start with 100 increment by 1;


insert into booking_detail(booking_id,user_id,ship_id,journey_id,booking_seats,date_of_booking,ticket_status,cost)
values(booking_id.nextval,11111,112233,10202,5,SYSTIMESTAMP,'pending',5000);
insert into booking_detail(booking_id,user_id,ship_id,journey_id,booking_seats,date_of_booking,ticket_status,cost) 
values(booking_id.nextval,22222,114455,10303,2,SYSTIMESTAMP,'pending',6000);
insert into booking_detail(booking_id,user_id,ship_id,journey_id,booking_seats,date_of_booking,ticket_status,cost) 
values(booking_id.nextval,33333,116677,10404,8,SYSTIMESTAMP,'pending',7000);

insert into booking_detail(booking_id,user_id,ship_id,journey_id,booking_seats,date_of_booking,ticket_status,cost)
values(booking_id.nextval,11111,112233,10202,8,SYSTIMESTAMP,'pending',5000);


--update booking_detail set cost=(booking_seats*(select amount from ship_detail where ship_id=767676)) where ship_id=767676 and user_id=12345; 
--update booking_detail set cost=(booking_seats*(select amount from ship_detail where ship_id=764376)) where ship_id=764376 and user_id=13345; 
--update booking_detail set cost=(booking_seats*(select amount from ship_detail where ship_id=987676)) where ship_id=987676 and user_id=14545; 

select*from booking_detail;

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
###TABLE:
| SHIP_ID | JOURNEY_ID | AVAILABLE_SEATS |
|---------|------------|-----------------|
| 112233  | 10202      | 100             |
| 112233  | 10707      | 200             |
| 114455  | 10303      | 100             |
| 114455  | 10808      | 200             |
| 116677  | 10404      | 100             |
| 116677  | 10909      | 200             |
| 117788  | 10505      | 100             |
| 117788  | 10606      | 200             |
| 112233  | 10202      | 100             |
| 112233  | 10707      | 200             |
| 114455  | 10303      | 100             |
| 114455  | 10808      | 200             |
| 116677  | 10404      | 100             |
| 116677  | 10909      | 200             |
| 117788  | 10505      | 100             |
| 117788  | 10606      | 200             |
~~~sql

create table seat_availability
(

ship_id number,
journey_id number,
available_seat number,


constraint ship_id_aq foreign key(ship_id) references ship_detail(ship_id),
constraint tttt foreign key(journey_id) references journey_detail(journey_id)

);



insert into seat_availability(ship_id,journey_id,available_seat) values(112233,10202,100);
insert into seat_availability(ship_id,journey_id,available_seat) values(112233,10707,200);
insert into seat_availability(ship_id,journey_id,available_seat) values(114455,10303,100);
insert into seat_availability(ship_id,journey_id,available_seat) values(114455,10808,200);
insert into seat_availability(ship_id,journey_id,available_seat) values(116677,10404,100);
insert into seat_availability(ship_id,journey_id,available_seat) values(116677,10909,200);
insert into seat_availability(ship_id,journey_id,available_seat) values(117788,10505,100);
insert into seat_availability(ship_id,journey_id,available_seat) values(117788,10606,200);
select*from seat_availability;
commit;
~~~~
###FEATURE:

###TABLE:
| ADMIN_ID | ADMIN_NAME | ADMIN_EMAIL       | PASS_WORD  |
|----------|------------|-------------------|------------|
| 1234     | sathish    | sathish@gmail.com | sathish123 |
| 1235     | suresh     | suresh@gmail.com  | suresh123  |

~~~SQL


create table AdminRegister
(
Admin_id number ,
Admin_name varchar(20) not null,
Email_id varchar(30) ,
pass_word varchar(30) not null,
constraint admin_id_uk unique (admin_id),
constraint Email_id_uh unique (Email_id)
);

insert into AdminRegister(Admin_id,Admin_name,Email_id,pass_word)
values(1234,'sathish','sathish@gmail.com','sathish123');
insert into AdminRegister(Admin_id,Admin_name,Email_id,pass_word)
values(1235,'suresh','suresh@gmail.com','suresh123');
select * from AdminRegister;
commit;

