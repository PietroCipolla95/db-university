## GROUP

1 Contare quanti iscritti ci sono stati ogni anno

```sql

SELECT COUNT(id), YEAR(`enrolment_date`)
FROM `students`
GROUP BY YEAR(`enrolment_date`);

```

2 Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql

SELECT COUNT(id), `office_address`
FROM `teachers`   
GROUP BY `office_address`;

```

3 Calcolare la media dei voti di ogni appello d'esame

```sql

SELECT `exam_id`, AVG(`vote`)
FROM `exam_student`
GROUP BY `exam_id`;

```

4 Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql

SELECT COUNT(id) AS number_of_degrees, `department_id`
FROM `degrees`
GROUP BY `department_id`;

```


## JOIN

1 Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql

SELECT `students`.`name`, `students`.`surname`, `students`.`registration_number`, `degrees`.`name` AS degree
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

```

2 Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql

SELECT `degrees`.`name`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `departments`.`name`, `departments`.`address`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = 'magistrale' AND `departments`.`name` = 'Dipartimento di Neuroscienze';

```

3 Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql

SELECT `courses`.`name` AS course_name, `courses`.`cfu`, `teachers`.name AS teacher_name, `teachers`.`surname` AS teacher_surname
FROM `course_teacher`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
WHERE `teachers`.`id` = 44;

```

4 Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql

SELECT `students`.`name`, `students`.`surname`, `degrees`.`name` AS degree_name, `departments`.`name` AS dep_name
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
ORDER BY `students`.name ASC, `students`.`surname` ASC;

```

5 Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql

SELECT `degrees`.`name` AS degree_name, `courses`.`name` AS course_name, `teachers`.name AS teacher_name, `teachers`.`surname` AS teacher_surname
FROM `course_teacher`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`
ORDER BY `degrees`.name ASC;

```

