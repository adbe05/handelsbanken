# Stored procedures

A stored procedure is a prepared SQL code that you can save, so the code can be reused over and over again.

So if you have an SQL query that you write over and over again, save it as a stored procedure, and then just call it to execute it.

You can also pass parameters to a stored procedure, so that the stored procedure can act based on the parameter value(s) that is passed.

References:
- https://www.w3schools.com/sql/sql_stored_procedures.asp

Execute

	create table Person(
		Name varchar(50),
		Country varchar(50),
		Income int
	)

Add some people

	insert into Person
	values
	('Mia', 'Sweden', 20000),
	('Olivia', 'Iceland', 50000),
	('James', 'Sweden', 25000),
	('Liam',	'Sweden', 28000),
	('Ava',	'Iceland', 60000),
	('Lisa', 'Spain', 10000)

	select * from Person

## Stored procedure

Run this query

	select * 
	from Person 
	where Country='Iceland'   

Create a stored procedure named *GetAllFromIceland* that execute the query above.

	create proc GetAllFromIceland
	as
	begin
		select * 
		from Person 
		where Country='Iceland'  
	end


## Run

Run the stored procedure

	exec GetAllFromIceland	

## Exercise: create again

Try to create the stored procedure again. What happens?

Solution:

	There is already an object named 'GetAllFromIceland' in the database.

## Exercise: modify procedure

Modify the stored procedure so it only show the names in Iceland

Hint: look for "ALTER"

Solution

	alter proc GetAllFromIceland
	as
	begin
		select Name
		from Person 
		where Country='Iceland'
	end

## Create or modify

If your not sure if the procedure exist or not, you can run this:

	create or alter proc GetAllFromIceland
	as
	begin
		select Name
		from Person 
		where Country='Iceland'
	end

	
## Exercise

Create a stored procedure that takes two parameters and look something like this

	create or alter proc GetPeopleWithFilter .......
	as
	begin
		select *
		from Person 
		where Country=@country and Income>=@minincome
	end

Detail: you don't need "begin" and "end"

Solution

	create or alter proc GetPeopleWithFilter @country varchar(50), @minincome int
	as
	begin
		select *
		from Person 
		where Country=@country and Income>=@minincome
	end

# Exercise

Call the stored procedure to get people living in Sweden with a salary higher than 2500

Expected:

	James	Sweden	25000
	Liam	Sweden	28000

Hint: 

	exec ............

Solution

	exec GetPeopleWithFilter 'Sweden', 25000  --James and Liam

# Details

It's not possible to create two stored procedures with the same name (even if they have different parameters)
