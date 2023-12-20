## Our World in Data Covid Data Analysis

## Data source

- [Covid 19 Data](https://ourworldindata.org/covid-deaths)


I first created two different tables with the dataset in order to analyze deaths and vaccinations seperately. I deleted everything that had to do with vaccines and called it covid_deaths and then deleted everything that had to do with deaths and called it covid_vaccinations. I then imported it into BigQuery.
The first query I pulled was the following:

```sql
SELECT location, date, total_cases, new_cases, total_deaths, population
FROM `Covid.CovidDeaths`
WHERE location = 'Bangladesh' 
ORDER BY 1,2;
