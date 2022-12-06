## Query Todo:
## Selezionare tutti gli studenti nati nel 1990 (160)
SELECT * 
FROM `students` 
WHERE year(`date_of_birth`) like '1990';

## Selezionare tutti i corsi che valgono più di 10 crediti (479)
SELECT * 
FROM `courses` 
WHERE `cfu` > 10;

## Selezionare tutti gli studenti che hanno più di 30 anni
SELECT * 
FROM `students` 
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30;

## Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)
SELECT * 
FROM `courses` 
WHERE `period` = 'I semestre' and `year` = 1;

## Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)
SELECT * 
FROM `exams` 
WHERE `date` = '2020-06-20' and HOUR(`hour`) > '14';

## Selezionare tutti i corsi di laurea magistrale (38)
SELECT * 
FROM `degrees` 
WHERE `level` = 'magistrale';

## Da quanti dipartimenti è composta l'università? (12)
SELECT COUNT(id) as numeroDipartimenti 
FROM `departments`;
## Quanti sono gli insegnanti che non hanno un numero di telefono? (50)
SELECT COUNT(id) as insegnantiSenzaNumero 
FROM `teachers` 
WHERE `phone` is NULL;

## Selezionare tutti i corsi del Corso di Laurea in Informatica (22)
SELECT `courses`.`id`, `courses`.`name`,`courses`.`period`,`courses`.`year`,`courses`.`cfu`,`courses`.`website`,`degrees`.`name` as `degrees_name`
FROM `courses`
JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Informatica';

## Selezionare le informazioni sul corso con id = 144, con tutti i relativi appelli d’esame
SELECT `courses`.`id`, `courses`.`name`,`courses`.`period`,`courses`.`year`,`courses`.`cfu`,`courses`.`website`,`exames`.`id` AS `exams_id`, `exames`.`date`,`exames`.`hour`,`exames`.`location`,`exames`.`address`
FROM `courses`
JOIN `exams`
ON `courses`.`id` = `exams`.`course_id`
WHERE `courses`.`id` = 144;

## Selezionare a quale dipartimento appartiene il Corso di Laurea in Diritto dell'Economia (Dipartimento di Scienze politiche, giuridiche e studi internazionali)
SELECT `departments`.`*`
FROM `departments`
JOIN `degrees`
ON `departments`.`id` = `degrees`.`departments_id`
WHERE `degrees`.`name` = 'Laurea in Diritto dell\'Economia';

## Selezionare tutti gli appelli d'esame del Corso di Laurea Magistrale in Fisica del primo anno
SELECT `teachers`.`name`,`teachers`.`surname`,`teachers`.`email`, `teachers`.`office_address`, `teachers`.`office_number`
FROM `teachers`
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `courses`.`id` = `course_teacher`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Laurea Magistrale in Fisica' AND `courses`.`year`=1;

## Selezionare tutti i docenti che insegnano nel Corso di Laurea in Lettere (21)
SELECT DISTINCT `courses`.`name`,`courses`.`period`,`courses`.`cfu`, `exames`.`date`,`exames`.`hour`,`exames`.`location`,`exames`.`address`, `degrees`.`name` as `degree_name`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `exams` ON `exams`.`course_id` = `courses`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Lettere';

## Selezionare il libretto universitario di Mirco Messina (matricola n. 620320)
SELECT `students`.`name`,`students`.`surname`,`students`.`registration_number`,`courses`.`id`,`courses`.`name`,`exams`.`date`,`exam_student`.`vote`
FROM `exam_student`
JOIN `students` ON `students`.`id` = `exam_student`.`student_id`
JOIN `exams` ON `exams`.`id` = `exam_student`.`exam_id`
JOIN `courses` ON `courses`.`id` = `exams`.`course_id`
WHERE `students`.`name` = 'Mirco' AND `students`.`surname` = 'Messina' AND `exam_student`.`vote` >= 18

## Selezionare il voto medio di superamento d'esame per ogni corso, con anche i dati del corso di laurea associato, ordinati per media voto decrescente
SELECT AVG(`exam_student`.`vote`) AS `Avarage_Vote`, `courses`.`name` AS `Course_Name`, `degrees`.`name` AS `Degree_Name`
FROM `exam_student`
JOIN `exams` ON `exam_student`.`exam_id` =  `exams`.`id`
JOIN `courses` ON `exams`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
WHERE `exam_student`.`vote` >= 18
GROUP BY `courses`.`id`
ORDER BY `Avarage_Vote` DESC;


 


