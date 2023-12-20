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
```

<br>

The first calculation I wanted was total deaths divided by total cases to get the case fatality rate. This shows the likelihood of dying if you contract COVID-19 in your country.

```sql
SELECT location, date, total_cases, total_deaths, (total_deaths/total_cases)*100 AS case_fatality_rate
FROM `Covid.CovidDeaths` 
WHERE location = "Bangladesh"
ORDER BY 1,2;
```

<br>

I then began looking at the total cases vs the population to see what percentage of the population got covid.

```sql
SELECT location, date, population, total_cases, (total_cases/population)*100 AS perecentage_infected
FROM `Covid.CovidDeaths` 
WHERE location = "Bangladesh"
ORDER BY 1,2;
```
<br>

I want to know what countries have the highest infection rates with the following query:

```sql
SELECT location, population, MAX(total_cases) AS highest_infection_count, MAX((total_cases/population))*100 AS percentage_infected
FROM `Covid.CovidDeaths` 
GROUP BY location, population
ORDER BY 4 DESC;
```

<br>

One thing That I noticed was the there were some areas of data that was showing whole continents instead of countries. This happended becasue the continent location was labled as Null and the "location" or country was labeled with the corresponding continent.

```sql
SELECT location, population, MAX(total_cases) AS highest_infection_count, MAX((total_cases / population) * 100) AS percentage_infected
FROM `Covid.CovidDeaths`
WHERE continent IS NULL
GROUP BY location, population
ORDER BY 4 DESC;
```
<br>

In order to fix this and get the right data we need to search for data where the continent is not null. The following code applies to the prior SQL query.

```sql
SELECT location, population, MAX(total_cases) AS highest_infection_count, MAX((total_cases / population) * 100) AS percentage_infected
FROM `Covid.CovidDeaths`
WHERE continent IS NOT NULL
GROUP BY location, population
ORDER BY 4 DESC;
```

<br>

Now I am going to do the same for deaths. The following query will show us the percentage of deaths and who had the highest deaths in comparison to their population.

```sql
SELECT location, population, MAX(total_deaths) AS total_death_count, MAX(total_deaths)/population*100 AS percentage_deaths
FROM `Covid.CovidDeaths`
WHERE continent IS NOT NULL
GROUP BY location, population
ORDER BY percentage_deaths DESC;
```
