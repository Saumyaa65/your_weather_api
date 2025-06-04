# Simple Weather API with Flask

This project implements a **simple weather API** using the **Flask framework**, designed to serve historical temperature data for various weather stations. It allows users to query temperature information by station ID, date, or retrieve all data for a specific station or year.

## Overview

The "Simple Weather API" provides a lightweight and efficient way to access historical temperature records. By setting up a local server, users can retrieve temperature data through well-defined API endpoints, making it a useful tool for data analysis, personal projects, or learning about API development with Flask.

## Features

* **Home Page:** Displays a list of available weather stations with their IDs and names, providing an overview of the data sources.
* **Specific Date Temperature:** Retrieve the temperature for a given station on a specific date.
* **All Station Data:** Fetch all available temperature data for a specified weather station.
* **Yearly Station Data:** Get all temperature records for a particular station within a specified year.
* **Data from Local Files:** Reads historical data directly from structured text files.
* **Temperature Conversion:** Automatically converts temperature values (stored in tenths of a degree) to standard units (e.g., Celsius).

## Technologies Used

* Python
* Flask (for building the web API)
* Pandas (for efficient data reading and manipulation)

## How It Works

The Flask application sets up several routes (API endpoints) to handle different types of weather data requests:

1.  **Home Page (`/`):**
    * When a user accesses the root URL, the `home()` function is triggered.
    * It reads station information from `data_small/stations.txt`.
    * It renders an HTML template (`home.html`, which you would need to create in a `templates/` directory) and injects the stations data as an HTML table.

2.  **Specific Date Temperature (`/api/v1/<station>/<date>`):**
    * This endpoint takes a `station` ID and a `date` as parameters.
    * It constructs the filename for the corresponding station's data file (e.g., `data_small/TG_STAID000001.txt`).
    * It reads the data file, parses the 'DATE' column, and filters the DataFrame to find the temperature for the exact specified date.
    * The temperature value (originally in tenths of a degree) is divided by 10.
    * Returns a JSON object containing the station ID, date, and temperature.

3.  **All Station Data (`/api/v1/<station>`):**
    * This endpoint takes a `station` ID as a parameter.
    * It reads the entire data file for that station.
    * Converts the entire DataFrame into a list of dictionaries, where each dictionary represents a row (a date's data).
    * Returns this list as a JSON response.

4.  **Yearly Station Data (`/api/v1/yearly/<station>/<year>`):**
    * This endpoint takes a `station` ID and a `year` as parameters.
    * It reads the data file for the specified station.
    * It filters the DataFrame to include only records from the given year (by checking if the ' DATE' column string starts with the `year` string).
    * Returns the filtered yearly data as a JSON response (list of dictionaries).
