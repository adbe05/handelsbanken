# Keys

*Purpose: intro to "keys". See the difference when keys are used or not*

## Create

Create a new database

## Exercise: color table

Create a table "Color" with the columns:
- Id
- Name

Solution

	create table Color(
		Id int, 
		Name varchar(50),
	)

## Exercise: person table

Create a table "Person" with:
- Name
- FavoriteColorId 

Solution

	create table Person(
		Name varchar(50),
		FavoriteColorId int 
	)

## Exercise: add colors

Add the following colors:
- 91 Red
- 92 Green
- 93 Blue
- 94 Purple
- 95 Indigo

Solution

	insert into Color 
	values
	(91, 'Red'),
	(92, 'Green'),
	(93, 'Blue'),
	(94, 'Purple'),
	(95, 'Indigo')

## Exercise: add people

Add this people:
- Mia likes Red
- James likes Green
- Liam likes Blue

Solution

	insert into Person
	values
	('Mia', 91),
	('James', 92),
	('Liam', 93)

## Exercise: add yellow

List all content form the tables

	select * from Color
	select * from Person

Add the color Yellow with Id=91:

	insert into Color values (91, 'Yellow');

What's the problem with the data now?

Solution:

	Now it's not cleared what the color with Id=91 is. Is it red or yellow? Not good.

## Exercise: add Joe

Add Joe:

	insert into Person values ('Joe', 666666);

What's the problem with the data now?

Solution

	Joe like the color 666666, but what color is that?
	No one knows...

## Recreate with keys

Create a new database and start to use a **primary key** and **foreign key**

Create a new database

Add the following two tables with data:

	create table Color(
		Id int primary key, --- new!
		Name varchar(50),
	)

	create table Person(
		Name varchar(50),
		FavoriteColor int foreign key references Color(Id), --- new!
	)

	insert into Color 
	values
	(91, 'Red'),
	(92, 'Green'),
	(93, 'Blue'),
	(94, 'Purple'),
	(95, 'Indigo')

	insert into Person
	values
	('Mia', 91),
	('James', 92),
	('Liam', 93)


## Exercise: add yellow

Try to add "Yellow" with Id 91

What happens? 

Solution

	insert into Color values (91, 'Yellow');

	We get this

		Violation of PRIMARY KEY constraint 'PK__Color__3214EC0773BC1B85'. Cannot insert duplicate key in object 'dbo.Color'. The duplicate key value is (91).

	Problem solved! This is not allowed anymore because of out "primary key" above. Good!

	If you now run 

		select * from Color

	...you see that the color Yellow wasn't inserted (good)

## Exercise: add Joe

Try to add the person
- Joe 666666

What happens? Good/bad?

Solution

	insert into Person values ('Joe', 666666);

	We get

		The INSERT statement conflicted with the FOREIGN KEY constraint "FK__Person__Favorite__37A5467C". The conflict occurred in database "Demo", table "dbo.Color", column 'Id'.

	Problem solved! This is now allowed anymore because of out "foreign key" above. Good!
