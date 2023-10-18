
# Ex DB University - pt 2

## Group by

### 1. Contare quanti iscritti ci sono stati ogni anno

```sql

SELECT YEAR(`enrolment_date`) AS enrolment_year, COUNT(*) AS number_of_enrolled
FROM `students`
GROUP BY YEAR(`enrolment_date`);

```

### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql

SELECT `office_address`, COUNT(*) AS number_of_teachers
FROM `teachers`
GROUP BY `office_address`;

```

### 3. Calcolare la media dei voti di ogni appello d'esame

```sql

SELECT `exam_id`, AVG(`vote`) AS average_vote
FROM `exam_student`
GROUP BY `exam_id`;

```

### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql

SELECT `department_id`, COUNT(*) AS number_of_degrees
FROM `degrees`
GROUP BY `department_id`;

```


## Joins

### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql

SELECT `students`.*, `degrees`.`name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

```

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql


```

### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql


```

### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql


```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql


```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql


```

## BONUS
### Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql


```