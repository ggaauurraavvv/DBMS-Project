# DBMS-Project
create database project2;
use project2;
CREATE TABLE Users (
    UserID INT PRIMARY KEY,
    FirstName VARCHAR(50) NOT NULL,
    LastName VARCHAR(50) NOT NULL,
    Email VARCHAR(100) UNIQUE NOT NULL,
    PhoneNumber VARCHAR(15) UNIQUE NOT NULL,
    UserType ENUM('Driver', 'Rider') NOT NULL
);

INSERT INTO Users (UserID, FirstName, LastName, Email, PhoneNumber, UserType)
VALUES
    (1, 'Aarav', 'Kumar', 'aarav.kumar@example.com', '9876543210', 'Driver'),
    (2, 'Aanya', 'Singh', 'aanya.singh@example.com', '8765432109', 'Rider'),
    (3, 'Vikram', 'Sharma', 'vikram.sharma@example.com', '7654321098', 'Driver'),
    (4, 'Neha', 'Gupta', 'neha.gupta@example.com', '6543210987', 'Rider'),
    (5, 'Sarika', 'Mishra', 'sarika.mishra@example.com', '5432109876', 'Driver'),
    (6, 'Neha', 'Verma', 'neha.verma@example.com', '4321098765', 'Rider'),
    (7, 'Rajesh', 'Yadav', 'rajesh.yadav@example.com', '3210987654', 'Driver'),
    (8, 'Preeti', 'Rajput', 'preeti.rajput@example.com', '2109876543', 'Rider'),
    (9, 'Vikas', 'Joshi', 'vikas.joshi@example.com', '1098765432', 'Driver'),
    (10, 'Shweta', 'Agrawal', 'shweta.agrawal@example.com', '0987654321', 'Rider'),
    (11, 'Amit', 'Singh', 'amit.singh@example.com', '9876543211', 'Driver'),
    (12, 'Anushka', 'Shukla', 'anushka.shukla@example.com', '8765432112', 'Rider'),
    (13, 'Varun', 'Gandhi', 'varun.gandhi@example.com', '7654321123', 'Driver'),
    (14, 'Aarti', 'Sharma', 'aarti.sharma@example.com', '6543211234', 'Rider'),
    (15, 'Sanjay', 'Kapoor', 'sanjay.kapoor@example.com', '5432112345', 'Driver'),
    (16, 'Meera', 'Malik', 'meera.malik@example.com', '4321123456', 'Rider'),
    (17, 'Rahul', 'Thakur', 'rahul.thakur@example.com', '3211234567', 'Driver'),
    (18, 'Asha', 'Jain', 'asha.jain@example.com', '2123456789', 'Rider'),
    (19, 'Vishal', 'Ahuja', 'vishal.ahuja@example.com', '1234567890', 'Driver'),
    (20, 'Sneha', 'Saxena', 'sneha.saxena@example.com', '2345678901', 'Rider');

CREATE TABLE Drivers (
    DriverID INT PRIMARY KEY,
    UserID INT UNIQUE NOT NULL,
    VehicleType VARCHAR(50) NOT NULL,
    LicensePlate VARCHAR(15) NOT NULL,
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);

INSERT INTO Drivers (DriverID, UserID, VehicleType, LicensePlate)
VALUES
    (1, 1, 'Sedan', 'MH1234AB'),
    (3, 3, 'SUV', 'KA5678CD'),
    (5, 5, 'Hatchback', 'DL9876EF'),
    (7, 7, 'Sedan', 'TN7654GH'),
    (9, 9, 'SUV', 'KL4321IJ'),
    (11, 11, 'Hatchback', 'GJ8765KL'),
    (13, 13, 'Sedan', 'PB7890CD'),
    (15, 15, 'SUV', 'RJ2345XY'),
    (17, 17, 'Hatchback', 'UP9876PQ'),
    (19, 19, 'Sedan', 'MP1234AB');

CREATE TABLE Riders (
    RiderID INT PRIMARY KEY,
    UserID INT UNIQUE NOT NULL,
    CreditCardNumber VARCHAR(16) NOT NULL,
    FOREIGN KEY (UserID) REFERENCES Users(UserID)
);
INSERT INTO Riders (RiderID, UserID, CreditCardNumber)
VALUES
    (2, 2, '1234567812345678'),
    (4, 4, '8765432187654321'),
    (6, 6, '9876543298765432'),
    (8, 8, '2345678923456789'),
    (10, 10, '3456789034567890'),
    (12, 12, '4567890145678901'),
    (14, 14, '5678901256789012'),
    (16, 16, '6789012367890123'),
    (18, 18, '7890123478901234'),
    (20, 20, '8901234589012345');
    
    CREATE TABLE Reviews (
    ReviewID INT PRIMARY KEY,
    RiderID INT NOT NULL,
    DriverID INT NOT NULL,
    Rating INT NOT NULL,
    Comment TEXT,
    FOREIGN KEY (RiderID) REFERENCES Riders(RiderID),
    FOREIGN KEY (DriverID) REFERENCES Drivers(DriverID)
);

INSERT INTO Reviews (ReviewID, RiderID, DriverID, Rating, Comment)
VALUES
    (1, 2, 1, 5, 'Great driver, excellent service!'),
    (2, 4, 3, 4, 'The ride was good, but a bit late.'),
    (3, 6, 5, 5, 'Superb experience, highly recommended!'),
    (4, 8, 7, 3, 'Average ride, can improve'),
    (5, 10, 9, 4, 'Nice ride, comfortable car'),
    (6, 12, 11, 5, 'Excellent driver, punctual'),
    (7, 14, 13, 3, 'Driver was okay, but the car was dirty'),
    (8, 16, 15, 4, 'Smooth ride, friendly driver'),
    (9, 18, 17, 5, 'Outstanding service, very professional'),
    (10, 20, 19, 2, 'Disappointing ride, driver was rude');
    

CREATE TABLE Rides (
    RideID INT PRIMARY KEY,
    DriverID INT NOT NULL,
    RiderID INT NOT NULL,
    PickupLocation VARCHAR(100) NOT NULL,
    Destination VARCHAR(100) NOT NULL,
    RideDate DATETIME NOT NULL,
    Fare DECIMAL(10, 2) NOT NULL,
    FOREIGN KEY (DriverID) REFERENCES Drivers(DriverID),
    FOREIGN KEY (RiderID) REFERENCES Riders(RiderID)
);

INSERT INTO Rides (RideID, DriverID, RiderID, PickupLocation, Destination, RideDate, Fare)
VALUES
    (1, 1, 2, 'Central Park', 'Times Square', '2023-10-30 08:00:00', 25.00),
    (2, 3, 4, 'Union Station', 'Museum of Art', '2023-10-30 09:00:00', 30.50),
    (3, 5, 6, 'Beachfront', 'Downtown', '2023-10-30 10:00:00', 15.75),
    (4, 7, 8, 'Airport', 'Hotel', '2023-10-30 11:00:00', 40.25),
    (5, 9, 10, 'City Center', 'Shopping Mall', '2023-10-30 12:00:00', 12.00),
    (6, 11, 12, 'Park Street', 'Zoo', '2023-10-30 13:00:00', 22.75),
    (7, 13, 14, 'Train Station', 'Restaurant', '2023-10-30 14:00:00', 18.50),
    (8, 15, 16, 'Suburb', 'Downtown', '2023-10-30 15:00:00', 35.00),
    (9, 17, 18, 'Mall', 'Cinema', '2023-10-30 16:00:00', 11.75),
    (10, 19, 20, 'Airport', 'Hotel', '2023-10-30 17:00:00', 40.75);
    INSERT INTO Rides (RideID, DriverID, RiderID, PickupLocation, Destination, RideDate, Fare)
VALUES
    (11, 3, 2, 'Downtown', 'Shopping Mall', '2023-10-31 10:00:00', 18.25),
    (12, 7, 2, 'Park Street', 'Zoo', '2023-10-31 11:00:00', 26.50),
    (13, 9, 2, 'Train Station', 'Restaurant', '2023-10-31 12:00:00', 16.75),
    (14, 1, 2, 'Suburb', 'Downtown', '2023-10-31 13:00:00', 33.00),
    (15, 11, 2, 'Mall', 'Cinema', '2023-10-31 14:00:00', 14.00),
    (16, 9, 2, 'Airport', 'Hotel', '2023-10-31 15:00:00', 36.75),
    (17, 7, 2, 'City Center', 'Times Square', '2023-10-31 16:00:00', 10.25);

    

    
CREATE TABLE Payments (
    PaymentID INT PRIMARY KEY,
    RiderID INT NOT NULL,
    RideID INT NOT NULL,
    PaymentAmount DECIMAL(10, 2) NOT NULL,
    PaymentDate DATETIME NOT NULL,
    FOREIGN KEY (RiderID) REFERENCES Riders(RiderID),
    FOREIGN KEY (RideID) REFERENCES Rides(RideID)
);
INSERT INTO Payments (PaymentID, RiderID, RideID, PaymentAmount, PaymentDate)
VALUES
    (1, 2, 1, 25.00, '2023-10-30 08:30:00'),
    (2, 4, 2, 30.50, '2023-10-30 09:30:00'),
    (3, 6, 3, 15.75, '2023-10-30 10:30:00'),
    (4, 8, 4, 40.25, '2023-10-30 11:30:00'),
    (5, 10, 5, 12.00, '2023-10-30 12:30:00'),
    (6, 12, 6, 22.75, '2023-10-30 13:30:00'),
    (7, 14, 7, 18.50, '2023-10-30 14:30:00'),
    (8, 16, 8, 35.00, '2023-10-30 15:30:00'),
    (9, 18, 9, 11.75, '2023-10-30 16:30:00'),
    (10, 20, 10, 40.75, '2023-10-30 17:30:00');
    INSERT INTO Payments (PaymentID, RiderID, RideID, PaymentAmount, PaymentDate)
VALUES
    (11, 2, 11, 18.25, '2023-10-31 10:00:00'),
    (12, 2, 12, 26.50, '2023-10-31 11:00:00'),
    (13, 2, 13, 16.75, '2023-10-31 12:00:00'),
    (14, 2, 14, 33.00, '2023-10-31 13:00:00'),
    (15, 2, 15, 14.00, '2023-10-31 14:00:00'),
    (16, 2, 16, 36.75, '2023-10-31 15:00:00'),
    (17, 2, 17, 10.25, '2023-10-31 16:00:00');

CREATE VIEW TopRatedDrivers AS
SELECT Drivers.DriverID, Users.FirstName, Users.LastName, AVG(Reviews.Rating) AS AverageRating
FROM Drivers
INNER JOIN Users ON Drivers.UserID = Users.UserID
LEFT JOIN Reviews ON Drivers.DriverID = Reviews.DriverID
GROUP BY Drivers.DriverID, Users.FirstName, Users.LastName;
#Highly rated drivers

SELECT * FROM TopRatedDrivers;

CREATE VIEW TopRatedRiders AS
SELECT Users.UserID, Users.FirstName, Users.LastName, MAX(Reviews.Rating) AS HighestRating
FROM Users
INNER JOIN Riders ON Users.UserID = Riders.UserID
INNER JOIN Reviews ON Riders.RiderID = Reviews.RiderID
GROUP BY Users.UserID, Users.FirstName, Users.LastName;
#High rating users

SELECT * FROM TopRatedRiders;

CREATE VIEW DriverStats AS
SELECT Drivers.DriverID, Users.FirstName, Users.LastName,
    COUNT(Rides.RideID) AS TotalRides,
    SUM(Rides.Fare) AS TotalEarnings
FROM Drivers
INNER JOIN Users ON Drivers.UserID = Users.UserID
LEFT JOIN Rides ON Drivers.DriverID = Rides.DriverID
GROUP BY Drivers.DriverID, Users.FirstName, Users.LastName;

select * from driverstats;
# Information about the rides



#DQL Statement
SELECT FirstName
FROM Users
WHERE UserID IN (SELECT UserID FROM Drivers WHERE VehicleType = 'Sedan');

SELECT Users.FirstName, Users.LastName
FROM Users
INNER JOIN Riders ON Users.UserID = Riders.UserID
WHERE Riders.RiderID IN (SELECT RiderID FROM Reviews WHERE Rating = 5);

SELECT Drivers.DriverID, Users.FirstName, Users.LastName,
       COUNT(Rides.RideID) AS TotalRides,
       SUM(Rides.Fare) AS TotalEarnings,
       AVG(Reviews.Rating) AS AverageRating
FROM Drivers
INNER JOIN Users ON Drivers.UserID = Users.UserID
LEFT JOIN Rides ON Drivers.DriverID = Rides.DriverID
LEFT JOIN Reviews ON Drivers.DriverID = Reviews.DriverID
GROUP BY Drivers.DriverID, Users.FirstName, Users.LastName
HAVING COUNT(Rides.RideID) >= 3;

SELECT Drivers.DriverID, Users.FirstName, Users.LastName, AVG(Reviews.Rating) AS AverageRating
FROM Drivers
INNER JOIN Users ON Drivers.UserID = Users.UserID
LEFT JOIN Reviews ON Drivers.DriverID = Reviews.DriverID
GROUP BY Drivers.DriverID, Users.FirstName, Users.LastName;
#This SQL query calculates the average rating for each driver based on their reviews and provides the driver's name and ID. The query uses joins to bring together data from the Drivers, Users, and Reviews tables and calculates the average rating using the AVG() function.

SELECT SUM(PaymentAmount) AS TotalPayment
FROM Payments
WHERE RiderID = 2;

SELECT SUM(PaymentAmount) AS TotalPaymentAmount30th
FROM Payments
WHERE DATE(PaymentDate) = '2023-10-30';

SELECT SUM(PaymentAmount) AS TotalPaymentAmount30th
FROM Payments
WHERE DATE(PaymentDate) = '2023-10-31';

#DML STATEMENTS
SELECT COUNT(*) AS TotalDrivers
FROM Drivers;

#Question 2: What is the full name and email of the rider with RiderID 6?
SELECT CONCAT(FirstName, ' ', LastName) AS FullName, Email
FROM Users
WHERE UserID = (SELECT UserID FROM Riders WHERE RiderID = 6);



INSERT INTO Users (UserID, FirstName, LastName, Email, PhoneNumber, UserType)
VALUES
    (1, 'Aarav', 'Kumar', 'aarav.kumar@example.com', '9876543210', 'Driver'),
    (2, 'Aanya', 'Singh', 'aanya.singh@example.com', '8765432109', 'Rider');
   
UPDATE Riders
SET CreditCardNumber = '1111222233334444'
WHERE RiderID = 2;

UPDATE Drivers
SET LicensePlate = 'TX8765UV'
WHERE DriverID = 7;

#DDL STATEMENTS






SELECT * FROM TopRatedDrivers;


Select * from topratedriders;
