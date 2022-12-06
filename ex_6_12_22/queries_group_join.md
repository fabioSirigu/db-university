Group by:
## Contare quanti iscritti ci sono stati ogni anno
SELECT COUNT(`id`) AS `total_student`, YEAR(`enrolment_date`) AS `year`
FROM `students`
GROUP BY `year`;

## Contare gli insegnanti che hanno l'ufficio nello stesso edificio
SELECT COUNT(`id`) AS `total_teachers`, `office_address` AS `address`
FROM `teachers`
GROUP BY `address`;

## Calcolare la media dei voti di ogni appello d'esame
SELECT `exam_id` AS `id appello`, AVG(`vote`) AS `avarage`
FROM `exam_student` 
GROUP BY `id appello`;

## Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT `department_id` AS `numero dipartimento`, COUNT(id) AS `numero di corsi di laurea` 
FROM `degrees` 
GROUP BY `numero dipartimento`;

## JOIN
## Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `students`.`*`, `degrees`.`name` AS `degrees name`
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

## Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze
SELECT `degrees`.`*`, `departments`.`name` 
FROM `degrees` 
JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` 
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `degrees`.`level` = 'magistrale';
## Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
SELECT `courses`.`*` , `teachers`.`name`, `teachers`.`surname` 
FROM `course_teacher` 
JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` 
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
WHERE `teachers`.`id` = 44;

## Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
SELECT `students`.`name` AS `Student Name`,`students`.`surname` AS `Student Surname`, `degrees`.`*` , `departments`.`name` AS `Department Name`
FROM `degrees` 
JOIN `students` ON `degrees`.`id` = `students`.`degree_id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

## Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
SELECT  `degrees`.`*`, `teachers`.`name` AS `name teacher`, `teachers`.`surname` AS `surname teacher`, `courses`.`name` AS `name course` 
FROM `course_teacher` 
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id`;
## Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
SELECT DISTINCT `teachers`.`*`, `departments`.`name` AS `Department Name` 
FROM `course_teacher` 
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id` 
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id` 
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
WHERE `departments`.`name` = 'Dipartimento di Matematica';

## BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami
