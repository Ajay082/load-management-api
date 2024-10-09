# Load Management API

## Overview
The Load Management API is a Spring Boot application designed to manage logistics loads for various shippers. It provides endpoints to add, retrieve, update, and delete load information in a seamless manner. The API interfaces with a PostgreSQL database to store load data.

## Table of Contents
- [Technologies Used](#technologies-used)
- [Getting Started](#getting-started)
- [Project Structure](#project-structure)
- [Database Setup](#database-setup)
- [API Endpoints](#api-endpoints)
- [Example Requests](#example-requests)
- [Contributing](#contributing)
- [License](#license)

## Technologies Used
- **Java 23**
- **Spring Boot**
- **Spring Data JPA**
- **PostgreSQL**
- **Maven**

## Getting Started
To run the Load Management API locally, follow these steps:

### Prerequisites
- Java Development Kit (JDK) 11 or higher
- PostgreSQL database installed and running
- Maven for project management

### Clone the Repository
```bash
git clone https://github.com/Ajay082/load-management-api.git
cd load-management-api
```

### Configure Database
1. Open `src/main/resources/application.properties`.
2. Update the following properties with your database credentials:
   ```properties
   spring.datasource.url=jdbc:postgresql://localhost:5432/your_database_name
   spring.datasource.username=your_username
   spring.datasource.password=your_password
   spring.jpa.hibernate.ddl-auto=update
   ```

### Build the Project
```bash
mvn clean install
```

### Run the Application
```bash
mvn spring-boot:run
```
The application should start on `http://localhost:8080`.

## Project Structure
```
load-management-api
│
├── src
│   ├── main
│   │   ├── java
│   │   │   └── com
│   │   │       └── example
│   │   │           └── load_api
│   │   │               ├── controller
│   │   │               ├── model
│   │   │               ├── repository
│   │   │               └── service
│   │   └── resources
│   │       └── application.properties
└── pom.xml
```

## Database Setup
### PostgreSQL Database
1. **Create Database**: Open your PostgreSQL command line or any database GUI (like pgAdmin) and create a database:
   ```sql
   CREATE DATABASE your_database_name;
   ```

2. **Create Load Table**: The table will be automatically created by Hibernate if you have set `spring.jpa.hibernate.ddl-auto=update`. However, if you want to create it manually, use the following SQL:
   ```sql
   CREATE TABLE loads (
       load_id SERIAL PRIMARY KEY,
       loading_point VARCHAR(255),
       unloading_point VARCHAR(255),
       product_type VARCHAR(255),
       truck_type VARCHAR(255),
       no_of_trucks INT,
       weight DECIMAL,
       comment TEXT,
       date DATE,
       shipper_id BIGINT
   );
   ```

## API Endpoints
| Method | Endpoint                | Description                               |
|--------|-------------------------|-------------------------------------------|
| POST   | /load                   | Add a new load                            |
| GET    | /load                   | Get list of loads by shipperId           |
| GET    | /load/{loadId}         | Get load details by loadId                |
| PUT    | /load/{loadId}         | Update an existing load                   |
| DELETE | /load/{loadId}         | Delete a load by loadId                  |

## Example Requests
### Add a New Load
```http
POST /load
Content-Type: application/json

{
    "loadingPoint": "Delhi",
    "unloadingPoint": "Jaipur",
    "productType": "Chemicals",
    "truckType": "Canter",
    "noOfTrucks": 1,
    "weight": 100.5,
    "comment": "Handle with care",
    "date": "2024-10-09",
    "shipperId": 1
}
```

### Get Loads by Shipper ID
```http
GET /load?shipperId=1
```

### Update an Existing Load
```http
PUT /load/1
Content-Type: application/json

{
    "loadingPoint": "Mumbai",
    "unloadingPoint": "Pune",
    "productType": "Electronics",
    "truckType": "Trailer",
    "noOfTrucks": 2,
    "weight": 200.75,
    "comment": "Fragile items",
    "date": "2024-10-10",
    "shipperId": 1
}
```

### Delete a Load
```http
DELETE /load/1
```

## Contributing
Feel free to submit issues or create pull requests for improvements and enhancements.


### Notes:
- Replace placeholders like `yourusername`, `your_database_name`, `your_username`, and `your_password` with actual values.
- You can add any additional instructions or details that are relevant to your specific implementation.

Let me know if you need any modifications or additional information!

