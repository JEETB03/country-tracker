

# Visited Countries Tracker

## Overview
This is a simple web application built using **Node.js** with **Express**, **PostgreSQL** as the database, and **EJS** for templating. The app allows users to track the countries they've visited by inserting country names, which are stored in a PostgreSQL database. The application also displays the total number of visited countries on the homepage.

## Features
- **View Visited Countries:** The app fetches and displays a list of all countries the user has marked as visited.
- **Add a Country:** Users can enter the name of a country they visited, and the application will store its country code in the database.
- **Validation:** The app checks for country existence and prevents duplicates, notifying the user if a country is already added or does not exist.

## Technologies Used
- **Node.js**
- **Express**
- **PostgreSQL**
- **EJS (Embedded JavaScript Templating)**
- **Body-Parser** (for parsing incoming request bodies)

## Prerequisites
Before running this project, ensure that you have the following installed:
- [Node.js](https://nodejs.org/)
- [PostgreSQL](https://www.postgresql.org/)
- Basic knowledge of SQL and a database with country data.

### Database Setup
Create a PostgreSQL database called `World` and set up the following tables:

1. **countries** (Stores country names and their corresponding country codes)
```sql
CREATE TABLE countries (
  country_code VARCHAR(3) PRIMARY KEY,
  country_name VARCHAR(100) NOT NULL
);
```

2. **visited_countries** (Stores visited countries)
```sql
CREATE TABLE visited_countries (
  id SERIAL PRIMARY KEY,
  country_code VARCHAR(3) REFERENCES countries(country_code)
);
```

Populate the `countries` table with the country codes and country names. You can find this data from public sources like ISO country code lists.

## Installation

1. Clone the repository:
   ```bash
   git clone https://github.com/JEETB03/country-tracker.git
   cd visited-countries-tracker
   ```

2. Install the dependencies:
   ```bash
   npm install
   ```

3. Set up your PostgreSQL connection by editing the connection details inside the `db` object in `index.js`:
   ```javascript
   const db = new pg.Client({
     user: "your-username",
     host: "localhost",
     database: "World",
     password: "your-password",
     port: 5432,
   });
   ```

4. Create the necessary tables in your PostgreSQL database using the SQL scripts mentioned earlier.

## Running the Application

1. Start the server:
   ```bash
   node index.js
   ```

2. Open your browser and navigate to `http://localhost:3000`.

## Usage
- On the home page, you will see a list of visited countries along with the total number of countries visited.
- To add a country, type the country's name into the input field and click "Submit".
- The app checks if the country is valid and not already added before saving it to the database.

## Error Handling
- **Duplicate Entry:** If a country has already been marked as visited, a message will appear stating that the country has already been added.
- **Invalid Country:** If the user enters a country name that doesn't exist in the database, they will be prompted with an error message.

## Future Improvements
- Add user authentication to track countries per user.
- Implement an API to fetch live country data rather than using a static database.
- Add a front-end framework like React or Vue.js for better user experience.

