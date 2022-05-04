# MYSQL-DATABASE

-- create the database
DROP DATABASE IF EXISTS REPAIR_SHOP;
CREATE DATABASE REPAIR_SHOP;

-- select the database
USE REPAIR_SHOP;
-- create customer info table
CREATE TABLE CUSTOMERS(
CUSTOMER_ID INT PRIMARY KEY AUTO_INCREMENT,
FIRST_NAME VARCHAR(40) NOT NULL, 
LAST_NAME VARCHAR(40) NOT NULL,
EMAIL VARCHAR(25)   NOT NULL ,
PHONE VARCHAR(15) NOT NULL) ;

-- create device information table
   
   CREATE TABLE DEVICE_INFO (
    DEVICE_ID INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    DEVICE_NAME VARCHAR(40) NOT NULL,
    MODEL VARCHAR(15) NOT NULL,
    BRAND VARCHAR(15)  NULL,
    ISSUE VARCHAR(40) NOT NULL ,
    CUSTOMER_ID INT  NULL ,
	CONSTRAINT Cust_Key
	FOREIGN KEY (CUSTOMER_ID) REFERENCES CUSTOMERS (CUSTOMER_ID));
    -- create session info table

-- create employee table
CREATE TABLE EMPLOYEE (
    EMPLOYEE_ID INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    FIRST_NAME VARCHAR(40) NOT NULL, 
    LAST_NAME VARCHAR(40) NOT NULL,
    POSITION VARCHAR(25) NOT NULL,
    HIRE_DATE DATE  NOT NULL,
    MANAGER_ID INT  NULL);
   
 -- create replacement parts table
CREATE TABLE PARTS (
    PART_ID INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    PART_NAME VARCHAR(40) NOT NULL, 
    PART_PRICE INT   NULL,
    PART_TYPE VARCHAR(20) NOT NULL DEFAULT 'Third Party',
    DEVICE_ID INT NOT NULL,
    CONSTRAINT  DEV_FK
    FOREIGN KEY (DEVICE_ID) REFERENCES DEVICE_INFO(DEVICE_ID));
    
    -- create repair cost table
CREATE TABLE REPAIRS (
    REPAIR_ID INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    REPAIR_FEE INT NOT NULL,
    TAX DECIMAL(5,2) NOT NULL DEFAULT '5.56',
    TOTAL_DUE DECIMAL(5,2) NULL,
	PART_ID INT NOT NULL, 
    FOREIGN KEY (PART_ID) REFERENCES PARTS (PART_ID));
       
CREATE TABLE SESSION_INFO (
    SESSION_ID INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
    CHECK_IN_DATE DATE  NOT NULL,
    QUOTED_MINUTES INT NOT NULL,
    START_TIME TIME NOT NULL,
    END_TIME TIME NOT NULL,
    TOTAL_MIN_SPENT INT NOT NULL,
    DEVICE_ID  INT NOT NULL ,
	EMPLOYEE_ID  INT NOT NULL,
    CHECK(END_TIME > START_TIME),
	REPAIR_ID  INT NOT NULL,
  FOREIGN KEY (EMPLOYEE_ID) REFERENCES EMPLOYEE(EMPLOYEE_ID),
  FOREIGN KEY (DEVICE_ID) REFERENCES DEVICE_INFO(DEVICE_ID),
  FOREIGN KEY (REPAIR_ID) REFERENCES REPAIRS(REPAIR_ID));
-- create device insurance table

CREATE TABLE INSURANCE (
    INSURANCE_ID INT PRIMARY KEY NOT NULL AUTO_INCREMENT,
	INSURANCE_TYPE VARCHAR(20)  NULL, 
    SESSION_ID INT NOT NULL,
    FOREIGN KEY (SESSION_ID) REFERENCES SESSION_INFO(SESSION_ID));
  
    
INSERT  INTO CUSTOMERS VALUES 
(1,'Yemi','Alade', 'yemi@me.com','937-876-9809'),
(2,'James','MacPherson','macjames@outlook.com','937-977-4567'),
(3,'Melanie','Green','melg21@aol.com','937-543-1243'),
(4,'Jane','Porter','porter@yahoo.com','937-980-5436'), 
(5,'Matt','Zinger','mattzing@gmail.com','937-123-6540'),
(6,'Mitch','Porter','mitchel@gmail.com','937-234-1654'),
(7,	'Dexter','Barnes','dexter.barnes@yahoo.com','515-127-4566'),	
(8,	'Liam',	'Henderson','liam.henderson@aol.com','650-123-2234'),	
(9,	'Callum','Jenkins','callum.jenkins@gmail.com','650-123-4234'),
(10,'Ronnie','Perry','ronnie.perry@yahoo.com','650-123-5234'),					
(11,'Steven','King',  'sking@gmail.com','515.123.4567' ),
(12, 'Neema','Kochhar','nmkochhar@me.com', '515.123.4568' ), 
(13, 'Lex','Eden', 'ldehaan@hotmail.com','515.123.4569'),
(14, 'Alexander','Grand', 'alexgrand@yahoo.fr', '590.423.4567'), 
(15, 'Jane','Markita', 'janamark@yahoo.com', '576.423.4597'); 

INSERT  INTO DEVICE_INFO VALUES 
(1,'Iphone SE','2nd Gen','Apple', 'Battery drains too fast',1),
(2,'Iphone SE',' 2nd Gen','Apple','Cracked display',1),
(3,'Galaxy','S22', 'Samsung','Liquid damage',9),
(4,'Iphone 13','Pro max','Apple', 'Not charging',3),
(5,'Galaxy','S21','Samsung', 'Camera not functional',4),
(6,'Iphone 12','Mini','Apple','5G sensor stopped working',5),
(7,'Galaxy','S21', 'Samsung','Face ID',6),
(8,'Iphone 13','Standard','Apple', 'unresponsive screen',7),
(9,'Galaxy','S22','Samsung', 'Does not power on',8),
(10,'Iphone 11','Pro Max','Apple','Cracked display',2),
(11,'Iphone 10','XR','Apple','Cracked display',10);


INSERT  INTO EMPLOYEE VALUES 
(1,'Tommy', 'Bailey','Technical Pro','2016-09-21',NULL),
(2,'Jude','Rivera','Technical Specialist','2018-07-21',1),	
(3,'Blake','Cooper','Seasonal Tech','2021-08-09',1),	
(4,'Louie','Richardson','Technical Pro','2016-01-03',NULL),
(5,'Nathan','Cox','Inventory Operator',	'2016-05-21',NULL),
(6,'Gabriel','Howard','Schedule Planner','2016-06-25',4),
(7,	'Leon','Powell','Stock Clerk',	'2016-07-16',5)	,	
(8,	'Kai',	'Long',	'Technical Pro','2017-09-28',NULL),
(9,	'Aaron','Patterson','Stock Clerk','2018-01-14',	8),	
(10, 'Roman', 'Hughes','Seasonal specialist','2019-03-08',8),
(11,'John','Mathew','Product Expert','2015-08-25',NULL),
(12,'Jim','Parker','Technical Expert','2015-02-05',NULL),
(13,'Sofia','Ran','Technical Specialist','2019-04-23',11),
(14,'Wendy','Blake','Stock clerk','2020-02-05',12),
(15,'Sarah','Ross','Seasonal specialist','2020-02-05',11);


INSERT  INTO PARTS VALUES 
(1,'Display', '100','Apple Original',2),
(2,'Battery','80','Apple Original',1),	
(3,'Whole Unit','279','Samsung Original',3),	
(4,'Charging port','56','Apple Original',4),
(5,'TeleCam','150',DEFAULT,4),
(6,'RV Sensor','76',DEFAULT,5),
(7,'TrueDepth Cm','270',DEFAULT,7),	
(8,'New Display','56','Apple Original',8),
(9,'Whole unit','280','Samsung Original',9),
(10,'New Display','130',DEFAULT,10);

INSERT  INTO REPAIRS VALUES 
(1,'80', '5.76','85.76',1),
(2,'76','6.13',NULL,2),	
(3,'156',DEFAULT,'161.56',4),	
(4,'70', '5.76',NULL,3),
(5,'86','6.13','92.13',6),	
(6,'156',DEFAULT,'201.9',5),	
(7,'121', DEFAULT,'136.56',8),
(8,'150','5.57',NULL,7),
(9,'50',DEFAULT,'55.56',9),
(10,'100','7.81','107.81',10);


INSERT INTO SESSION_INFO VALUES
(1,'2021-08-09','30', '10:30','11:13','43',2,4,1),
(2,'2021-08-09','30', '10:30','12:00','120',6,3,2),
(3,'2016-09-21', '60','9:30','11:00','90',3,2,3),
(4,'2016-01-03','50','1:15','2:10','55',7,9,6),
(5,'2016-05-21','13','2:00','2:45','45',9,5,4),
(6,'2016-09-21','45','3:10','3:55','45',1,8,3),
(7,'2021-08-09','60', '10:30','11:30','60',2,4,1),
(8,'2021-08-09','30', '4:30','4:45','15',6,7,2);

INSERT INTO INSURANCE VALUES
    (1,NULL,2),
    (2,'1Y Warranty',3),
    (3,'2Y Warranty',1),
    (4,NULL,7),
	(5,'1Y Warrant',4),
    (6,NULL,6),
    (7,'1Y Warranty',5);

	
