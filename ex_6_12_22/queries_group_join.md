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
SELECT `exam_id` as `id appello`, AVG(`vote`) as `avarage`
FROM `exam_student` 
GROUP BY `id appello`;

## Contare quanti corsi di laurea ci sono per ogni dipartimento
SELECT `department_id` as `numero dipartimento`, COUNT(id) as `numero di corsi di laurea` 
FROM `degrees` 
GROUP BY `numero dipartimento`;

## JOIN
## Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT `students`.`*`, `degrees`.`name` 
FROM `students` 
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

## Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

## Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

## Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
## Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
## Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)
## BONUS: Selezionare per ogni studente quanti tentativi d’esame ha sostenuto per superare ciascuno dei suoi esami