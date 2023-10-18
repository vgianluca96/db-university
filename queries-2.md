
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

SELECT `students`.*, `degrees`.`name` AS `degree_name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

```

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql

SELECT `degrees`.*, `departments`.`name` AS `department_name`
FROM `degrees`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze';

```

### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql

SELECT `courses`.*, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
FROM `teachers`
JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
WHERE `teachers`.`id` = 44;

```

### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql

SELECT `students`.*, `degrees`.`name` AS `degree_name`, `departments`.`name` AS `department_name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname` ASC,`students`.`name` ASC;

```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql

SELECT `degrees`.*, `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`, `teachers`.`surname` AS `teacher_surname`
FROM `courses`
JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
ORDER BY `degrees`.`name` ASC;

```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql

SELECT DISTINCT `teachers`.*, `departments`.`name` AS `department_name`
FROM `teachers`
JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'
ORDER BY `teachers`.`surname` ASC, `teachers`.`name` ASC;

```

## BONUS
### Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

**Prima eseguo il seguente comando per disattivare opzione ONLY_FULL_GROUP_BY**
```sql

SET GLOBAL sql_mode=(SELECT REPLACE(@@sql_mode,'ONLY_FULL_GROUP_BY',''));

```

**Poi eseguo la query**
```sql

SELECT `students`.`name` as `student_name`, `students`.`surname` as `student_surname`, `courses`.`id` AS `course_id`, `courses`.`name` AS `course_name`, COUNT(`exams`.`course_id`) AS `tentatives`, MAX(`exam_student`.`vote`) AS `max_vote`
FROM `exam_student`
JOIN `students`
ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams`
ON `exams`.`id` = `exam_student`.`exam_id`
JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
WHERE `exam_student`.`vote` >= 18
GROUP BY `exams`.`course_id`, `students`.`name`
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

```