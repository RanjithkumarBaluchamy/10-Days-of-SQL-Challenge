## 1. Asian Population

Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

```sql
SELECT city.name
FROM city
LEFT JOIN country
ON (city.countrycode = country.code)
WHERE continent = 'Africa';
```

## 2. African Cities

Given the CITY and COUNTRY tables, query the names of all cities where the CONTINENT is 'Africa'.

```sql
SELECT CITY.NAME
FROM CITY JOIN COUNTRY
ON CITY.COUNTRYCODE=COUNTRY.CODE
WHERE CONTINENT='Africa';
```

## 3. Average Population of Each Continent

Given the CITY and COUNTRY tables, query the names of all the continents (COUNTRY.Continent) and their respective average city populations (CITY.Population) rounded down to the nearest integer.

```sql
SELECT COUNTRY.CONTINENT, FLOOR(AVG(CITY.POPULATION))
FROM CITY JOIN COUNTRY
  ON CITY.COUNTRYCODE=COUNTRY.CODE
GROUP BY COUNTRY.CONTINENT;
```

OR

``SELECT continent, FLOOR(AVG(population))
FROM (
    SELECT city.name, continent, city.population AS population
    FROM city
    LEFT JOIN country
    ON (city.countrycode = country.code)
) t
WHERE continent IS NOT NULL
GROUP BY continent ORDER BY continent;``

## 4. Average Population of Each Continent

You are given two tables: Students and Grades. Students contains three columns ID, Name and Marks.

![image](https://user-images.githubusercontent.com/42794483/220068481-e85e5807-e114-4e3c-8bc2-a1ad8f8dec0e.png)

Grades contains the following data:

![image](https://user-images.githubusercontent.com/42794483/220068527-e11f64f3-518d-488a-bb16-a8919b4851ae.png)

Ketty gives Eve a task to generate a report containing three columns: Name, Grade and Mark. Ketty doesn't want the NAMES of those students who received a grade lower than 8. The report must be in descending order by grade -- i.e. higher grades are entered first. If there is more than one student with the same grade (8-10) assigned to them, order those particular students by their name alphabetically. Finally, if the grade is lower than 8, use "NULL" as their name and list them by their grades in descending order. If there is more than one student with the same grade (1-7) assigned to them, order those particular students by their marks in ascending order.

Write a query to help Eve.

## Sample Input

![image](https://user-images.githubusercontent.com/42794483/220068647-d31251b8-980f-45c4-a2ef-aacf93a1da96.png)

## Sample Output

Maria 10 99
Jane 9 81
Julia 9 88 
Scarlet 8 78
NULL 7 63
NULL 7 68

Note: Print "NULL"  as the name if the grade is less than 8.

## Explanation
Consider the following table with the grades assigned to the students:

![image](https://user-images.githubusercontent.com/42794483/220068741-5aa82fd7-c771-4fa1-a207-e5b2bc5a5530.png)



So, the following students got 8, 9 or 10 grades:
Maria (grade 10)
Jane (grade 9)
Julia (grade 9)
Scarlet (grade 8)

```sql
SELECT CASE 
    WHEN Grades.Grade < 8 THEN 'NULL' 
    ELSE Students.Name 
    END 
, Grades.Grade, Students.Marks 
FROM Students, Grades 
WHERE Students.Marks >= Grades.Min_mark AND Students.Marks <= Grades.Max_mark 
ORDER BY Grades.Grade DESC, Students.Name;
```

## 5. Top Competitors

Julia just finished conducting a coding contest, and she needs your help assembling the leaderboard! Write a query to print the respective hacker_id and name of hackers who achieved full scores for more than one challenge. Order your output in descending order by the total number of challenges in which the hacker earned a full score. If more than one hacker received full scores in same number of challenges, then sort them by ascending hacker_id.

### Input Format

The following tables contain contest data:

Hackers: The hacker_id is the id of the hacker, and name is the name of the hacker. 

![image](https://user-images.githubusercontent.com/42794483/220049991-418f22a0-b848-4c39-ba69-822054d353f4.png)

Difficulty: The difficult_level is the level of difficulty of the challenge, and score is the score of the challenge for the difficulty level. 

![image](https://user-images.githubusercontent.com/42794483/220050053-2adbae8c-9405-48d9-89f0-87575e0e780a.png)

Challenges: The challenge_id is the id of the challenge, the hacker_id is the id of the hacker who created the challenge, and difficulty_level is the level of difficulty of the challenge. 

![image](https://user-images.githubusercontent.com/42794483/220050265-08ed65ea-499f-45ba-a9fa-06454774f04f.png)

Submissions: The submission_id is the id of the submission, hacker_id is the id of the hacker who made the submission, challenge_id is the id of the challenge that the submission belongs to, and score is the score of the submission.

![image](https://user-images.githubusercontent.com/42794483/220050366-0f3dad3d-8373-4445-8b29-2421748cb28e.png)

## Sample Input
Hackers Table: 

![image](https://user-images.githubusercontent.com/42794483/220050442-4dbe2e58-fddd-4bd9-af8c-cce9069c4832.png)

Difficulty Table: 

![image](https://user-images.githubusercontent.com/42794483/220051091-e0a47787-7682-43a5-8a88-014d1f9fb895.png)

Challenges Table: 

![image](https://user-images.githubusercontent.com/42794483/220051008-fd63819c-6320-4880-a8a1-a471e06189b0.png)

Submissions Table: 

![image](https://user-images.githubusercontent.com/42794483/220050963-3daeceec-e5eb-421b-b12f-d81288dec9de.png)

### Sample Output
90411 Joe
### Explanation
Hacker 86870 got a score of 30 for challenge 71055 with a difficulty level of 2, so 86870 earned a full score for this challenge.
Hacker 90411 got a score of 30 for challenge 71055 with a difficulty level of 2, so 90411 earned a full score for this challenge.
Hacker 90411 got a score of 100 for challenge 66730 with a difficulty level of 6, so 90411 earned a full score for this challenge.
Only hacker 90411 managed to earn a full score for more than one challenge, so we print the their hacker_id and name as 2 space-separated values.

**MySQL**
```sql
SELECT t.hacker_id, h.name
FROM (
    SELECT 
        s.hacker_id AS hacker_id, 
        COUNT(*) AS cnt
    FROM submissions s 
    LEFT JOIN challenges c 
        ON (s.challenge_id = c.challenge_id)
    lEFT JOIN difficulty d
        ON (c.difficulty_level = d.difficulty_level)
    WHERE 
        s.score = d.score
    GROUP BY 
        hacker_id
    HAVING cnt > 1
) t 
LEFT JOIN hackers h
ON (t.hacker_id = h.hacker_id)
ORDER BY t.cnt DESC, t.hacker_id ASC;
```

OR
**DB2**
``
SELECT Submissions.hacker_id, Hackers.name from Hackers, Submissions, Challenges, Difficulty
WHERE Submissions.score = Difficulty.score
AND Hackers.hacker_id = Submissions.hacker_id 
AND Submissions.challenge_id = Challenges.challenge_id 
AND Challenges.difficulty_level = Difficulty.difficulty_level
GROUP BY Submissions.hacker_id, Hackers.name
HAVING count(*) > 1 
ORDER BY count(*) DESC, Submissions.hacker_id ASC;``

##  5 Population census
Given the CITY and COUNTRY tables, query the sum of the populations of all cities where the CONTINENT is 'Asia'.

Note: CITY.CountryCode and COUNTRY.Code are matching key columns.

### Input Format

The CITY and COUNTRY tables are described as follows:

![image](https://user-images.githubusercontent.com/42794483/220911707-13f59514-e9f2-425e-b550-dab5c5cb76e2.png) ![image](https://user-images.githubusercontent.com/42794483/220911759-dfcc1c25-b97d-4fe5-925e-5fa644036ac5.png)

**Solution**
```SELECT SUM(city.population)
FROM city
LEFT JOIN country
ON (city.countrycode = country.code)
WHERE continent = 'Asia';```
