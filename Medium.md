@fkibgldxtdbmzhd1

## Q1
Query the two cities in STATION with the shortest and longest CITY names, as well as their respective lengths (i.e.: number of characters in the name). 
If there is more than one smallest or largest city, choose the one that comes first when ordered alphabetically.

SELECT TOP 1 CITY, LEN(CITY)
FROM STATION
ORDER BY LEN(CITY),city;
SELECT TOP 1 CITY, LEN(CITY)
FROM STATION
ORDER BY LEN(CITY) desc,city;

Note: Just don't use union

## Q2

Write a query identifying the type of each record in the TRIANGLES table using its three side lengths.
Output one of the following statements for each record in the table

SELECT

CASE
    WHEN A+B<=C OR B+C<=A OR A+C<=B THEN 'Not A Triangle'
    WHEN A=B AND B=C THEN 'Equilateral'
    WHEN A=B OR B=C OR C=A THEN 'Isosceles'
    WHEN A!=B AND B!=C AND A!=C THEN 'Scalene'
END

FROM TRIANGLES

Note: Not a traingle comes first

## Q3

Query an alphabetically ordered list of all names in OCCUPATIONS, immediately followed by the first letter of each profession as a parenthetical 
(i.e.: enclosed in parentheses). For example: AnActorName(A), ADoctorName(D), AProfessorName(P), and ASingerName(S).
Query the number of ocurrences of each occupation in OCCUPATIONS. Sort the occurrences in ascending order, and output them in the following format:

SELECT CONCAT(NAME,'(',LEFT(OCCUPATION,1),')')
FROM OCCUPATIONS
ORDER BY CONCAT(NAME,'(',LEFT(OCCUPATION,1),')');

SELECT (CONCAT('There are a total of ',CONVERT(CHAR,(COUNT(OCCUPATION))),' ',LOWER(OCCUPATION),'s.'))
FROM OCCUPATIONS
GROUP BY OCCUPATION
ORDER BY COUNT(OCCUPATION),OCCUPATION;

Note: Pay attentio to capitals and punctuations

## Q4

Samantha was tasked with calculating the average monthly salaries for all employees in the EMPLOYEES table, but did not realize her keyboard's  key was broken until after completing the calculation. She wants your help finding the difference between her miscalculation (using salaries with any zeros removed), and the actual average salary.

Write a query calculating the amount of error (i.e.:  average monthly salaries), and round it up to the next integer.

SELECT (AVG(SALARY)-AVG(CONVERT(INT,REPLACE(CONVERT(CHAR,SALARY),'0',''))))+1
FROM EMPLOYEES


## Q5

SELECT DOCTOR,PROFESSOR, SINGER, ACTOR
FROM
(SELECT ROW_NUMBER() OVER (PARTITION BY OCCUPATION ORDER BY NAME)
, NAME, OCCUPATION FROM OCCUPATIONS
) T1
PIVOT
(MAX(NAME) FOR OCCUPATION IN (SELECT DOCTOR,PROFESSOR, SINGER, ACTOR))
AS P1

Note: When both rows are strings use row_number to pivot

## Q6
We define an employee's total earnings to be their monthly MONTHS*SALARY worked, and the maximum total earnings to be the maximum total earnings for any employee in the Employee table. Write a query to find the maximum total earnings for all employees as well as the total number of employees who have maximum total earnings. Then print these values as  space-separated integers.

WITH MAX_SAL AS
(
SELECT MAX(MONTHS*SALARY) AS MAX_SALARY
FROM EMPLOYEE
)

SELECT  MAX(MONTHS*SALARY),COUNT(EMPLOYEE_ID)
FROM EMPLOYEE
WHERE (MONTHS*SALARY) = (SELECT * FROM MAX_SAL)

## Q7
Consider A and B to be two points on a 2D plane where  are the respective minimum and maximum values of Northern Latitude (LAT_N) and  are the respective minimum and maximum values of Western Longitude (LONG_W) in STATION.

SELECT ROUND(SQRT(POWER((MAX(LAT_N)-MIN(LAT_N)),2) + POWER((MAX(LONG_W)-MIN(LONG_W)),2)),4)
FROM STATION

Note: Use Power()

## Q8
A median is defined as a number separating the higher half of a data set from the lower half. Query the median of the Northern Latitudes (LAT_N) from STATION and round your answer to  decimal places.

WITH LAT_SORT AS
(SELECT TOP 500 LAT_N, ROW_NUMBER() OVER (ORDER BY LAT_N) AS RN
FROM STATION
ORDER BY LAT_N DESC)

SELECT 
CAST(LAT_N AS DECIMAL(10,4))
FROM LAT_SORT
WHERE RN = (SELECT CEILING(MAX(RN)/2)+1 FROM LAT_SORT)

Note: There is no function in SQL to calculate the median directly, so need to sort and take the middle element
