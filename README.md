# International-Census-Inferences

# Public database: International Census Data

# Question 1. Which was the most fertile year between 2000 and 2010 in India?

SELECT * FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`
WHERE country_name = "India" AND YEAR BETWEEN 2000 AND 2010
ORDER BY total_fertility_rate desc

# Output:

country_name	year	total_fertility_rate
India	2000	3.148

# Question 2. Which were the five countries with the highest total fertility rates in the year 2010?

SELECT * FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates`
WHERE YEAR = 2010
ORDER BY total_fertility_rate desc
LIMIT 5

# Output: 

country_name	year	total_fertility_rate
Niger	2010	7.4318
Chad	2010	6.6545
Mali	2010	6.515
Angola	2010	6.464
Somalia	2010	6.44


# Question 3. List out life expectancy rates and the corresponding mid year population in India?

SELECT 
L.life_expectancy, L.country_name, L.year,
P.midyear_population 
FROM `bigquery-public-data.census_bureau_international.mortality_life_expectancy` L
LEFT JOIN `bigquery-public-data.census_bureau_international.midyear_population` P
ON (
  L.country_code = P.country_code
)
WHERE L.country_code = "IN" 
ORDER BY midyear_population desc

# Output: 

country_name	year	total_fertility_rate
Niger	2010	7.4318
Chad	2010	6.6545
Mali	2010	6.515
Angola	2010	6.464
Somalia	2010	6.44


# Question 4. List the top 5 countries with the highest population and their corresponding fertility rates in the year 2019.

SELECT
F.country_name, F.total_fertility_rate, F.year,
P.population
FROM `bigquery-public-data.census_bureau_international.age_specific_fertility_rates` F
LEFT JOIN `bigquery-public-data.census_bureau_international.midyear_population_agespecific` P
ON (
  F.year = P.year
)
WHERE F.year = 2019 
ORDER BY population desc
LIMIT 5

# Output:

country_name	total_fertility_rate	year	population
Afghanistan	4.92	2019	14823938
Aruba	1.8308	2019	14823938
Antigua and Barbuda	1.9816	2019	14823938
Algeria	2.6249	2019	14823938
United Arab Emirates	1.7256	2019	14823938


# Question 5. In India, which year observed the highest growth rate and what was the corresponding population?

SELECT
G.country_name, G.year, G.growth_rate,
P.population
FROM `bigquery-public-data.census_bureau_international.birth_death_growth_rates` G
LEFT JOIN `bigquery-public-data.census_bureau_international.midyear_population_agespecific` P
ON (
  G.country_code = P.country_code
)
WHERE G.country_code = "IN"
ORDER BY growth_rate desc
LIMIT 1

# Output:

country_name	year	growth_rate	population
India	1991	1.904	12225742


# Question 6. List the 10 most populous countries in the year 2019.

SELECT 
midyear_population, year, country_name
FROM `bigquery-public-data.census_bureau_international.midyear_population`
WHERE year = 2019
ORDER BY midyear_population desc
LIMIT 10

# Output:

midyear_population	year	country_name
1389618778	2019	China
1311559204	2019	India
331883986	2019	United States
264935824	2019	Indonesia
210797836	2019	Pakistan
210301591	2019	Brazil
208679114	2019	Nigeria
161062905	2019	Bangladesh
141944641	2019	Russia
127318112	2019	Mexico

# Question 7. Which are the countries that had a population of over 100 million (100,000,000) in the year 2019?

SELECT 
midyear_population, year, country_name
FROM `bigquery-public-data.census_bureau_international.midyear_population`
WHERE year = 2019 AND midyear_population > 100000000
ORDER BY midyear_population asc

# Output: 

midyear_population	year	country_name
101776661	2019	Egypt
107535277	2019	Philippines
111483031	2019	Ethiopia
125853035	2019	Japan
127318112	2019	Mexico
141944641	2019	Russia
161062905	2019	Bangladesh
208679114	2019	Nigeria
210301591	2019	Brazil
210797836	2019	Pakistan
264935824	2019	Indonesia
331883986	2019	United States
1311559204	2019	India
1389618778	2019	China

# Question 8. How many countries had a population over 100 million in the year 2019?

SELECT COUNT(country_name) as No_of_countries
FROM `bigquery-public-data.census_bureau_international.midyear_population` 
WHERE year = 2019 AND midyear_population > 100000000 

# Output:

No_of_countries
14


# Question 9. What are the average life expectancy rates of males and females in China in the last decade?

SELECT AVG (life_expectancy_male) AS life_expectancy_male , AVG (life_expectancy_female) AS life_expectancy_female
FROM `bigquery-public-data.census_bureau_international.mortality_life_expectancy`
WHERE country_name = "China" AND year BETWEEN 2009 AND 2019

# Output:

life_expectancy_male	life_expectancy_female
73.23636363636363	77.57818181818182


# Question 10. List the 5 countries with the lowest infant mortality rates in the year 2010.

SELECT 
country_name, infant_mortality
FROM `bigquery-public-data.census_bureau_international.mortality_life_expectancy`
WHERE year = 2010
ORDER BY infant_mortality asc
LIMIT 5

# Output:

country_name	infant_mortality
Monaco	1.78
Iceland	1.82
Japan	2.3
Luxembourg	2.42
Bermuda	2.46













