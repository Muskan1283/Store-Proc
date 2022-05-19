# Store-Proc
create database MVC_ADO_DB
use MVC_ADO_DB

create table Department(id int primary key identity,
Name varchar(80))

create table Employee(id int primary key identity,
Name varchar(100),
Email varchar(80),
Mobile varchar(100),
Gender varchar(50),
Address varchar(100),
IsActive bit,
Department int foreign key references Department(id))


create proc sp_Department
@action varchar(20),
@id int=0,
@name varchar(100)=null
as
begin

if @action='Create'
begin
insert into Department(Name)values(@name)
end
else if @action='Select'
begin
select*from Department
end
else if @action='Delete'
begin
delete from Department where id=@id
end
else if @action='Select_one'
begin
select*from Department where id=@id
end
else if @action='Update'
begin
update Department set Name=@name where id=@id
end
end

sp_Department 'Select'
sp_Department 'Create',0,'Manager'
sp_Department 'Select_one',2




