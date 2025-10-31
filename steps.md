# Demographic Analysis of Nationalities in Slovakia (2021–2024)

A small data analysis project using data from the Statistical Office of the Slovak Republic (Štatistický úrad SR).  
This project focuses on exploring demographic trends by **nationality** and **gender** across Slovak regions.

---

## Step 1: Data Collection and Cleaning

### Files downloaded

Excel files containing all nationalities in Slovakia, broken down by gender, from the Statistical Office of the Slovak Republic (ŠÚ SR).

- Men: `Narodnost_muzi_2021_2024.xlsx`  
- Women: `Narodnost_zeny_2021_2024.xlsx`

### Data cleaning and preparation

1. Imported all Excel files into a single working file.  
2. Combined the data into one dataset with the following columns:
   - **Uzemie** (Region / Administrative unit)  
   - **rok_2021 … rok_2024** (Years)  
   - **Narodnost** (Nationality)  
   - **Pohlavie** (Gender)  
3. Ensured consistency in naming conventions and removed any empty or duplicate rows.  
4. Saved the cleaned dataset as:

   `demografia_narodnost_pohlavie_2021_2024.xlsx`

### Notes

- This cleaned dataset will be used for all subsequent analyses in SQL and Power BI.  
- Its structure allows for easy filtering by year, region, nationality, and gender.

### Data source

The data for this analysis was downloaded from the Statistical Office of the Slovak Republic (ŠÚ SR).  

**Dataset:** Bilancia podľa národnosti a pohlavia - SR-oblasť-kraj-okres, m-v  
**Last updated:** 31.03.2025  
**Territorial level:** Slovakia + regions + districts  
**Time period:** Annual, 1996–2022  
**Dimensions:**  
- Years  
- Regions / Areas / Districts  
- Gender  
- Nationality  
- Data  
**View:** Demographic Balance by Nationality and Sex - SR-Area-Reg-District, U-R (dom7002rr)

---

## Step 2: Data Analysis with SQLite

To analyse the dataset, I imported the cleaned Excel file into an SQLite database.  
I used **DBeaver** as the database management tool to explore, query, and manipulate the data.

This setup enabled me to:

- Run SQL queries to aggregate and filter data by year, region, nationality, and gender.  
- Perform basic statistical analysis to uncover trends and patterns.  
- Prepare datasets for visualisation in Power BI.
## Step 3: Example SQL Analysis

As an example, I explored how the population of different nationalities changed in **urban and rural areas** between 2021 and 2024.  
This analysis provides an overview of demographic differences between **cities (Mesta)** and the **countryside (Vidiek)**.

### SQL query

```sql
SELECT 
    Uzemie,
    Narodnost,
    SUM(rok_2021) AS population_2021,
    SUM(rok_2024) AS population_2024,
    (SUM(rok_2024) - SUM(rok_2021)) AS change_in_population
FROM demografia_narodnost_pohlavie
WHERE Uzemie IN ('Mesta', 'Vidiek')
GROUP BY Uzemie, Narodnost
ORDER BY change_in_population DESC;
```
This query compares the total population of each nationality in **cities and rural areas** and shows how their numbers changed between 2021 and 2024.  

Such an overview can reveal:
- Which nationalities are growing or declining in urban and rural environments.  
- Possible migration patterns or demographic shifts.  

The results of this query will be visualised in Power BI later on.
## Step 4: SQL Analysis – Population by Nationality in Urban and Rural Areas

For this step, I exported the full result of the previous SQL query (Step 3) from DBeaver into a **CSV file**, which contains all ~60 rows.  

- **Full dataset (CSV):** [`sql_analysis_urban_rural.csv`](./sql_analysis_urban_rural.csv)  

### Sample of the data

| Uzemie | Narodnost   | population_2021 | population_2024 | change_in_population |
|--------|------------|----------------|----------------|--------------------|
| Vidiek | slovenska  | 2,137,203      | 2,178,436      | 41,233             |
| Mesta  | ukrajinska | 6,608          | 8,816          | 2,208              |
| Vidiek | ceska      | 9,603          | 10,221         | 618                |
| Mesta  | vietnamska | 2,414          | 2,959          | 545                |
| Vidiek | ukrajinska | 3,160          | 3,593          | 433                |
| Mesta  | srbska     | 807            | 1,201          | 394                |
| Mesta  | ruska      | 2,510          | 2,846          | 336                |
| Mesta  | cinska     | 1,133          | 1,305          | 172                |

> This exported CSV file can be opened in Excel, Power BI, or any data tool for further analysis and visualisation.  
> The table above is just a preview of the full dataset.

