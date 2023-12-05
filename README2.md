# db-university 
### GROUP-BY
1. Contare quanti iscritti ci sono stati ogni anno -> SELECT YEAR(`enrolment_date`) as `enrollment_year`, COUNT(*) as `students_enrolled` FROM `students` GROUP BY `enrollment_year`;
2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio -> SELECT `office_address`, COUNT(*) as `number_of_teachers` FROM `teachers` GROUP BY `office_address`;
3. Calcolare la media dei voti di ogni appello d'esame -> SELECT `exam_id`, COUNT(*) as `number_of_exams`, AVG(`vote`) as `average_vote` FROM `exam_student` GROUP BY `exam_id`;
4. Contare quanti corsi di laurea ci sono per ogni dipartimento -> SELECT `department_id`, COUNT(*) as `number_of_degree_courses` FROM `degrees` GROUP BY `department_id`;

### JOIN
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia -> SELECT `students`.*, `degrees`.`name` 
    FROM `students`
    INNER JOIN `degrees`
    ON `degrees`.`id` = `students`.`degree_id`
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia';
2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze -> SELECT `departments`.*, `degrees`.`name`, `level` FROM `departments` INNER JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id` WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' AND `level` = 'magistrale';
3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44) -> SELECT `teachers`.`id`, `teachers`.`name`, `teachers`.`surname`, `courses`.`id`, `courses`.`name` FROM `teachers` INNER JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` INNER JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` WHERE `teacher_id` = 44;
4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
nome -> SELECT `students`.`surname`, `students`.`name`, `degrees`.`name` as `degrees`, `departments`.`name` as `departments`
    FROM `students`
    INNER JOIN `degrees` ON `degrees`.`id` = `students`.`degree_id`
    INNER JOIN `departments` ON `departments`.`id` = `degrees`.`department_id`
    ORDER BY `students`.`surname` ASC;
5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti -> SELECT `degrees`.`name`, `courses`.`name`, CONCAT(`teachers`.`name`, ' ', `teachers`.`surname`) as `teachers` FROM `degrees` INNER JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` INNER JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id` INNER JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;
6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)
7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.
