### Project/Goals: Organise and manipulate the ecommerce data base using the tables to answer questions and make predictions.
#### Setup

I followed these steps in setting up for the project.

1. Downloaded the source csv files to your local computer.
2. Analyzed each file to check each tables list of columns and their expected data types.
3. Created a table for each source csv file, and named the table to correspond with the source files.
4. Created the tables with all the columns having the **TEXT** data type. This helped with the seamless ingestion of the csv files.
5. In Postgres, I right-clicked on each table and clicked on Import/Export data. Then followed the prompt to import each file to their corresponding tables.
6. I started off with the starting with data section, so that I could make sense of the data in each table.
7. I followed with cleaning the data.
8. Then I ended with answering questions with the cleaned data.

#### Results
I was able to use the data to determine the following:
- Cities and countries that have the highest level of transaction revenues on the site.
- The average number of products ordered from visitors in each city and country.
- There was no pattern in the types (product categories) of products ordered from visitors in each city and country.
- The top-selling product from each city/country and that there was no pattern worthy of noting in the products sold.
- The impact of revenue generated from each city/country.

#### Challenges 
There was not much information about the data and the source. Most of the queries had to be written based on assumptions about the data.

#### Future Goals
Create more QA queries for my QA processes.
