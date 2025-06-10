# Compass-DBMS
its a database management system for a compass made using MySql queries  

-- create database Compass;
-- use compass
-- 1. Users Table
-- CREATE TABLE User (
--     user_id INT PRIMARY KEY AUTO_INCREMENT,
--     username VARCHAR(50) UNIQUE NOT NULL,
--     password VARCHAR(255) NOT NULL, -- Store hashed passwords in practice
--     last_login DATETIME
-- );

-- -- 2. Manufacturer Table (NEW: Avoid repeating manufacturer names)
-- CREATE TABLE Manufacturer (
--     manufacturer_id INT PRIMARY KEY AUTO_INCREMENT,
--     name VARCHAR(100) NOT NULL,
--     contact_info VARCHAR(255)
-- );

-- -- 3. Compass Table (Added user_id and manufacturer_id as FKs)
-- CREATE TABLE Compass (
--     compass_id INT PRIMARY KEY AUTO_INCREMENT,
--     model VARCHAR(50),
--     creation_date DATE NOT NULL,
--     user_id INT, -- Links to User (OWNS relationship)
--     manufacturer_id INT, -- Links to Manufacturer
--     FOREIGN KEY (user_id) REFERENCES User(user_id) ON DELETE CASCADE,
--     FOREIGN KEY (manufacturer_id) REFERENCES Manufacturer(manufacturer_id) ON DELETE SET NULL
-- );

-- -- 4. Calibration Table (NEW: Track calibration history instead of a static status)
-- CREATE TABLE Calibration (
--     calibration_id INT PRIMARY KEY AUTO_INCREMENT,
--     compass_id INT NOT NULL,
--     calibration_date DATE NOT NULL,
--     status ENUM('calibrated', 'pending', 'failed') NOT NULL,
--     notes TEXT,
--     FOREIGN KEY (compass_id) REFERENCES Compass(compass_id) ON DELETE CASCADE
-- );

-- -- 5. Measurement Table
-- CREATE TABLE Measurement (
--     measurement_id INT PRIMARY KEY AUTO_INCREMENT,
--     compass_id INT NOT NULL,
--     timestamp DATETIME NOT NULL,
--     pitch DECIMAL(5,2),
--     magnetic_direction DECIMAL(5,2),
--     FOREIGN KEY (compass_id) REFERENCES Compass(compass_id) ON DELETE CASCADE
-- );

-- -- 6. Destination Table (NEW: Normalize destination data)
-- CREATE TABLE Destination (
--     destination_id INT PRIMARY KEY AUTO_INCREMENT,
--     name VARCHAR(100) NOT NULL,
--     latitude DECIMAL(9,6) NOT NULL,
--     longitude DECIMAL(9,6) NOT NULL
-- );

-- -- 7. Location Table (Renamed/Enhanced: Tracks route points with timestamps)
-- CREATE TABLE Location (
--     location_id INT PRIMARY KEY AUTO_INCREMENT,
--     compass_id INT NOT NULL,
--     destination_id INT, -- Links to Destination
--     timestamp DATETIME NOT NULL,
--     latitude DECIMAL(9,6) NOT NULL, -- Current latitude
--     longitude DECIMAL(9,6) NOT NULL, -- Current longitude
--     sequence_number INT, -- Optional: Order of points in a route
--     FOREIGN KEY (compass_id) REFERENCES Compass(compass_id) ON DELETE CASCADE,
--     FOREIGN KEY (destination_id) REFERENCES Destination(destination_id) ON DELETE SET NULL
-- );



-- Insert sample users
-- INSERT INTO User (username, password, last_login) VALUES
-- ('john_doe', 'securepass123', '2024-01-15 08:30:00'),
-- ('sarah_smith', 'mountain#456', '2024-01-14 15:22:00');

--- - Insert manufacturers
-- INSERT INTO Manufacturer (name, contact_info) VALUES
-- ('GeoNav Inc.', 'support@geonav.com'),
-- ('OutdoorTech', 'help@outdoortech.com');

-- -- Insert compasses (owned by users and linked to manufacturers)
-- INSERT INTO Compass (model, creation_date, user_id, manufacturer_id) VALUES
-- ('GeoNav Pro X3', '2023-05-10', 1, 1),
-- ('OutdoorTech TrailMaster', '2023-12-01', 2, 2);

-- -- Insert calibration records
-- INSERT INTO Calibration (compass_id, calibration_date, status, notes) VALUES
-- (1, '2024-01-01', 'calibrated', 'Factory calibration'),
-- (1, '2024-01-14', 'pending', 'Field recalibration needed'),
-- (2, '2023-12-05', 'calibrated', 'Initial setup');

-- -- Insert destinations
-- INSERT INTO Destination (name, latitude, longitude) VALUES
-- ('Mountaineer''s Peak', 40.712776, -74.005974),
-- ('Lake Serenity', 34.052235, -118.243683);

-- -- Insert measurements from compasses
-- INSERT INTO Measurement (compass_id, timestamp, pitch, magnetic_direction) VALUES
-- (1, '2024-01-15 09:00:00', 12.5, 45.3),
-- (1, '2024-01-15 09:05:00', 14.2, 47.8),
-- (2, '2024-01-14 10:30:00', -5.7, 180.0);

-- -- Insert location/route data
-- INSERT INTO Location (compass_id, destination_id, timestamp, latitude, longitude, sequence_number) VALUES
-- (1, 1, '2024-01-15 09:00:00', 40.712700, -74.005900, 1),
-- (1, 1, '2024-01-15 09:05:00', 40.712800, -74.005800, 2),
-- (2, 2, '2024-01-14 10:30:00', 34.052200, -118.243600, 1);
