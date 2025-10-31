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

