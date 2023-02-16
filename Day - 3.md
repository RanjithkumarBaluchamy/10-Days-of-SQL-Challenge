###**Query a count of the number of cities in CITY with populations larger than 100,000.**
### Input Format
The CITY table is described as follows:
| Field       | Type         |
|-------------|--------------|
| ID          | NUMBER       |
| NAME        | VARCHAR2(17) |
| COUNTRYCODE | VARCHAR2(3)  |
| DISTRICT    | VARCHAR2(20) |
| POPULATION  | NUMBER       |

**SOLUTION**
``SELECT COUNT(POPULATION) FROM CITY
WHERE POPULATION > 100000;``


###**Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

Equilateral: It's a triangle with  sides of equal length.
Isosceles: It's a triangle with  sides of equal length.
Scalene: It's a triangle with  sides of differing lengths.
Not A Triangle: The given values of A, B, and C don't form a triangle.
Input Format

The TRIANGLES table is described as follows:

| Column| Type    |
|-------|---------|
| A     | Integer |
| B     | Integer |
| C     | Integer |


Each row in the table denotes the lengths of each of a triangle's three sides.

### Sample Input

| A       | B   | C    |
|---------|-----|------|
| 20      | 20  | 23 |
| 20      | 20  | 20 |
| 20      | 21  | 21 |
| 13       |14   | 30 |

**Solution**

``SELECT CASE
WHEN a < c and b < c and a + b <= c THEN 'Not A Triangle'
WHEN a < b and c < b and a + c <= b THEN 'Not A Triangle'
WHEN b < a and c < a and b + c <= a THEN 'Not A Triangle'
WHEN a = b and b = c THEN 'Equilateral'
WHEN a = b or b = c or a = c THEN 'Isosceles'
ELSE 'Scalene' END
FROM Triangles;``


###**Generate the following two result sets:

Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

There are a total of [occupation_count] [occupation]s.
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

Note: There will be at least two entries in the table for each type of occupation.

### Input Format

The OCCUPATIONS table is described as follows:

| Column     | Type   |
|---------|-----|
| Nmae      | String  |
| Occupation  | String  |

Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.

### Sample Input

An OCCUPATIONS table that contains the following records:

| Name      | Occupation|
|-----------|---------|
| Samantha  | String  |
| Julia     | String  |
| Maria     | String  |
| Meera     | String  |
| Ashely    | String  |
| Ketty     | String  |
| Christeen | String  |
| Jane      | String  |
| Jenny     | String  |
| Priya     | String  |


### Sample output
Ashely(P)
Christeen(P)
Jane(A)
Jenny(D)
Julia(A)
Ketty(P)
Maria(A)
Meera(S)
Priya(S)
Samantha(D)
There are a total of 2 doctors.
There are a total of 2 singers.
There are a total of 3 actors.
There are a total of 3 professors.

### Explanation

The results of the first query are formatted to the problem description's specifications.
The results of the second query are ascendingly ordered first by number of names corresponding to each profession (2 < 2 < 3 < 3), and then alphabetically by profession (doctor < singer, and actor < professor). 


**Solution**
``SELECT (name || '(' || SUBSTR(occupation,1,1) || ')') FROM occupations ORDER BY name;
SELECT ('There are a total of ' || COUNT(occupation) || ' ' || LOWER(occupation) || 's' || '.') FROM occupations GROUP BY occupation ORDER BY COUNT(occupation), occupation ASC;
``
