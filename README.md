# Sql-Server-Practice-2024
This Practice baseed on Sql Server Version 2022 or earlier versions
I'll  try to cover Complete Sql Server Workflow Practice



![sql Operatopns](https://github.com/orbitrover/Sql-Practice-2024/assets/8413437/bc669a0e-4ac0-4259-ae45-0d78e53e3106)

    ---DDL
    Create Database SampleDB;
    
    --DDL
    ---Run This Command if multiple use is accessing the same database and drop common refuse the droping DB
    Alter Database SampleDB Set SINGLE_USER With Rollback Immediate
    
    ---DDL
    ---Use For Drop Database
    Drop Database SampleDB;
    
    Use EmployeeDB
    Go
    
    --DDL
    --Drop Table Employee
    Create Table Employee
    (
    Id int primary key identity(1,1),
    FirstName varchar(60),
    LastName varchar(30),
    Salary numeric(10,2),
    Mobile char(10),
    Email nvarchar(200)
    )
    
    --SET IDENTITY_INSERT [dbo].[Employee] ON 
    --DML
    insert into Employee ( [FirstName], [LastName], [Salary], [Mobile], [Email])
    Values('Orbit', 'Rover', 9000, '7089256777', 'orbitrover@gmail.com')
    ,('Pushpendra', 'Singh',11500, '7089256777', 'orbitrover@gmail.com')
    ,('Himani', null,7500, '7089256777', 'orbitrover@gmail.com')
    ,('Laxmi', 'Rai',15420, '7089256777', 'orbitrover@gmail.com')
    ,('Alex', 'Jack',8500, '7089256777', 'orbitrover@gmail.com')
    --SET IDENTITY_INSERT [dbo].[Employee] Off
    
    --DML
    insert into Employee ( [FirstName], [LastName], [Salary], [Mobile], [Email])
    Values('Nion', 'Tesla', 6790, '7089256777', 'orbitrover@gmail.com')
    ,('Rocky', 'Rabbit',5500, '7089256777', 'orbitrover@gmail.com')
    
    
    --DML
    insert into Employee
    Values('Bear', 'Bro', 12300, '7089256777', 'orbitrover@gmail.com')
    ,('Lazy', 'Lion',14600, '7089256777', 'orbitrover@gmail.com')
    
    ---DML
    Select * from Employee;
    
    Select Id, FirstName+' '+LastName as EmployeeName 
    ,Case When Salary > 14000 Then 'Manager' Else
    Case When Salary > 10000 and Salary < 14000 Then 'Developer' Else 'Clearks' End
    End as Designation
    from Employee;
    
    Select * from Employee Where Id > 6;
    
    Select * from Employee Where FirstName Like '%a%'; ---Full Search in Given Text
    Select * from Employee Where FirstName Like 'pu%'; ---find any values that start with “a”
    Select * from Employee Where FirstName Like '%a'; ---find any values that ends with “a”
    Select * from Employee Where FirstName Like '_a%';---find any values that have “a” in the second position
    Select * from Employee Where FirstName Like '%a_';---find any values that have “a” in the second position in the last
    Select * from Employee Where FirstName Like 'a_%_%';---ind any values that start with “a” and are at least 3 characters in length
    Select * from Employee Where FirstName Like '[a-c]%'; ---ind any values starting with “a”, “b”, or “c”
    Select * from Employee Where FirstName Like '[aeiou]%';---Find any values that start with given vovels
    Select * from Employee Where FirstName Like '[al]%';---Find any values that start with given vovels
    Select * from Employee Where FirstName Like '%[aeiou]';---Find any values that ends with given vovels
    Select * from Employee Where FirstName Like '[aeiou]%[aeiou]';---Find any values that start and ends with given vovels
    
    --DDL
    --Drop Table EmployeeAttendance
    Create Table EmployeeAttendance
    (
    EmployeeId int,
    CheckinDateTime datetime default GETDATE(),
    CheckoutDateTime datetime  default GETDATE(),
    )
    Insert into EmployeeAttendance(EmployeeId, IsHalfDay)
    Values(5, 'Yes')
    ,(2)
    ,(3)
    
    Select * from EmployeeAttendance;
    
    ---DDL
    Alter Table EmployeeAttendance
    Drop Column IsHalfDay
    
    Alter Table EmployeeAttendance
    Add IsHalfDay bit default 0
    
    EXEC sp_rename 'dbo.EmployeeAttendance.IsHalfDay', 'IsHalfDays', 'COLUMN';
