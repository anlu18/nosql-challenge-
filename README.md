

---

## NoSQL Database Setup and Analysis

### Overview
This project involves setting up and updating a NoSQL database, as well as performing exploratory data analysis on a dataset of UK food establishments. The key tasks include inserting and updating records, querying the database for specific information, and converting query results into a format suitable for analysis using Pandas.

### Database Setup and Updates

- **Script Files:**
  - `NoSQL_setup.ipynb`: This notebook is used to set up and update the database.
  - `NoSQL_analysis.ipynb`: This notebook queries relevant information for analysis and converts the results into Pandas DataFrames.

- **Data Import:**
  The data provided in the `establishments.json` file was imported into the MongoDB database using the following command in the Terminal:
  ```
  mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json
  ```

#### Key Operations

1. **Insert a New Restaurant:**
   - A new halal restaurant located in Greenwich was added to the database using:
     ```python
     establishments.insert_one(new_restaurant)
     ```

2. **Update Restaurant Information:**
   - The newly added restaurant was updated with the correct `BusinessTypeID` using:
     ```python
     establishments.update_one(
         new_restaurant, 
         {'$set': {'BusinessTypeID': 1}}
     )
     ```

3. **Delete Establishments in Dover:**
   - All establishments under the Local Authority of Dover were removed from the database:
     ```python
     establishments.delete_many({'LocalAuthorityName': 'Dover'})
     ```

4. **Convert Geolocation Data:**
   - The latitude and longitude fields were converted to decimal numbers:
     ```python
     establishments.update_many(
         {}, 
         [{'$set': {
             'geocode.longitude': {'$toDouble': '$geocode.longitude'}, 
             'geocode.latitude': {'$toDouble': '$geocode.latitude'}
         }}]
     )
     ```

### Exploratory Analysis

1. **Hygiene Score Analysis:**
   - **Query:** Identify establishments with a hygiene score of 20.
   - **Result:** There are 41 establishments with a hygiene score of 20 in the `uk_food` dataset.

2. **Rating Analysis in London:**
   - **Query:** Find establishments in London with a `RatingValue` of 4 or higher.
   - **Result:** There are 34 establishments in London with a `RatingValue` greater than or equal to 4.

3. **Top Establishments Near "Penang Flavours":**
   - **Query:** Identify the top 5 establishments with a `RatingValue` of '5', sorted by the lowest hygiene score, and located nearest to the newly added restaurant "Penang Flavours".
   - **Result:** The top 5 establishments are:
     - "Volunteer"
     - "Plumstead Manor Nursery"
     - "Atlantic Fish Bar"
     - "Iceland"
     - "Howe and Co Fish and Chips - Van 17"

---

