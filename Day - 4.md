### ** Pivot the Occupation column in OCCUPATIONS so that each Name is sorted alphabetically and displayed underneath its corresponding Occupation. The output column headers should be Doctor, Professor, Singer, and Actor, respectively.

Note: Print NULL when there are no more names corresponding to an occupation.

### Input Format

The OCCUPATIONS table is described as follows:
| Column      | Type   |
|-------------|--------|
| Name        | String |
| Occupation  | String |


Occupation will only contain one of the following values: Doctor, Professor, Singer or Actor.
### Sample Input

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
Jenny    Ashley     Meera  Jane
Samantha Christeen  Priya  Julia
NULL     Ketty      NULL   Maria

### Explaination
The first column is an alphabetically ordered list of Doctor names.
The second column is an alphabetically ordered list of Professor names.
The third column is an alphabetically ordered list of Singer names.
The fourth column is an alphabetically ordered list of Actor names.
The empty cell data for columns with less than the maximum number of names per occupation (in this case, the Professor and Actor columns) are filled with NULL values.

### SOLUTION
``SELECT 
    MAX(CASE WHEN Occupation = 'Doctor' THEN Name END) AS Doctor,
    MAX(CASE WHEN Occupation = 'Professor' THEN Name END) AS Professor,
    MAX(CASE WHEN Occupation = 'Singer' THEN Name END) AS Singer,
    MAX(CASE WHEN Occupation = 'Actor' THEN Name END) AS Actor
FROM (
  SELECT 
    ROW_NUMBER() OVER (PARTITION BY Occupation ORDER BY Name) rn, 
    Name, 
    Occupation 
  FROM Occupations 
  GROUP BY Occupation, Name
) AS tab2 
GROUP BY rn;``




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
