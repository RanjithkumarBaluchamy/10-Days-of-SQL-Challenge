## 1. Aggregations - Count Function

Query a count of the number of cities in CITY with populations larger than 100,000.

### Input Format

The CITY table is described as follows: 

| Field      | Type|
|-----------|---------|
| ID  | NUMBER  |
| NAME     | VARCHAR2(17)  |
| COUNTRYCODE     | VARCHAR2(3)  |
| DISTRICT     | VARCHAR2(20)  |
| POPULATION    | NUMBER  |

```sql
SELECT COUNT(NAME)
FROM CITY
WHERE POPULATION > 100000;
```

## 2. Sum Function

Query the total population of all cities in CITY where District is California.

```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE DISTRICT='California';
```

## 3. Averages

Query the average population of all cities in CITY where District is California.

```sql
SELECT AVG(POPULATION)
FROM CITY
WHERE DISTRICT='California';
```

## 4. Average Population

Query the average population for all cities in CITY, rounded down to the nearest integer.

```sql
SELECT FLOOR(AVG(POPULATION))
FROM CITY;
```

## 5. Japan Population

Query the sum of the populations for all Japanese cities in CITY. The COUNTRYCODE for Japan is JPN.

```sql
SELECT SUM(POPULATION)
FROM CITY
WHERE COUNTRYCODE='JPN';
```

## 6. Population Density Difference

Query the difference between the maximum and minimum populations in CITY.

```sql
SELECT MAX(POPULATION)-MIN(POPULATION)
FROM CITY;
```

## 7. Weather Observation Station 2

Query the sum of LAT_N, followed by the sum of LONG_W, from STATION. The two results should be separated by a space and rounded to 22 decimal places.

## Input Format

The STATION table is described as follows:

![image](https://user-images.githubusercontent.com/42794483/221651321-8bc61486-d80b-4f79-a757-9470661c1055.png)

where LAT_N is the northern latitude and LONG_W is the western longitude.

## Output Format
Your results must be in the form:
lat lon

**Solution**
```sql
SELECT ROUND(SUM(LAT_N), 2), ROUND(SUM(LONG_W), 2)
FROM STATION
```

## 8. Weather Observation Station 13

Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than 38.788038.7880 and less than 137.2345137.2345. Truncate your answer to 44 decimal places.

Query the sum of Northern Latitudes (LAT_N) from STATION having values greater than  and less than . Truncate your answer to  decimal places.

## Input Format

The STATION table is described as follows:

![image](https://user-images.githubusercontent.com/42794483/221651833-d8666d64-e874-49a2-9e2f-4313c3789c4d.png)

where LAT_N is the northern latitude and LONG_W is the western longitude.

**Solution**

```sql
SELECT ROUND(SUM(LAT_N), 4)
FROM STATION
WHERE LAT_N>38.7880 AND LAT_N<137.2345;
```

## 9. Weather Observation Station 14

Query the greatest value of the Northern Latitudes (LAT_N) from STATION that is less than 137.2345137.2345. Truncate your answer to 44 decimal places.
## Input Format

The STATION table is described as follows:

![image](https://user-images.githubusercontent.com/42794483/222670780-396bef85-4c5d-4a1a-a9be-48c4704bf115.png)

where LAT_N is the northern latitude and LONG_W is the western longitude.

```sql
SELECT ROUND(MAX(LAT_N), 4)
FROM STATION
WHERE LAT_N<137.2345;
```

## 10. Weather Observation Station 15

Query the Western Longitude (LONG_W) for the largest Northern Latitude (LAT_N) in STATION that is less than 137.2345137.2345. Round your answer to 44 decimal places.

## Input Format

The STATION table is described as follows:

![image](https://user-images.githubusercontent.com/42794483/222671810-49bc31b8-2eaf-4cb9-93bf-b96332e18b23.png)

where LAT_N is the northern latitude and LONG_W is the western longitude.

```sql
SELECT ROUND(LONG_W, 4)
FROM STATION
WHERE LAT_N<137.2345
ORDER BY LAT_N DESC
LIMIT 1;
```

## 11. Weather Observation Station 16

Query the smallest Northern Latitude (LAT_N) from STATION that is greater than 38.778038.7780. Round your answer to 44 decimal places.

```sql
SELECT ROUND(LAT_N, 4)
FROM STATION
WHERE LAT_N>38.7780
ORDER BY LAT_N
LIMIT 1;
```

## 12. Weather Observation Station 17

Query the Western Longitude (LONG_W) for the smallest Northern Latitude (LAT_N) in STATION that is greater than 38.778038.7780. Round your answer to 44 decimal places.

```sql
SELECT ROUND(LONG_W, 4)
FROM STATION
WHERE LAT_N>38.7780
ORDER BY LAT_N
LIMIT 1;
```

## 12. Weather Observation Station 18

Consider P1(a,b) and P2(c,d) to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

Query the Manhattan Distance between points P1P1 and P2P2 and round it to 44 decimal digits.

```sql
SELECT ROUND(ABS(MAX(LAT_N)-MAX(LONG_W))+ABS(MIN(LAT_N)-MIN(LONG_W)), 4)
FROM STATION;
```

## 12. Weather Observation Station 19

Consider P1(a,b) and P2(c,d) to be two points on a 2D plane where (a,b) are the respective minimum and maximum values of Northern Latitude (LAT_N) and (c,d) are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

Query the Euclidean Distance between points P1P1 and P2P2 and round it to 44 decimal digits.

```sql
SELECT ROUND(SQRT(POW(MAX(LAT_N)-MAX(LONG_W), 2) + POW(MIN(LAT_N)-MIN(LONG_W), 2)), 4)
FROM STATION;
```

## 12. Weather Observation Station 20

A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to 44 decimal places.

```sql
SELECT ROUND(LAT_N,4)
FROM STATION
ORDER BY (LAT_N) LIMIT 249,1
```

## 13. The Blunder

Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's 00 key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeroes removed), and the actual average salary.

Write a query calculating the amount of error (i.e.: actual???miscalculated average monthly salaries), and round it up to the next integer.

```sql
SELECT CEIL(AVG(Salary)-AVG(CONVERT(REPLACE(convert(Salary, char(4)), '0', ''), UNSIGNED INTEGER)))
FROM EMPLOYEES;
```

## 14. Top Earners

We define an employee's total earnings to be their monthly  worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as  space-separated integers.

## Input Format
The Employee table containing employee data for a company is described as follows:

``SQL
SELECT (salary*months) AS earnings, COUNT(*) as num
FROM employee
GROUP BY earnings
ORDER BY earnings DESC
LIMIT 1;``

### **Weather Observation Station 2 In SQL | HackerRank Solution
Query the following two values from the STATION table:

The sum of all values in LAT_N rounded to a scale of  decimal places.
The sum of all values in LONG_W rounded to a scale of  decimal places.
Input Format

The STATION table is described as follows:
![image](https://user-images.githubusercontent.com/42794483/221170596-5be61c08-921f-42b4-9c5d-cc588333b5b8.png)
where LAT_N is the northern latitude and LONG_W is the western longitude.

## Output Format
Your results must be in the form:
lat lon

**Solution**
``select round(sum(lat_n), 2), round(sum(long_w), 2) 
from station;``
