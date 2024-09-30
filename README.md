# Database Interacation in Web Applications

This demonstrates the cconnection of MySQL database and Node.js to create a simple API

## Requirements
- [Node.js](https://nodejs.org/) installed
-  MySQL installed and running
-  A code editor, like [Visual Studio Code](https://code.visualstudio.com/download)

## Setup
1. Clone the repository
2. Initialize the node.js environment
   ```
   npm init -y
   ```
3. Install the necessary dependancies
   ```
   npm install express mysql2 dotenv nodemon
   ```
4. Create a ``` server.js ``` and ```.env``` files
5. Basic ```server.js``` setup
   <br>
   
   ```js
   const express = require('express')
   const app = express()

   
   // Question 1 goes here


   // Question 2 goes here


   // Question 3 goes here


   // Question 4 goes here

   

   // listen to the server
   const PORT = 3000
   app.listen(PORT, () => {
     console.log(`server is runnig on http://localhost:${PORT}`)
   })
   ```
<br><br>

## Run the server
   ```
   nodemon server.js
   ```
<br><br>

## Setup the ```.env``` file
```.env
DB_USERNAME=root
DB_HOST=localhost
DB_PASSWORD=your_password
DB_NAME=hospital_db
```

<br><br>

## Configure the database connection and test the connection
Configure the ```server.js``` file to access the credentials in the ```.env``` to use them in the database connection

<br>

## 1. Retrieve all patients
Create a ```GET``` endpoint that retrieves all patients and displays their:
- ```patient_id```
- ```first_name```
- ```last_name```
- ```date_of_birth```

<br>

## 2. Retrieve all providers
Create a ```GET``` endpoint that displays all providers with their:
- ```first_name```
- ```last_name```
- ```provider_specialty```

<br>

## 3. Filter patients by First Name
Create a ```GET``` endpoint that retrieves all patients by their first name

<br>

## 4. Retrieve all providers by their specialty
Create a ```GET``` endpoint that retrieves all providers by their specialty

<br>


## NOTE: Do not fork this repository




Step-by-Step Implementation
Clone the Repository: Follow your usual git cloning procedure.

Initialize the Node.js Environment:

bash
npm init -y
Install Necessary Dependencies:

bash
npm install express mysql2 dotenv nodemon
Create server.js and .env Files:

Create a file named server.js.
Create a file named .env.
Set Up the .env File: In your .env file, add:

makefile
Copy code
DB_USERNAME=root
DB_HOST=localhost
DB_PASSWORD=your_password
DB_NAME=hospital_db
Basic Setup in server.js:

Here’s how you can set up your server.js file:

javascript
const express = require('express');
const mysql = require('mysql2');
const dotenv = require('dotenv');

dotenv.config();
const app = express();

// Database connection
const db = mysql.createConnection({
  host: process.env.DB_HOST,
  user: process.env.DB_USERNAME,
  password: process.env.DB_PASSWORD,
  database: process.env.DB_NAME,
});

// Connect to the database
db.connect(err => {
  if (err) {
    console.error('Database connection failed:', err);
    return;
  }
  console.log('Connected to the database.');
});

// Question 1: Retrieve all patients
app.get('/patients', (req, res) => {
  db.query('SELECT patient_id, first_name, last_name, date_of_birth FROM patients', (err, results) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(results);
  });
});

// Question 2: Retrieve all providers
app.get('/providers', (req, res) => {
  db.query('SELECT first_name, last_name, provider_specialty FROM providers', (err, results) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(results);
  });
});

// Question 3: Filter patients by First Name
app.get('/patients/first_name/:name', (req, res) => {
  const { name } = req.params;
  db.query('SELECT * FROM patients WHERE first_name = ?', [name], (err, results) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(results);
  });
});

// Question 4: Retrieve all providers by their specialty
app.get('/providers/specialty/:specialty', (req, res) => {
  const { specialty } = req.params;
  db.query('SELECT * FROM providers WHERE provider_specialty = ?', [specialty], (err, results) => {
    if (err) {
      return res.status(500).json({ error: err.message });
    }
    res.json(results);
  });
});

// Listen to the server
const PORT = 3000;
app.listen(PORT, () => {
  console.log(`Server is running on http://localhost:${PORT}`);
});
Run the Server:
bash
nodemon server.js
Explanation of the Code:
Environment Variables: dotenv is used to access sensitive configuration from the .env file.
MySQL Connection: A connection to the MySQL database is established using the credentials from the .env file.
Endpoints:
GET /patients: Fetches all patients.
GET /providers: Fetches all providers.
GET /patients/first_name/
: Filters patients by their first name.
GET /providers/specialty/
: Filters providers by their specialty.
