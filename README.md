CREATE DATABASE TourBookingDb;
GO

USE TourBookingDb;
GO

CREATE TABLE Tours (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    Name NVARCHAR(255) NOT NULL,
    Price DECIMAL(18,2) NOT NULL CHECK (Price >= 0),
    Duration INT NOT NULL CHECK (Duration BETWEEN 1 AND 30),
    Description NVARCHAR(1000) NULL
);
GO

CREATE TABLE Bookings (
    Id INT IDENTITY(1,1) PRIMARY KEY,
    BookingDate DATETIME NOT NULL DEFAULT GETDATE(),
    CustomerName NVARCHAR(100) NOT NULL,
    CustomerEmail NVARCHAR(100) NOT NULL,
    TourId INT NOT NULL,
    NumberOfPeople INT NOT NULL CHECK (NumberOfPeople >= 1),
    CONSTRAINT FK_Bookings_Tours FOREIGN KEY (TourId)
        REFERENCES Tours(Id)
        ON DELETE CASCADE
);
GO
