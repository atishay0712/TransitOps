# Database Design

## Tables

Users

Vehicles

Drivers

Trips

Maintenance

FuelLogs

Expenses


---

## Detailed Table Schema

### 1. Users Table
```sql
CREATE TABLE Users (
    user_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    role VARCHAR(20) NOT NULL
);
CREATE TABLE Vehicles (
    vehicle_id INTEGER PRIMARY KEY AUTOINCREMENT,
    vehicle_no VARCHAR(20) UNIQUE NOT NULL,
    type VARCHAR(20) NOT NULL,
    capacity INTEGER,
    status VARCHAR(20) DEFAULT 'Active'
);
CREATE TABLE Drivers (
    driver_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name VARCHAR(100) NOT NULL,
    license_no VARCHAR(20) UNIQUE NOT NULL,
    phone VARCHAR(15)
);
CREATE TABLE Trips (
    trip_id INTEGER PRIMARY KEY AUTOINCREMENT,
    vehicle_id INTEGER NOT NULL,
    driver_id INTEGER NOT NULL,
    source VARCHAR(100) NOT NULL,
    destination VARCHAR(100) NOT NULL,
    trip_date DATE NOT NULL,
    FOREIGN KEY (vehicle_id) REFERENCES Vehicles(vehicle_id),
    FOREIGN KEY (driver_id) REFERENCES Drivers(driver_id)
);
CREATE TABLE Maintenance (
    maintenance_id INTEGER PRIMARY KEY AUTOINCREMENT,
    vehicle_id INTEGER NOT NULL,
    service_date DATE NOT NULL,
    cost DECIMAL(10,2),
    description TEXT,
    FOREIGN KEY (vehicle_id) REFERENCES Vehicles(vehicle_id)
);
CREATE TABLE FuelLogs (
    fuel_id INTEGER PRIMARY KEY AUTOINCREMENT,
    vehicle_id INTEGER NOT NULL,
    log_date DATE NOT NULL,
    liters DECIMAL(10,2),
    cost DECIMAL(10,2),
    FOREIGN KEY (vehicle_id) REFERENCES Vehicles(vehicle_id)
);
CREATE TABLE Expenses (
    expense_id INTEGER PRIMARY KEY AUTOINCREMENT,
    vehicle_id INTEGER NOT NULL,
    expense_date DATE NOT NULL,
    type VARCHAR(50),
    amount DECIMAL(10,2),
    FOREIGN KEY (vehicle_id) REFERENCES Vehicles(vehicle_id)
);
