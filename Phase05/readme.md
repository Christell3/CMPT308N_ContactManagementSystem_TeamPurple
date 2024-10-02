Phase 05
[TeamPurple_ContactManagementSystem_Phase05.pdf](https://github.com/user-attachments/files/17231970/TeamPurple_ContactManagementSystem_Phase05.pdf)

CREATE DATABASE ProjectPhase04; #delete if database alr created
use ProjectPhase04; #change name of schema if diff

create table Contact (
Contact_ID int,
FName varchar(45),
LName varchar(45),
DOB  date,
Age date,
EmpStatus varchar(10),
primary key(Contact_ID),
unique(FName),
unique(LName)
);

create table Address (
Address_ID int,
Contact_ID int,
Street varchar(45),
City varchar(45),
State varchar(30),
ZipCode varchar(10),
Country varchar(30),
primary key(Address_ID),
foreign key(Contact_ID) references Contact(Contact_ID)
);

create table UserEvent (
Event_ID int,
Address_ID int,
EName varchar(50),
Edate date,
ELocation varchar(40),
EDescrip varchar(100),
EType varchar(30),
primary key(Event_ID),
foreign key(Address_ID) references Address(Address_ID)
);

create table Email (
Email_ID int,
Event_ID int ,
EAddr varchar(45),
EType varchar(10),
Priority  varchar(8),
DelivStatus varchar(8),
primary key(Email_ID),
foreign key(Event_ID) references UserEvent(Event_ID)
);

create table Phone (
Phone_ID int,
Contact_ID int,
Event_ID int,
PhoneNum varchar(20),
PType varchar(20),
IsPrimary varchar(1),
FaxNum varchar(20),
Ext int(4),
primary key(Phone_ID),
foreign key(Event_ID) references UserEvent(Event_ID),
foreign key(Contact_ID) references Contact(Contact_ID)
);

create table Users (
User_ID int,
UserN varchar(45),
PassW varchar(45),
LastLogin date,
UserType varchar(10),
primary key(User_ID)
);

create table UserGroup (
Group_ID int,
Contact_ID int,
User_ID int,
GName varchar(45),
GType varchar(45),
GDescrip varchar(100),
primary key(Group_ID),
foreign key(Contact_ID) references Contact(Contact_ID),
foreign key(User_ID) references Users(User_ID)
);

create table SocialMedia (
SM_ID int,
Group_ID int,
Platform varchar(45),
SMUser varchar(45),
ProfURL varchar(45),
primary key(SM_ID),
foreign key(Group_ID) references UserGroup(Group_ID)
);

create table Job (
Job_ID int,
Contact_ID int,
CompName varchar(45),
JobTitle varchar(45),
Dept varchar(45),
StartDate date,
EndDate date,
primary key(Job_ID),
foreign key(Contact_ID) references Contact(Contact_ID)
);

create table Note (
Note_ID int,
Contact_ID int,
NoteTXT varchar(100),
DateCreated date,
LastModDate date,
primary key(Note_ID),
foreign key(Contact_ID) references Contact(Contact_ID)
);
use proj;
SET FOREIGN_KEY_CHECKS=0;
insert into Users(User_ID,Contact_ID,UserN,PassW,LastLogin,UserType)
values
(0001,1001,'Christelle.B','Spongebob','2024-07-09','user'),
(0002,1002,'jessicalanes','imissmymom','2024-08-15','user'),
(0003,1003,'Adam03','helloworld','2024-09-28','admin'),
(0004,1004,'MichaelS','thebestboss','2024-09-25','user'),
(0005,1005,'GraceHMarkus','passw','2024-09-29','admin'),
(0006,1006,'NancyB','BarneysBeanery','2024-09-29','user'),
(0007,1007,'IsabellaA','marist','2024-09-29','admin'),
(0008,1008,'BrownEmma','hyena21','2024-09-30','user'),
(0009,1009,'WilliamsDaniel','mountains','2021-01-30','user'),
(0010,1010, 'TaylorEmily','goat56','2009-09-30','user');

insert into Contact(Contact_ID,FName,LName,DOB,Age,EmpStatus)
values
(1001,'MaNye','Wade','2004-08-17',20,'employed'),
(1002,'Emma','Johnson','1992-04-15',32,'employed'),
(1003,'Liam','Martin','1985-12-01',38,'employed'),
(1004,'Olivia','Brown','2000-07-22',24,'unemployed'),
(1005,'David','Thompson','1990-03-12',34,'employed'),
(1006,'Sarah','Mitchell','1985-06-25',39,'employed'),
(1007,'Michael','Brown','1998-01-08',26,'unemployed'),
(1008,'Emily','Jones','1995-11-14',28,'employed'),
(1009,'James','Carter','1975-08-30',49,'unemployed'),
(1010,'Joshua','Green','2001-02-17',23,'employed');

insert into Address(Address_ID,Contact_ID,Street,City,State,ZipCode,Country)
values
(2001,1001,'123 Maple Avenue','Los Angeles','California','90001','USA'),
(2002,1002,'206 Oak Street','Chicago','Illinois','60614','USA'),
(2003,1003,'323 Pine Road','Austin','Texas','73301','USA'),
(2004,1004,'400 Birch Lane','New York','New York','10001','USA'),
(2005,1005,'765 Sunset Blvd','Chicago','Illinois','60614','USA'),
(2006,1006,'40 Riverdale Drive','Miami','Florida','33101','USA'),
(2007,1007,'2 Elm Street','Houston','Texas','77002','USA'),
(2008,1008,'208 Beacon Hill Road','Boston','Massachusetts','02108','USA'),
(2009,1009,'22 King Avenue','Toronto','Ontario','M5V 3E7','Canada'),
(2010,1010,'89 Queen Street','Auckland','Auckland Region','1010','New Zealand');

insert into UserEvent(Event_ID,Address_ID,EName,EDate,ELocation,EDescrip,EType)
values
(3001,2001,'Company Retreat','2023-10-12','Aspen Lodge','Team-building activities and workshops.','work'),
(3002,2002,'John Birthday Party','2024-11-05','Johns House','Birthday celebration with friends.','friends'),
(3003,2003,'Family ','2024-07-18','Green Park','Annual family gathering with a barbecue.','family'),
(3004,2004,'Networking Lunch','2024-09-30','The Bistro','Casual lunch for professional networking.','work'),
(3005,2005,'Annual Sales Meeting','2024-10-05', 'Elm Convention Center', 'Company-wide sales update and strategy.', 'work'),
(3006,2006,'Sarah’s Baby Shower','2022-11-10', 'Sarah’s House', 'Celebration for Sarahs upcoming baby.','family'),
(3007,2007,'College Reunion Dinner','2023-12-02','Olive Garden','Casual dinner with college friends.','friends'),
(3008,2008,'Marketing Team Brainstorm','2024-10-18','Office Conference Room B','Ideas session for upcoming campaigns.','work'),
(3009,2009,'Thanksgiving Potluck','2024-11-23','Jacksons Backyard', 'Friends gathering for a potluck.','friends'),
(3010,2010,'Emilys Graduation Party','2024-06-15','The Beach House','Celebration of Emilys graduation.','friends');


insert into Email(Email_ID,Contact_ID,Eaddr,EType,Priority,DelivStatus)
values
(4001,(select Contact_ID from Users where UserN='Christelle.B'),'ChristelleB@gmail.com','Personal','High','Sent'),
(4002,(select Contact_ID from Users where UserN='jessicalanes'),'jessicalanes@gmail.com','Personal','High','Sent'),
(4003,(select Contact_ID from Users where UserN='Adam03'),'Adam03@gmail.com','Personal','High','Sent'),
(4004,(select Contact_ID from Users where UserN='MichaelS'),'MiachelS@gmail.com','Personal','High','Sent'),
(4005,(select Contact_ID from Users where UserN='GraceHMarkus'),'GraceHMarkus.com','Personal','High','Sent'),
(4006,(select Contact_ID from Users where UserN='NancyB'),'NancyB@gmail.com','Personal','High','Sent'),
(4007,(select Contact_ID from Users where UserN='IsabellaA'),'IsabellaA@gmail.com','Personal','High','Sent'),
(4008,(select Contact_ID from Users where UserN='BrownEmma'),'EmmaBrown@gmail.com','Personal','High','Sent'),
(4009,(select Contact_ID from Users where UserN='WilliamsDaniel'),'DanielWilliams@gmail.com','Personal','High','Sent'),
(4010,(select Contact_ID from Users where UserN='TaylorEmily'),'EmilyTaylor@gmail.com','Personal','High','Sent');

insert into Phone(Phone_ID,Contact_ID,CellNum,Ptype,IsPrimary,FaxNum)
values
(5001,(select Contact_ID from Users where UserN='Christelle.B'),'1111111111','Cell','Yes','1111111111'),
(5002,(select Contact_ID from Users where UserN='jessicalanes'),'1111111112','Cell','Yes','2111111111'),
(5003,(select Contact_ID from Users where UserN='Adam03'),'1111111113','Cell','Yes','3111111111'),
(5004,(select Contact_ID from Users where UserN='MichaelS'),'1111111114','Work','No','4111111111'),
(5005,(select Contact_ID from Users where UserN='GraceHMarkus'),'1111111115','Cell','Yes','5111111111'),
(5006,(select Contact_ID from Users where UserN='NancyB'),'1111111116','Cell','Yes','6111111111'),
(5007,(select Contact_ID from Users where UserN='IsabellaA'),'1111111117','Cell','No','7111111111'),
(5008,(select Contact_ID from Users where UserN='BrownEmma'),'1111111118','Cell','Yes','8111111111'),
(5009,(select Contact_ID from Users where UserN='WilliamsDaniel'),'1111111119','Work','Yes','9111111111'),
(5010,(select Contact_ID from Users where UserN='TaylorEmily'),'1111111110','Cell','Yes','1011111111');

insert into UserGroup(Group_ID,Contact_ID,User_ID,GName,GType,GDescrip)
values
(6001,(select Contact_ID from Users where UserN='Christelle.B'),(select User_ID from Users where UserN='Christelle.B'),'Work Project','Work','A work project'),
(6002,(select Contact_ID from Users where UserN='jessicalanes'),(select User_ID from Users where UserN='jessicalanes'),'Fam','Family','Family group chat'),
(6003,(select Contact_ID from Users where UserN='Adam03'),(select User_ID from Users where UserN='Adam03'),'Buds','Friends','Friends'),
(6004,(select Contact_ID from Users where UserN='MichaelS'),(select User_ID from Users where UserN='MichaelS'),'Roomies','Friends','Roomate group chat'),
(6005,(select Contact_ID from Users where UserN='GraceHMarkus'),(select User_ID from Users where UserN='GraceHMarkus'),'Team Chat','Organization','Water polo team groupchat'),
(6006,(select Contact_ID from Users where UserN='NancyB'),(select User_ID from Users where UserN='NancyB'),'Big3','Friends','Friend chat'),
(6007,(select Contact_ID from Users where UserN='IsabellaA'),(select User_ID from Users where UserN='IsabellaA'),'Feral Creatures','Friends','Friend group chat'),
(6008,(select Contact_ID from Users where UserN='BrownEmma'),(select User_ID from Users where UserN='BrownEmma'),'Hikes','Organization','Hiking group chat'),
(6009,(select Contact_ID from Users where UserN='WilliamsDaniel'),(select User_ID from Users where UserN='WilliamsDaniel'),'Siblinds','Family','Family group chat'),
(6010,(select Contact_ID from Users where UserN='TaylorEmily'),(select User_ID from Users where UserN='TaylorEmily'),'Kiara Birthday Party','Friends','Planning a party');

Insert into SocialMedia(SM_ID, Group_ID, Platform, SMUser, ProfURL)
VALUES
(7001, 6001, 'LinkedIn', 'john.doe', 'https://www.linkedin.com/in/john-doe'),
(7002, 6002, 'Twitter', 'sarah.smith', 'https://www.twitter.com/sarah_smith'),
(7003, 6003, 'Facebook', 'michael.brown', 'https://www.facebook.com/michael.brown'),
(7004, 6004, 'Instagram', 'linda.williams', 'https://www.instagram.com/linda_williams'),
(7005, 6005, 'LinkedIn', 'daniel.jones', 'https://www.linkedin.com/in/daniel-jones'),
(7006, 6006, 'YouTube', 'sophia.miller', 'https://www.youtube.com/c/sophia_miller'),
(7007, 6007, 'Facebook', 'oliver.johnson', 'https://www.facebook.com/oliver.johnson'),
(7008, 6008, 'Twitter', 'emma.davis', 'https://www.twitter.com/emma_davis'),
(7009, 6009, 'Instagram', 'william.garcia', 'https://www.instagram.com/william_garcia'),
(7010, 6010, 'YouTube', 'amelia.martinez', 'https://www.youtube.com/c/amelia_martinez');

INSERT INTO Job (Job_ID, Contact_ID, CompName, JobTitle, Dept, StartDate, EndDate)
VALUES
(8001, 1001, 'TechCorp', 'Software Engineer', 'Engineering', '2022-01-15', '2023-06-30'),
(8002, 1002, 'HealthPlus', 'Data Analyst', 'Analytics', '2021-09-01', '2022-12-31'),
(8003, 1003, 'EcoEnergy', 'Project Manager', 'Operations', '2023-03-01', NULL),
(8004, 1004, 'InnovateX', 'UX Designer', 'Design', '2020-05-10', '2021-07-15'),
(8005, 1005, 'EduPro', 'Education Consultant', 'Consulting', '2019-11-25', '2020-12-20'),
(8006, 1006, 'GreenTech', 'Environmental Engineer', 'Sustainability', '2021-04-01', '2022-08-30'),
(8007, 1007, 'FinServe', 'Financial Analyst', 'Finance', '2019-06-15', '2020-12-31'),
(8008, 1008, 'Health Innovations', 'Clinical Researcher', 'Research', '2022-02-01', '2023-03-31'),
(8009, 1009, 'AutoDrive', 'Mechanical Engineer', 'Engineering', '2020-10-01', NULL),
(8010, 1010, 'BrightFuture', 'Marketing Manager', 'Marketing', '2023-05-15', NULL);

INSERT INTO Note (Note_ID, Contact_ID, NoteTXT, DateCreated, LastModDate)
VALUES
(9001, 1001, 'Followed up on project progress.', '2023-08-01', '2023-08-05'),
(9002, 1002, 'Discussed the budget for Q3.', '2023-07-15', '2023-07-20'),
(9003, 1003, 'Sent final report to the client.', '2023-09-10', '2023-09-12'),
(9004, 1004, 'Scheduled a meeting to review performance.', '2023-06-22', '2023-06-25'),
(9005, 1005, 'Updated contact details and preferences.', '2023-05-10', '2023-05-11'),
(9006, 1006, 'Discussed potential collaboration for 2024.', '2023-04-18', '2023-04-22'),
(9007, 1007, 'Finalized the contract terms and signed agreement.', '2023-03-01', '2023-03-05'),
(9008, 1008, 'Completed training session feedback.', '2023-02-15', '2023-02-17'),
(9009, 1009, 'Updated CRM with new business opportunities.', '2023-01-30', '2023-02-02'),
(9010, 1010, 'Follow-up call scheduled with partner.', '2023-09-20', '2023-09-21');

oading TableCreationValues.sql…]()
