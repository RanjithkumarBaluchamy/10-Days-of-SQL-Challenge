### Type of Triangle
Write a query identifying the type of each record in the TRIANGLES table using its three side lengths. Output one of the following statements for each record in the table:

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

## The PADS

Generate the following two result sets:

Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical (i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

There are total [occupation_count] [occupation]s.
where [occupation_count] is the number of occurrences of an occupation in OCCUPATIONS and [occupation] is the lowercase occupation name. If more than one Occupation has the same [occupation_count], they should be ordered alphabetically.

```sql
SELECT CONCAT(Name, '(', LEFT(Occupation, 1), ')')
FROM OCCUPATIONS
ORDER BY Name;

SELECT CONCAT('There are total ', COUNT(Occupation), ' ', LOWER(Occupation), 's.')
FROM OCCUPATIONS
GROUP BY Occupation
ORDER BY COUNT(Occupation), Occupation;
```

### ** You are given a table, BST, containing two columns: N and P, where N represents the value of a node in Binary Tree, and P is the parent of N.


### Input Format

The OCCUPATIONS table is described as follows:
| Colum | Type   |
|----|--------|
| N  | Integer |
| P  | Integer |


Write a query to find the node type of Binary Tree ordered by the value of the node. Output one of the following for each node:

Root: If node is root node.
Leaf: If node is leaf node.
Inner: If node is neither root nor leaf node.
### Sample Input

| Name      | Occupation|
|-----------|---------|
| 1  | 2  |
| 3     | 2  |
| 6     | 8  |
| 9     | 8  |
| 2    | 5  |
| 8     | 5  |
| 5 | null  |

### Sample output
1 Leaf
2 Inner
3 Leaf
5 Root
6 Leaf
8 Inner
9 Leaf

### Explaination
The Binary Tree below illustrates the sample:
![image](https://user-images.githubusercontent.com/42794483/218974480-cda608b0-8b5c-4709-b630-ae57ee8d838d.png)


### SOLUTION
``/*
Enter your query here.
*/
SELECT
    N,
    CASE 
        WHEN P IS NULL THEN 'Root'
        ELSE CASE 
            WHEN N IN (SELECT DISTINCT P FROM BST) THEN 'Inner'
            ELSE 'Leaf'
        END
    END 
FROM BST
ORDER BY N ASC;``
