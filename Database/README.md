# Car Finder Database
## Phyical Database Design

![Physical Relationship Diagram](CarFinderERD.png)

```
----------------Create the Database----------------

USE master;
GO

DROP DATABASE IF EXISTS CarFinderDb;
GO

CREATE DATABASE CarFinderDb;
GO

USE CarFinderDb;
GO

----------------Create the Tables----------------

CREATE TABLE Buyers
(
	buyerid		INT			IDENTITY(1,1)	NOT NULL,
	email		NVARCHAR(40)				NOT NULL,
	username	NVARCHAR(30)				NOT NULL,
	password	NVARCHAR(40)				NOT NULL,
	address		NVARCHAR(50)				NULL,
	city		NVARCHAR(20)				NOT NULL,
	state		NVARCHAR(5)				NOT NULL,
	zipcode		INT					NOT NULL,
	phonenumber NVARCHAR(15)				NULL,
	CONSTRAINT PK_Buyers PRIMARY KEY (buyerid),
	CONSTRAINT UC_Email UNIQUE (email)
);
GO

CREATE TABLE Sellers
(
	sellerid	INT			IDENTITY(1,1)	NOT NULL,
	email		NVARCHAR(40)				NOT NULL,
	username	NVARCHAR(30)				NOT NULL,
	password	NVARCHAR(40)				NOT NULL,
	address		NVARCHAR(50)				NULL,
	city		NVARCHAR(20)				NOT NULL,
	state		NVARCHAR(5)				NOT NULL,
	zipcode		INT					NOT NULL,
	phonenumber NVARCHAR(15)				NOT NULL,
	vehicleid	INT					NULL,
	CONSTRAINT PK_Sellers PRIMARY KEY (sellerid),
	CONSTRAINT UC_Email2 UNIQUE (email)
);
GO

CREATE TABLE Buyers_Sellers
(
	buyerid		INT		NULL,
	sellerid	INT		NULL,
	CONSTRAINT FK_Buyers_Sellers_Buyers FOREIGN KEY (buyerid)
		REFERENCES Sellers(sellerid),
	CONSTRAINT FK_Buyers_Sellers_Sellers FOREIGN KEY (sellerid)
	REFERENCES Buyers(buyerid)
);
GO

CREATE TABLE Vehicles
(
	vehicleid		INT			IDENTITY(1,1)	NOT NULL,
	VIN				NVARCHAR(20)			NOT NULL,
	listeddate		DATE					NOT NULL,
	saveddate		DATE					NULL,
	condition		NVARCHAR(10)				NULL,
	year			INT					NULL,
	make			NVARCHAR(20)				NULL,
	model			NVARCHAR(30)				NULL,
	bodytype		NVARCHAR(15)				NULL,
	color			NVARCHAR(10)				NULL,
	price			INT					NULL,
	mileage			INT					NULL,
	transmission	NVARCHAR(10)					NULL,
	drivetrain		NVARCHAR(10)				NULL,
	fueltype		NVARCHAR(10)				NULL,
	fueleconomy		INT					NULL,
	cylinders		INT					NULL,
	doors			INT					NULL,
	sellerid		INT					NOT NULL,
	CONSTRAINT PK_Vehicles PRIMARY KEY (vehicleid)
);
GO

CREATE TABLE Buyers_Vehicles
(
	buyerid		INT		NULL,
	vehicleid	INT		NULL,
	CONSTRAINT FK_Buyers_Vehicles_Buyers FOREIGN KEY (buyerid)
		REFERENCES Vehicles(vehicleid),
	CONSTRAINT FK_Buyers_Vehicles_Vehicles FOREIGN KEY (vehicleid)
	REFERENCES Buyers(buyerid)
);
GO
```
