## 1-> Contare quanti iscritti ci sono stati ogni anno
``
SELECT YEAR(`enrolment_date`) AS `year`, 
COUNT(*) AS `subscriber_num` 
FROM `students` 
GROUP BY `year`;
``
## 2-> Contare gli insegnanti che hanno l'ufficio nello stesso edificio
``
SELECT COUNT(*) AS `teachers_num`,`office_number` 
FROM `teachers` 
WHERE `office_number` = `office_number` 
GROUP BY(`office_number`);
``
## 3-> Calcolare la media dei voti di ogni appello d'esame
## 4-> Contare quanti corsi di laurea ci sono per ogni dipartimento
