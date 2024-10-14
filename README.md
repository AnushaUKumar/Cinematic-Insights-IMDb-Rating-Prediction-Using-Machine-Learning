# Cinematic Insights Database Normalization and IMDb Prediction

## Project Overview

This project focuses on creating a normalized database from raw movie datasets and then using it for IMDb score prediction and analysis. The data starts in a non-normalized format (TSV) and is processed using **SQLite** into a normalized database structure. The project is divided into several stages: reading the raw TSV data, creating a non-normalized database (`Cinematic_Pulse`), transforming it into a normalized structure (`Normalised`), and inserting the data into normalized tables such as **Media**, **IMDb**, **Genre**, and **Season**. Additionally, a `GenreSplit` table is created to handle multiple genres.

## Key Features

1. **Data Loading and Preprocessing**:
   - Reads raw data from a TSV (Tab-Separated Values) file (`titles.tsv`) and loads it into a non-normalized SQLite database (`Cinematic_Pulse1.db`).
   - Handles missing and inconsistent values, ensuring the data is ready for further processing.

2. **Non-Normalized to Normalized Database**:
   - Creates a normalized database (`Normalised1.db`) with separate tables for **Media**, **IMDb**, **Genre**, and **Season**.
   - Data from the non-normalized `Cinematic_Pulse1.db` is split and inserted into the normalized tables.
   - Ensures that each normalized table references others using foreign keys (e.g., linking the **Media** table to the **IMDb** table).

3. **PostgreSQL and SQL Queries**:
   - Utilizes SQL queries to extract relevant data from the non-normalized tables.
   - Data normalization ensures minimal redundancy, optimal storage, and faster querying.

4. **Genre Splitting**:
   - Handles movies with multiple genres by splitting the genres into a separate `GenreSplit` table, making the data more queryable and manageable.

5. **Database Normalization**:
   - Normalizes the data to avoid redundancy and improve performance by following database normalization principles (1NF, 2NF, and 3NF).
   - Ensures referential integrity across the tables by linking related fields (e.g., **IMDb_ID** in **Media** references **IMDb** table).

6. **Final Prediction Task**:
   - After data normalization, the clean and structured data is ready for machine learning tasks like predicting IMDb ratings and analyzing cinematic trends.

## Database Schema

### Non-Normalized Database (`Cinematic_Pulse1.db`)
- **Raw TSV Data**: Initially stored as-is, with all fields loaded into a single non-normalized table.
- **Fields in the non-normalized table**: 
    - IMDb Score
    - Votes
    - Media ID
    - Title
    - Type
    - Description
    - Release Year
    - Runtime
    - Genres (list format)
    - Seasons

### Normalized Database (`Normalised1.db`)

#### Tables:
- **IMDb**: Stores IMDb-related data.
  - `IMDb_ID`: Unique ID for IMDb data.
  - `IMDb_Score`: IMDb score for the movie/TV show.
  - `IMDb_Votes`: Number of votes the movie/TV show has on IMDb.
  
- **Media**: Stores general media data such as movie or TV show information.
  - `ID`: Unique media ID.
  - `Title`: Title of the movie/TV show.
  - `Type`: Whether it's a movie or TV show.
  - `Description`: Brief summary of the movie/TV show.
  - `Release_Year`: Year of release.
  - `Age_Certification`: Age certification of the media.
  - `Runtime`: Runtime in minutes.
  - `TMDB_Popularity`: Popularity score from TMDB.
  - `TMDB_Score`: TMDB rating.

- **Genre**: Stores the genres associated with media.
  - `Media_ID`: Foreign key referencing the **Media** table.
  - `Genre`: A list of genres associated with the media.

- **Season**: Stores the number of seasons for TV shows.
  - `Media_ID`: Foreign key referencing the **Media** table.
  - `Seasons`: Number of seasons.

- **GenreSplit**: Handles the splitting of genres into individual entries.
  - `Media_ID`: Foreign key referencing the **Media** table.
  - `Single_Genre`: A single genre extracted from the `Genre` table for easier querying.

## Installation

To set up and run the project, follow these steps:

### 1. Clone the Repository

```bash
git clone https://github.com/YOUR_USERNAME/cinematic-insights.git
cd cinematic-insights
```

### 2. Run the Code
To execute the code and generate the databases:
python main_script.py

This script will:

- Create the Cinematic_Pulse1.db with non-normalized data.
- Create the Normalised1.db with normalized tables for Media, IMDb, Genre, and Season.
- Insert the relevant data into the normalized tables.
#### Database Normalization Process
- Step 1: Load the TSV data into a non-normalized database.
- Step 2: Create separate tables for Media, IMDb, Genre, and Season.
- Step 3: Transfer the data from the non-normalized database to the normalized structure.
- Step 4: Handle the splitting of multiple genres into the GenreSplit table.
  
## Future Enhancements
- Enhanced Scraping: Improve data collection by scraping more platforms such as IMDb, TMDB, and Rotten Tomatoes for additional information.
- Advanced Querying: Add functionality for more complex SQL queries, such as finding media based on multiple genres or analyzing IMDb trends over time.
- Data Analysis: Integrate machine learning models for advanced predictions on IMDb ratings based on other factors like cast, budget, and release timing.

## Technologies Used
- Python: Core programming language for data manipulation and database management.
- SQLite: Used for both non-normalized and normalized database storage.
- Pandas: For reading the raw TSV data and performing data manipulations.
- SQL: For querying and inserting data into the SQLite databases.
- PostgreSQL (Optional): Can be used for larger-scale deployment.

## Acknowledgments
Special thanks to the open-source community and the contributors who provided valuable insights into database normalization and IMDb prediction techniques.







