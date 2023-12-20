## Our World in Data Covid Data Analysis

## Data source

- [Covid 19 Data](https://ourworldindata.org/covid-deaths)

- `sql```SELECT location, date, total_cases, new_cases, total_deaths, population
FROM `Covid.CovidDeaths`
WHERE location = 'Bangladesh' 
ORDER BY 1,2;
