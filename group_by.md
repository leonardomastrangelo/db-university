## 1-> Contare quanti iscritti ci sono stati ogni anno
``
SELECT YEAR(`enrolment_date`) AS `year`, 
COUNT(*) AS `subscriber_num` 
FROM `students` 
GROUP BY `year`;
``
## 2-> Contare gli insegnanti che hanno l'ufficio nello stesso edificio
``
SELECT COUNT(*) AS `teachers_num`,`office_address` 
FROM `teachers` 
GROUP BY(`office_address`);
``
## 3-> Calcolare la media dei voti di ogni appello d'esame
``
SELECT ROUND(AVG(`vote`)) AS `avg_grades`, `exam_id` 
FROM `exam_student` 
GROUP BY `exam_id`;
``
## 4-> Contare quanti corsi di laurea ci sono per ogni dipartimento
``
SELECT `department_id`, 
COUNT(*) AS `degrees_num` 
FROM `degrees` 
GROUP BY(`department_id`);
``