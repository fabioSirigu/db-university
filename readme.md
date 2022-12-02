Modellizzare la struttura di una tabella per memorizzare tutti i dati riguardanti una **università**:
- sono presenti diversi **Dipartimenti** (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più **Corsi di Laurea** (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi **Corsi** (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi **Insegnanti**;
- ogni Corso prevede più **appelli d'Esame**;
- ogni **Studente** è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il **voto** ottenuto, anche se non sufficiente.
Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

## TABLE: UNIVERSITA'

      Realtionships:
      - oneToMany => dipartimenti & corsi di laurea
      - manyToMany => corsi di laurea & corsi
      - manyToMany => corsi & insegnanti
      - oneToMany => corsi & appelli d'esame
      - oneToMany => corso di laurea & studenti
      - manyToMany => studenti & appelli d'esame (+ pivot table 'appello_di_esame_studente')
      

## DIPARTIMENTI

      id: BIGINT, PK (SE NON SONO COMPRESE IN PK => AUTO_INCREMENT, UNIQUE, NOTNULL)
      name: VARCHAR (25), NOTNULL
      numero_corsi_di_laurea: VARCHAR (30), NULL
      numero_insegnanti:
      numero_iscritti:
      numero_dipartimenti
      description: TEXT, NULL
      corsi_di_laurea_id: BIGINT, NOTNULL



## CORSI DI LAUREA
## CORSI
## INSEGNANTI
## APPELLI D'ESAME
## STUDENTI
## VOTI