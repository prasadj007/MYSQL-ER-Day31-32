show databases;

#UC1 
create database employee_payroll_service;
use employee_payroll_service;
select database();

#UC2
drop table employee_payroll;
create table employee_payroll
(
	id INT unsigned NOT NULL AUTO_INCREMENT,
	name VARCHAR(150) NOT NULL,
    salary double NOT NULL ,
    start DATE NOT NULL,
    primary key (id)
);
describe employee_payroll;

#UC3
insert into employee_payroll (name,salary,start) values
	('Bill',1000000.0,'2018-01-03'),
    ('Mark',2000000.0,'2019-11-13'),
    ('Charlie',3000000.0,'2020-05-21');
    
#UC4    
select * from employee_payroll;  

#UC5
select salary from employee_payroll where name='Bill';
select * from employee_payroll where start between cast( '2018-01-01' as date) and date((now()));

#UC6
alter table employee_payroll add gender char(1) not null after name  ;
update employee_payroll set gender ='F' where name='Charlie';
select * from employee_payroll;
update employee_payroll set gender ='M' where name='Bill' or name='Mark';
select * from employee_payroll;

#UC7
select sum(salary) from employee_payroll where gender='M' group by gender;
select avg(salary) from employee_payroll where gender='M' group by gender;
select max(salary) from employee_payroll;
select min(salary) from employee_payroll;
select count(id) from employee_payroll;

#UC8
alter table employee_payroll add phone_number int(10) not null ;
alter table employee_payroll modify phone_number int(10) after name;
select * from employee_payroll;
update employee_payroll set phone_number='1325469781' where name='Bill';
select * from employee_payroll;
update employee_payroll set phone_number='978546132' where name='Mark';
select * from employee_payroll;
update employee_payroll set phone_number='654978132' where name='Charlie';
select * from employee_payroll;
alter table employee_payroll add address varchar(225) not null  default 'Mumbai,Maharashtra' after phone_number ;
select * from employee_payroll;
alter table employee_payroll rename employee_details;
select * from employee_details;

#UC9 
Drop table employee_payroll;
CREATE table employee_payroll (
ID          int NOT Null auto_increment,
Name        varchar(45) Not Null,
Salary      double Not Null,
Start_Date date not null,
Primary key(ID) 
);

insert into employee_payroll (Name,Salary,Start_Date) values
				('Bill',1000000.0,'2018-01-03'),
				('Mark',2000000.0,'2019-11-13'),
				('Charlie',3000000.0,'2020-05-21');

alter table employee_payroll drop Salary;
alter table employee_payroll add basic_pay float(10) not null default '500000.0' after name;
select * from employee_payroll;
alter table employee_payroll add Deductions float(10) not null default '60000.0' after basic_pay;
select * from employee_payroll;
alter table employee_payroll add Taxable_pay float(10) not null default '7000.0' after Deductions;
alter table employee_payroll add Income_Tax float(10) not null default '200000.0' after Taxable_pay;
alter table employee_payroll add Net_Pay float(10) not null default '1000000.0' after Income_Tax;
select * from employee_payroll;

#UC10
Drop table Employee_Details;
CREATE table Employee_Details (
EmployeeID      int NOT Null auto_increment,
Name       varchar(20) Not Null,
Gender    char not null,
Mobile_Number int(10) not null,
Address        varchar(50) Not Null,
Experience      Varchar(20) Not Null, 
EmailId         varchar(50) Not Null,
Primary key(EmployeeID),
FOREIGN KEY (EmployeeID) REFERENCES employee_payroll (id) ON DELETE CASCADE 
);
Insert into Employee_Details ( Name, Gender, Mobile_Number , Address, Experience, emailId) values ( 'Bill', 'M' ,'1325469781' , 'Mumbai' ,  '4 Years', 'lubill@hotmail.com'),
																								 ( 'Mark',  'M' , ' 789546122' , 'shimla', '3 Years', 'garysmith@cop.in'),
																								 ( 'Charlie', 'F' , '546981322', 'japan' , '2 Years', 'terisa2@gmial.com');
 Select * From employee_Details;  
  
#UC11
create table employee_department
(
Id                 int NOT Null auto_increment,
EmpId              int Not Null,
DeptName           varchar(45) Not null,
Primary key(Id),
FOREIGN KEY (EmpId) REFERENCES employee_details(EmployeeID) ON DELETE CASCADE
);

Insert into employee_department ( EmpId, DeptName) values (  '1', 'Finance'),
												  (  '2', 'Sales'),
												  ( '3', 'Marketing');
select * from employee_department;
Insert into employee_department ( EmpId, DeptName) values (  '3', 'HR');

#UC12
select * from employee_payroll emp1 , employee_details emp2
		 where  emp1.id=emp2.EmployeeID;
select sum(Net_Pay) from employee_payroll emp1 , employee_details emp2
		 where  emp1.id=emp2.EmployeeID;
select sum(Net_Pay) from employee_payroll emp1 , employee_details emp2
		 where  emp1.id=emp2.EmployeeID ;
select avg(Net_Pay) from employee_payroll emp1 , employee_details emp2
		 where  emp1.id=emp2.EmployeeID ; 
         
select count(name) from employee_details emp1 , employee_department emp2
		 where  emp1.EmployeeID=emp2.EmpId ;   #Count 4
         
select count(id) from employee_payroll emp1 , employee_details emp2
		 where  emp1.Id=emp2.EmployeeID ; 	#count 3