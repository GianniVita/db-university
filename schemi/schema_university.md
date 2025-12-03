## Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi `Dipartimenti` (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni `Dipartimento` offre più `Corsi di Laurea` (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni `Corso di Laurea` prevede diversi `Corsi` (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni `Corso` può essere tenuto da diversi `Insegnanti`;
- ogni `Corso` prevede più appelli d'`Esame`;
- ogni `Studente` è iscritto ad un solo `Corso di Laurea`;
- ogni `Studente` può iscriversi a più appelli di `Esame`;
- per ogni appello d'`Esame` a cui lo `Studente` ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.

## Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.


## Struttura del Database Universitario

# Departments
- id	BIGINT UNSIGNED	PK, AI
- nome  VARCHAR(100) NOT NULL
- codice VARCHAR(10) NOT NULL UNIQUE

# Degree Courses
- id    BIGINT UNSIGNED PK, AI
- dipartiento_id BIG UNSIGNED FK NOT NULL
- nome VARCHAR(100) NOT NULL
- durata_anni  TINYINT UNSIGNED NOT NULL

# Students
- matricola     BIGINT UNSIGNED PK,NOT NULL
- corso_laurea_id BIGINT UNSIGNED PK,NOT NULL
- nome VARCHAR(50) NOT NULL
- cognome VARCHAR(50) NOT NULL
- data_nascita DATE NOT NULL
- emial VARCHAR(100) UNIQUE

# Courses
- id    BIGINT UNSIGNED PK,AI 
- corso_laurea_id   BIGINT UNSIGNED FK,NOT NULL 
- nome_corso  VARCHAR(100)  
- codice_corso VARCHAR(10)
- cfu TINYINT NOT NULL

# Teacehrs
- id BIGINT PK,AI 
- nome_insegnante VARCHAR(50) NOT NULL
- cognome_insegnate VARCHAR(50) NOT NULL
- codice_fiscale CHAR(16) UNIQUE
- email  VARCHAR UNIQUE

# Course&Teacher-Pivot (Relazione * - *)
- corso_id BIGINT UNSIGNED FK,NOT NULL
- insegnate_id BIGINT UNSIGNED FK,NOT NULL

# Exam Sittings (Relazione 1 - * un corso prevede + appelli)
- id_exam BIGINT PK, AI 
- corso_id BIGINT FK(corso_id), NOT NULL
- data_esame DATETIME, NOT NULL
- luogo VARCHAR(100) , NOT NULL

# Exam Enrollment&GradeRecords (Relazione * - * many to many)
- appello_id BIGINT FK NOTNULL
- studente_matricola BIGINT FK NOT NULL
- voto TINYINT UNSIGNED NULL
- stato_iscrizione ENUM NOT NULL, DEFAULT'iscritto'
- data_verbalizzazione DATE NULL
- PRIMARY KEY (appello_id, studente_matricola) 