## 1-> Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
``
SELECT `students`.`name` AS `students_name`,`students`.`surname` AS `students_surname`,`students`.`registration_number`, `degrees`.`name` AS `degrees_name`
FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia";
``
## 2-> Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT `departments`.`name` AS `departments_name`, `degrees`.`name` AS `degrees_name`, `degrees`.`level` 
FROM `degrees`
JOIN `departments`	
ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = "magistrale"
AND `departments`.`name` = "Dipartimento di Neuroscienze";

## 3-> Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
--Versione 1--
``
SELECT `teachers`.`name`, `teachers`.`surname`, `teachers`.`id`, `courses`.`name` AS `courses_name`
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`name` = "Fulvio"
AND `teachers`.`surname` = "Amato";
``

--Versione 2--
``
SELECT `teachers`.`name`, `teachers`.`surname`, `teachers`.`id`, `courses`.`name` AS `courses_name`
FROM `courses`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`
WHERE `teachers`.`id` = 44;
``

## 4-> Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
``
SELECT `students`.`name` AS `students_name`, `students`.`surname` AS `students_surname`, `students`.`registration_number`, `degrees`.`name` AS `degrees_name`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `departments`.`name` AS `departments_name` 
FROM `students` 
JOIN `degrees` 
ON `students`.`degree_id` = `degrees`.`id` 
JOIN `departments` 
ON `degrees`.`department_id` = `departments`.`id` 
ORDER BY `students`.`name`, `students`.`surname`;
``

## 5-> Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
``
SELECT `degrees`.`name` AS `degrees_name`, `courses`.`name` AS `courses_name`, `teachers`.`surname` AS `teachers_surname` , `teachers`.`name` AS `teachers_name` 
FROM `degrees`
JOIN `courses`
ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher`
ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers`
ON `course_teacher`.`teacher_id` = `teachers`.`id`;
``

## 6-> Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
``
SELECT DISTINCT `teachers`.`name` AS `teachers_name`, `teachers`.`surname` AS `teachers_surname`, `courses`.`name` AS `courses_name`, `degrees`.`name` AS `degrees_name`, `departments`.`name` AS `depart_name`
FROM `teachers`
JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = "Dipartimento di Matematica";
``

## 7-> BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo.Successivamente, filtrare i tentativi con voto minimo 18.
``
SELECT `students`.`surname`,`students`.`name`,`exam_student`.`vote`,MAX(`exam_student`.`vote`) AS `max_vote`,`exams`.`id` AS `exams_id`,`courses`.`name` AS `courses_name`,`courses`.`cfu`, COUNT(`exam_student`.`student_id`) AS `tries`
FROM `students` 
JOIN `exam_student`
ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams`
ON `exam_student`.`exam_id` = `exams`.`id`
JOIN `courses`
ON `exams`.`course_id` = `courses`.`id`
GROUP BY `students`.`id`, `exam_student`.`exam_id`
HAVING `exam_student`.`vote` >= 18;
``