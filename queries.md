
# Ex DB University

## Query n. 1
SELECT *
FROM `students`
WHERE `date_of_birth` LIKE '1990-%';

## Query n. 2
SELECT *
FROM `courses`
WHERE `cfu` > 10;

## Query n. 3
SELECT *
FROM `students`
WHERE 2023 - YEAR(`date_of_birth`) > 30;

## Query n. 4
SELECT *
FROM `courses`
WHERE `period` = 'I semestre'
AND `year` = 1;

## Query n. 5


## Query n. 6


## Query n. 7


## Query n. 8