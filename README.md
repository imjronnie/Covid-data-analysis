# Our World in Data Covid Data Analysis

### Data source

- [Covid 19 Data](https://ourworldindata.org/covid-deaths)

### Data Exploration

I first created two tables with the dataset to analyze deaths and vaccinations separately. I deleted everything that had to do with vaccines and called it CovidDeaths and then deleted everything that had to do with deaths and called it CovidVaccinations. I then imported it into BigQuery.

<br>

The first query I pulled was the following:

```sql
SELECT location, date, total_cases, new_cases, total_deaths, population
FROM `Covid.CovidDeaths`
WHERE location = 'Bangladesh' 
ORDER BY 1,2;

<br>

The first calculation I wanted was total deaths divided by total cases to get the case fatality rate. This shows the likelihood of dying if you contract COVID-19 in your country.

```sql
SELECT location, date, total_cases, total_deaths, (total_deaths/total_cases)*100 AS case_fatality_rate
FROM `Covid.CovidDeaths` 
WHERE location = "Bangladesh"
ORDER BY 1,2;
