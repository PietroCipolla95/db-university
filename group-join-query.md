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