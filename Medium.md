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



## Q6



## Q7



## Q8
