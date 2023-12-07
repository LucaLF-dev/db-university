## 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
SELECT  `students`.`id` as 'id',
		`students`.`name` as 'Nome_studente',
		`students`.`surname` as 'Cognome_studente',
		`degrees`.`name` as 'Iscritto_al_corso_di laurea'
FROM `students`
INNER JOIN `degrees`
	ON `degrees`.`id` = `students`.`degree_id`
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';


## 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

SELECT  `departments`.`name` as 'Nome_dipartimento',
        `degrees`.`name` as 'Nome_del_corso'
FROM `degrees`
INNER JOIN `departments`
	ON `departments`.`id` = `degrees`.`department_id`
WHERE (`departments`.`name` = 'Dipartimento di Neuroscienze'
AND `degrees`.`name` LIKE 'Corso di laurea Magistrale %');


## 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT  `teachers`.`id` AS 'id',
        `teachers`.`name` AS 'Nome',
        `teachers`.`surname` AS 'Cognome',
		`course_teacher`.`course_id` AS 'id_del_corso'
FROM `teachers`
INNER JOIN `course_teacher`
	ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = '44';


## 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT  `students`.`surname` AS 'Cognome_dello_studente',
		`students`.`name` AS 'Nome_dello_studente',
        `degrees`.`name` AS 'Corso_di_Laurea',
        `departments`.`name` AS 'Nome_dipartimento'
FROM `students`
INNER JOIN `degrees`
	ON `students`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
	ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;

## 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT `degrees`.`name` AS 'Corso_di_Laurea',
		`courses`.`description` AS 'Corso',
        `course_teacher`.`course_id` AS 'id_Corso ',
        `course_teacher`.`teacher_id` AS 'id_del_professore',
        `teachers`.`name` AS 'Nome_del_professore',
        `teachers`.`surname` AS 'Cognome_del_professore'
FROM `degrees`
INNER JOIN `courses`
	ON `degrees`.`id` = `courses`.`degree_id`
INNER JOIN `course_teacher`
	ON `courses`.`id` = `course_teacher`.`teacher_id`  
INNER JOIN `teachers`
	ON `teachers`.`id` = `course_teacher`.`teacher_id`; 

## 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

SELECT `departments`.`name` AS 'Nome_del_dipartimento',
		`teachers`.`name` AS 'Nome_del_professore',
        `teachers`.`surname` AS 'Cognome_del_professore',
    	`course_teacher`.`teacher_id` AS 'id_del_professore'
FROM `departments`
LEFT JOIN `degrees`
	ON `departments`.`id` = `degrees`.`department_id`
LEFT JOIN `courses`
	ON `degrees`.`id` = `courses`.`degree_id`
LEFT JOIN `course_teacher`
	ON `courses`.`id` = `course_teacher`.`course_id`
LEFT JOIN `teachers`
	ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `departments`.`name` = 'Dipartimento di Matematica'  
GROUP BY `departments`.`name`,`teachers`.`name`,`teachers`.`surname`,`course_teacher`.`teacher_id`  


