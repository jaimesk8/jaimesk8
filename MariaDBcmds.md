- Hi, I’m @jaimesk8
- I’m currently  learning   SQL  w/ MariaDB 
- I’m looking to collaborate with every one
- How to reach me   ojaimemarinho@gmail.com

<!---
This is a reportory of some SQL in MariaDB.

MariaDB is a database management system released on January 22, 2009. 
MariaDB Compatibility is kept up to date with the latest MySQL version and will work just like MySQL. All commands, interfaces, 
libraries and APIs that exist in MySQL also exist in MariaDB. 
There is no need for data conversion to display MariaDB.


--->
DROP DATABASE IF EXISTS Company;

CREATE DATABASE Company CHARACTER SET LATIN1 COLLATE LATIN1_SWEDISH_CI;

USE Company;

CREATE TABLE employee (
	fname VARCHAR(10) NOT NULL, 
	minit CHAR,
	lname VARCHAR(20) NOT NULL,
	ssn CHAR(9) NOT NULL,
	bdate DATE,
	address VARCHAR(40),
	sex CHAR(1),
	salary DECIMAL(5),
	super_ssn CHAR(9),
	dno INT NOT NULL, 
PRIMARY KEY (ssn)) ENGINE = INNODB;

CREATE TABLE department (
	dname VARCHAR(15) NOT NULL,
	dnumber INT NOT NULL,
	mgr_ssn CHAR(9) NOT NULL, 
	mgr_start_date DATE,
PRIMARY KEY (dnumber),
UNIQUE (dname),
FOREIGN KEY (mgr_ssn) REFERENCES employee(ssn)) ENGINE = INNODB;

CREATE TABLE dept_locations (
	dnumber INT NOT NULL,
	dlocation VARCHAR(15) NOT NULL, 
PRIMARY KEY(dnumber, dlocation),
FOREIGN KEY (dnumber) REFERENCES department (dnumber)) ENGINE=INNODB;

CREATE TABLE project(
    pname VARCHAR(15) NOT NULL,
    pnumber INT NOT NULL,
    plocation VARCHAR(15),
    dnum INT NOT NULL,
    PRIMARY KEY (pnumber),
    UNIQUE (pname),
    FOREIGN KEY (dnum) REFERENCES department (dnumber)
)ENGINE = INNODB;

CREATE TABLE works_on(
    essn CHAR(9) NOT NULL,
    pno INT NOT NULL,
    hours DECIMAL(3,1) NOT NULL,
    PRIMARY KEY (essn, pno),
    FOREIGN KEY (essn) REFERENCES employee(ssn),
    FOREIGN KEY (pno) REFERENCES project(pnumber)
)ENGINE = INNODB;

CREATE TABLE dependent (
	essn CHAR(9) NOT NULL, 
	dependent_name VARCHAR(15) NOT NULL,
	sex CHAR, 
	bdate DATE,
	relationship VARCHAR(8),
PRIMARY KEY (essn, dependent_name),
FOREIGN KEY (essn) REFERENCES employee(ssn)) ENGINE = INNODB;

INSERT INTO employee VALUES
	('John','B','Smith',123456789,'1985-01-09','731 Fondren, Houston, TX','M',30000,333445555,5),
	('Franklin','T','Wong',333445555,'1986-12-08','638 Voss, Houston TX','M',40000,888665555,5),
	('Alicia','J','Zelaya',999887777,' 1988-01-19','3321 Castle, Spring TX','F',25000,987654321,4), 
	('Jennifer','S','Wa11ace',987654321,'1991-06-20','291 Berry, Bellaire TX','F',43000,888665555,4), 
	('Ramesh','K','Narayan',666884444,'1990-09-15','975 Fire Oak, Humble TX','M',38000,333445555,5), 
	('Joyce','A','Eng1ish',453453453,'1992-07-31','5631 Rice, Houston TX','F',25000,333445555,5), 
	('Ahmad','V','Jabbar',987987987,' 1999-03-29','980 Dallas, Houston TX','M',25000,987654321,4), 
	('James','E','Borg',888665555,'1997-11-10','450 Stone, Houston TX','M',55000,null,1);

INSERT INTO department VALUES
	('Research',5,333445555,'1998-05-22'),
	('Administration',4,987654321,' 1998-01-01'), 
	('Headquarters',1,888665555,'1997-06-19');

INSERT INTO project VALUES
	('ProductX',1,'Bellaire',5),
	('ProductY',2,'Sugarland',5),
	('ProductZ',3,'Houston',5), 
	('Computerisation', 10,'Stafford',4), 
	('Reorganization',20,'Houston',1), 
	('Newbenefits',30,'Stafford',4);

INSERT INTO works_on Values
	(123456789,1,32.5),
	(123456789,2,7.5),
	(666884444,3,40.0),
	(453453453, 1,20.0),
	(453453453,2,20.0),
	(333445555,2,10.0),
	(333445555,3,10.0),
	(333445555, 10,10.0),
	(333445555,20,10.0),
	(999887777,30,30.0),
	(999887777,10,10.0),
	(987987987,10,35.0),
	(987987987,30,5.0),
	(987654321,30,20.0),
	(987654321,20,15.0),
	(888665555,20,16.0);

INSERT INTO dependent VALUES
	(333445555,'A1ice','F','2010-04-04','Daughter'),
	(333445555,'Theodore','M','2011-10-25','Son'),
	(333445555,'Joy','F','1995-05-03','Spouse'),
	(987654321,'Abner','M','1996-02-28','Spouse'),
	(123456789,'Michael','M','2014-01-04','Son'),
	(123456789,'A1ice','F','2010-12-30','Daughter'),
	(123456789,'Elizabeth','F','1997-05-05','Spouse');

INSERT INTO dept_locations VALUES
	(1,'Houston'),
	(4,'Stafford'),
	(5,'Be1laire'),
	(5,'Sugarland'),
	(5,'Houston');

ALTER TABLE department
	ADD CONSTRAINT dep_emp FOREIGN KEY (mgr_ssn) references employee(ssn);

ALTER TABLE employee
	ADD CONSTRAINT emp_emp FOREIGN KEY (super_ssn) references employee(ssn);

ALTER TABLE employee
	ADD CONSTRAINT emp_dno FOREIGN KEY (dno) references department(dnumber);
	
INSERT INTO employee VALUES
    ('Robert', 'F', 'Scott', 943775543, '1972-06-21', '2365 Newcastle Rd,
    Bellaire, TX', 'M', 58000, 888665555, 1);

INSERT INTO department VALUES
    ('Production', 3, 943775543, '2007-10-01');

INSERT INTO project VALUES
    ('ProductA', 5, 'Bellaire', 3);

INSERT INTO works_on VALUES
    (943775543, 5, 40.0);

INSERT INTO dependent VALUES
    ('453453453', 'John', 'M', '1990-12-12', 'spouse');

UPDATE department SET Mgr_ssn = 123456789, Mgr_start_date = '2007-10-01' 
WHERE Dnumber = 5;

UPDATE employee SET Super_ssn = 943775543 WHERE Super_ssn = 999887777; 

UPDATE works_on SET Hours = 5.0 WHERE essn = 999887777 AND pno = 10;

«««««««««««««««««««««QUERYS«««««««««««««««««««««««««««««
«««««««««««««««««««««QUERYS«««««««««««««««««««««««««««««
«««««««««««««««««««««QUERYS«««««««««««««««««««««««««««««


/*Retrieve the name and address of all workers in the department 'Research'*/

SELECT Fname,Lname,Address FROM employee, department WHERE Dname='Research' AND Dnumber=Dno;
+----------+---------+--------------------------+
| Fname    | Lname   | Address                  |
+----------+---------+--------------------------+
| John     | Smith   | 731 Fondren, Houston, TX |
| John     | Smith   | 731 Fondren, Houston, TX |
| Franklin | Wong    | 638 Voss, Houston TX     |
| Franklin | Wong    | 638 Voss, Houston TX     |
| Joyce    | Eng1ish | 5631 Rice, Houston TX    |
| Joyce    | Eng1ish | 5631 Rice, Houston TX    |
| Ramesh   | Narayan | 975 Fire Oak, Humble TX  |
| Ramesh   | Narayan | 975 Fire Oak, Humble TX  |
+----------+---------+--------------------------+
8 rows in set (0.001 sec)


/*  For each Project located in 'Stafford', list the project numbers, 191 the controlling 
department number and the manager's department number, 
show the last name, 192 address and birth date */. 

 SELECT pnumber,dnum,lname, address, bdate
    -> FROM project, department, employee
    -> WHERE dnum=dnumber AND mgr_ssn=ssn AND plocation='Stafford';
+---------+------+---------+------------------------+------------+
| pnumber | dnum | lname   | address                | bdate      |
+---------+------+---------+------------------------+------------+
|      10 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
|      30 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
|      10 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
|      30 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
+---------+------+---------+------------------------+------------+
4 rows in set (0.002 sec)


//Show the Name and the address from all employee that work in Research Department
SELECT Fname, Lname, Address FROM employee, department WHERE Dname='Research';
+----------+---------+--------------------------+
| Fname    | Lname   | Address                  |
+----------+---------+--------------------------+
| John     | Smith   | 731 Fondren, Houston, TX |
| John     | Smith   | 731 Fondren, Houston, TX |
| Franklin | Wong    | 638 Voss, Houston TX     |
| Franklin | Wong    | 638 Voss, Houston TX     |
| Joyce    | Eng1ish | 5631 Rice, Houston TX    |
| Joyce    | Eng1ish | 5631 Rice, Houston TX    |
| Ramesh   | Narayan | 975 Fire Oak, Humble TX  |
| Ramesh   | Narayan | 975 Fire Oak, Humble TX  |
| James    | Borg    | 450 Stone, Houston TX    |
| James    | Borg    | 450 Stone, Houston TX    |
| Jennifer | Wa11ace | 291 Berry, Bellaire TX   |
| Jennifer | Wa11ace | 291 Berry, Bellaire TX   |
| Ahmad    | Jabbar  | 980 Dallas, Houston TX   |
| Ahmad    | Jabbar  | 980 Dallas, Houston TX   |
| Alicia   | Zelaya  | 3321 Castle, Spring TX   |
| Alicia   | Zelaya  | 3321 Castle, Spring TX   |
+----------+---------+--------------------------+
16 rows in set (0.001 sec)


SELECT Pnumber,Dnum, Lname, Address, Bdate FROM project,department, 
employee WHERE Dnum=Dnumber AND Mgr_ssn=Ssn AND Plocation='Stafford';
+---------+------+---------+------------------------+------------+
| Pnumber | Dnum | Lname   | Address                | Bdate      |
+---------+------+---------+------------------------+------------+
|      10 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
|      30 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
|      10 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
|      30 |    4 | Wa11ace | 291 Berry, Bellaire TX | 1991-06-20 |
+---------+------+---------+------------------------+------------+
4 rows in set (0.001 sec)

/* "Regex" 

SELECT Fname,Lname, bdate FROM employee WHERE bdate LIKE '_%8%';
+----------+--------+------------+
| Fname    | Lname  | bdate      |
+----------+--------+------------+
| John     | Smith  | 1985-01-09 |
| Franklin | Wong   | 1986-12-08 |
| Alicia   | Zelaya | 1988-01-19 |
+----------+--------+------------+
3 rows in set (0.072 sec)


SELECT Fname, Lname FROM employee WHERE bdate LIKE '__%8%';
+----------+--------+
| Fname    | Lname  |
+----------+--------+
| John     | Smith  |
| Franklin | Wong   |
| Alicia   | Zelaya |
+----------+--------+
3 rows in set (0.002 sec)

/*show how many people were born in January

SELECT Fname, Lname,bdate FROM employee WHERE bdate LIKE '%01%';
+--------+--------+------------+
| Fname  | Lname  | bdate      |
+--------+--------+------------+
| John   | Smith  | 1985-01-09 |
| Alicia | Zelaya | 1988-01-19 |
+--------+--------+------------+
2 rows in set (0.001 sec)


/* OR */ 


+--------+--------+------------+
| Fname  | Lname  | bdate      |
+--------+--------+------------+
| John   | Smith  | 1985-01-09 |
| Alicia | Zelaya | 1988-01-19 |
+--------+--------+------------+
2 rows in set (0.001 sec)


SELECT Fname, Lname, salary, bdate FROM employee WHERE salary LIKE '55%';
+-------+-------+----------+------------+
| Fname | Lname | salary   | bdate      |
+-------+-------+----------+------------+
| James | Borg  | 55000.00 | 1997-11-10 |
+-------+-------+----------+------------+
1 row in set (0.009 sec)



SELECT Fname, Lname, salary, bdate FROM employee WHERE salary LIKE '%000%';
+----------+---------+----------+------------+
| Fname    | Lname   | salary   | bdate      |
+----------+---------+----------+------------+
| John     | Smith   | 30000.00 | 1985-01-09 |
| Franklin | Wong    | 40000.00 | 1986-12-08 |
| Joyce    | Eng1ish | 25000.00 | 1992-07-31 |
| Ramesh   | Narayan | 38000.00 | 1990-09-15 |
| James    | Borg    | 55000.00 | 1997-11-10 |
| Jennifer | Wa11ace | 43000.00 | 1991-06-20 |
| Ahmad    | Jabbar  | 25000.00 | 1999-03-29 |
| Alicia   | Zelaya  | 25000.00 | 1988-01-19 |
+----------+---------+----------+------------+
8 rows in set (0.001 sec)


//MOSTRAR OS EMPLOYEES QUE O SALARIO ACABA EM .00 
SELECT Fname, Lname, salary, bdate FROM employee WHERE salary LIKE '%000%';
+----------+---------+----------+------------+
| Fname    | Lname   | salary   | bdate      |
+----------+---------+----------+------------+
| John     | Smith   | 30000.00 | 1985-01-09 |
| Franklin | Wong    | 40000.00 | 1986-12-08 |
| Joyce    | Eng1ish | 25000.00 | 1992-07-31 |
| Ramesh   | Narayan | 38000.00 | 1990-09-15 |
| James    | Borg    | 55000.00 | 1997-11-10 |
| Jennifer | Wa11ace | 43000.00 | 1991-06-20 |
| Ahmad    | Jabbar  | 25000.00 | 1999-03-29 |
| Alicia   | Zelaya  | 25000.00 | 1988-01-19 |
+----------+---------+----------+------------+
8 rows in set (0.001 sec)


//Mostrar todos 

 SELECT Fname,Lname,address,bdate FROM employee WHERE address REGEXP '[H][o]';
+----------+---------+--------------------------+------------+
| Fname    | Lname   | address                  | bdate      |
+----------+---------+--------------------------+------------+
| John     | Smith   | 731 Fondren, Houston, TX | 1985-01-09 |
| Franklin | Wong    | 638 Voss, Houston TX     | 1986-12-08 |
| Joyce    | Eng1ish | 5631 Rice, Houston TX    | 1992-07-31 |
| James    | Borg    | 450 Stone, Houston TX    | 1997-11-10 |
| Ahmad    | Jabbar  | 980 Dallas, Houston TX   | 1999-03-29 |
+----------+---------+--------------------------+------------+
5 rows in set (0.001 sec)

/////////////////
a expressão chama numero começado por 4 ou começado por 2ou5
////////////////

select fname, lname, bdate, salary
    -> from employee
    -> where salary REGEXP '^[40]+'
    -> OR salary REGEXP '^[25]+'
    -> order by salary;
+----------+---------+------------+----------+
| fname    | lname   | bdate      | salary   |
+----------+---------+------------+----------+
| Joyce    | Eng1ish | 1992-07-31 | 25000.01 |
| Ahmad    | Jabbar  | 1999-03-29 | 25000.01 |
| Alicia   | Zelaya  | 1988-01-19 | 25000.01 |
| Franklin | Wong    | 1986-12-08 | 40000.00 |
| Jennifer | Wa11ace | 1991-06-20 | 43000.00 |
| James    | Borg    | 1997-11-10 | 55000.00 |
+----------+---------+------------+----------+
6 rows in set (0.436 sec)


////////////ou/////////////////

select fname,bdate, salary from employee where salary REGEXP '^[40]+' order by salary;
+----------+------------+----------+
| fname    | bdate      | salary   |
+----------+------------+----------+
| Franklin | 1986-12-08 | 40000.00 |
| Jennifer | 1991-06-20 | 43000.00 |
+----------+------------+----------+
2 rows in set (0.001 sec)


select fname,bdate, salary from employee where salary REGEXP '^[40]+' order by salary;
+----------+------------+----------+
| fname    | bdate      | salary   |
+----------+------------+----------+
| Franklin | 1986-12-08 | 40000.00 |
| Jennifer | 1991-06-20 | 43000.00 |
+----------+------------+----------+
2 rows in set (0.001 sec)

================================================

DEPOIS DE INSERIR os DADOS DA TABELA WORK_ON_NFO

====================================
select emp_name, sum (hours_per_week)
from works_on_info
where emp_name='Narayan'; 

===================================
select emp_name, sum(hours_per_week) 
from works_on_info 
where emp_name='Wong' 
group by emp_name; 



MariaDB [company]> select fname, lname, dname, pname, hours
    -> from employee e, department d, project p, works_on w
    -> where e.ssn = w.essn and w.pno= p.number and e.dno= d.number
    -> and w.hours > 10
    -> and pname='Project X'
    -> order by w.hours;

MariaDB [company]> select Ssn, fname, lname, super_ssn from employee;
+-----------+----------+---------+-----------+
| Ssn       | fname    | lname   | super_ssn |
+-----------+----------+---------+-----------+
| 123456789 | John     | Smith   | 333445555 |
| 333445555 | Franklin | Wong    | 888665555 |
| 453453453 | Joyce    | Eng1ish | 333445555 |
| 653298653 | Richard  | Marini  | 333445555 |
| 666884444 | Ramesh   | Narayan | 333445555 |
| 888665555 | James    | Borg    | NULL      |
| 987654321 | Jennifer | Wa11ace | 888665555 |
| 987987987 | Ahmad    | Jabbar  | 987654321 |
| 999887777 | Alicia   | Zelaya  | 987654321 |
+-----------+----------+---------+-----------+
9 rows in set (0.002 sec)


/////update ssn 
MariaDB [company]> update employee set super_ssn = '333445555' where Ssn='653298653';
Query OK, 0 rows affected (0.001 sec)
Rows matched: 1  Changed: 0  Warnings: 0

MariaDB [company]> select * from dependent;
+-----------+----------------+------+------------+--------------+
| Essn      | Dependent_name | Sex  | Bdate      | Relationship |
+-----------+----------------+------+------------+--------------+
| 123456789 | A1ice          | F    | 2010-12-30 | Daughter     |
| 123456789 | Elizabeth      | F    | 1997-05-05 | Spouse       |
| 123456789 | Michael        | M    | 2014-01-04 | Son          |
| 333445555 | A1ice          | F    | 2010-04-04 | Daughter     |
| 333445555 | Joy            | F    | 1995-05-03 | Spouse       |
| 333445555 | Theodore       | M    | 2011-10-25 | Son          |
| 453453453 | John           | M    | 1990-12-12 | spouse       |
| 987654321 | Abner          | M    | 1996-02-28 | Spouse       |
+-----------+----------------+------+------------+--------------+
8 rows in set (0.023 sec)

MariaDB [company]> insert into dependent values (653298653,'Richard','M','1986-04-13','Son');
Query OK, 1 row affected (0.003 sec)

exe. 4.10 
b) 
MariaDB [company]> select CONCAT (fname,' ', lname) AS Parent, CONCAT (dependent_name, ' ', lname,' ', "(Junior)") AS Dependet from employee, dependent where ssn=essn and fname=dependent_name;
+----------------+-------------------------+
| Parent         | Dependet                |
+----------------+-------------------------+
| Richard Marini | Richard Marini (Junior) |
+----------------+-------------------------+
1 row in set (0.034 sec)


exe. 4.10 
c) 
(nao sei se esta certo) 
MariaDB [company]> select fname from employee where super_ssn= 333445555;
+---------+
| fname   |
+---------+
| John    |
| Joyce   |
| Richard |
| Ramesh  |
+---------+
4 rows in set (0.081 sec)

exe. 4.11

MariaDB [company]> select concat (fname, ' ', lname) Empregados, (select fname from employee where lname='wong') Spervisor from employee e
    -> where e.super_ssn = (select ssn from employee where lname='wong');
+----------------+-----------+
| Empregados     | Spervisor |
+----------------+-----------+
| John Smith     | Franklin  |
| Joyce Eng1ish  | Franklin  |
| Richard Marini | Franklin  |
| Ramesh Narayan | Franklin  |
+----------------+-----------+
4 rows in set (0.418 sec)

//////ou//////

select concat (fname, ' ', lname) Empregados,\
    -> ("wong") Supervisor
    -> from employee
    -> where super_ssn=(select ssn from employee where lname="wong");
+----------------+------------+
| Empregados     | Supervisor |
+----------------+------------+
| John Smith     | wong       |
| Joyce Eng1ish  | wong       |
| Richard Marini | wong       |
| Ramesh Narayan | wong       |
+----------------+------------+
4 rows in set (0.002 sec)

4.11. 
 select concat (fname,' ',minit,' ',lname)  AS "Borg´s direct staff"
    -> from employee
    -> where super_ssn=(select ssn from employee where lname="Borg");
+----------------------+
| Borg´s direct staff  |
+----------------------+
| Franklin T Wong      |
| Jennifer S Wa11ace   |
+----------------------+
2 rows in set (0.002 sec)

//// count command /////
select fname,lname,(select count(*),0,'-' from dependent where ssn=essn) as "Dependents" from employee order by 3;
+----------+---------+------------+
| fname    | lname   | Dependents |
+----------+---------+------------+
| Ramesh   | Narayan |          0 |
| James    | Borg    |          0 |
| Ahmad    | Jabbar  |          0 |
| Alicia   | Zelaya  |          0 |
| Joyce    | Eng1ish |          1 |
| Richard  | Marini  |          1 |
| Jennifer | Wa11ace |          1 |
| John     | Smith   |          3 |
| Franklin | Wong    |          3 |
+----------+---------+------------+
9 rows in set (0.064 sec)

//// replace command /////

select fname,lname, (select REPLACE(count(*),0,'-')
    from dependent
    where ssn = essn) as "Dependents"
    from employee
    order by 3;
+----------+---------+------------+
| fname    | lname   | Dependents |
+----------+---------+------------+
| Ramesh   | Narayan | -          |
| James    | Borg    | -          |
| Ahmad    | Jabbar  | -          |
| Alicia   | Zelaya  | -          |
| Joyce    | Eng1ish | 1          |
| Richard  | Marini  | 1          |
| Jennifer | Wa11ace | 1          |
| John     | Smith   | 3          |
| Franklin | Wong    | 3          |
+----------+---------+------------+
9 rows in set (0.079 sec)


///having comand///

 select lname, count(*) from employee, dependent where ssn=essn group by lname having count(*) >0;
+---------+----------+
| lname   | count(*) |
+---------+----------+
| Eng1ish |        1 |
| Marini  |        1 |
| Smith   |        3 |
| Wa11ace |        1 |
| Wong    |        3 |
+---------+----------+
5 rows in set (0.002 sec)


Q18. retrive the names of all employees who do not have supervisors.
///// is null /////

select fname,lname from employee where super_ssn is null;
+-------+-------+
| fname | lname |
+-------+-------+
| James | Borg  |
+-------+-------+
1 row in set (0.001 sec)

/// retrive all empolyees with no supervisor //// 

select concat(fname,' ',lname) "No Supervisor", super_ssn from employee where super_ssn is null;
+---------------+-----------+
| No Supervisor | super_ssn |
+---------------+-----------+
| James Borg    | NULL      |
+---------------+-----------+
1 row in set (0.001 sec)





Thanks for your time!! Enjoy 
