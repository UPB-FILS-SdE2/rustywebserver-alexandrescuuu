[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-24ddc0f5d75046c5622901739e7c5dd533143b0c8e959d652212380cedb1ea36.svg)](https://classroom.github.com/a/TXciPqtn)
# Rustwebserver

## Descriere 
- server web facut in rust cu ajutorul bibliotecii asincrone tokio.
- gestioneza metode http de tip GET si POST
- executa scripturi de tip .sh dintr-un anume server
- serveste fisiere statice dintr-un folder mentionat de utilizator

## Detalii implementare
- serverul porneste astfel :
  ```
  rustywebserver {port} folder
  ```
- in implementarea acestuia am avut mai multe puncte pe care a trb sa le ating :
  - crearea serverului asincrion folosind libraria tokio in main conform documentatiei si apelarea functiei handle_request
  - in handle_request - > gestionez cererile HTTP și trimite răspunsurile corespunzătoare ( body, code, status ) conform fiecarei metode in server
      - in cadrul handle_request ma folosesc de niste functii ajutatoare precum
          - parse_headers - pentru a extrage headerurile mentionate intr-un anume script
          - parse_request - pentru a extrage din cererea http : metoda folosita, calea si parametrii de interogare atunci cand sunt mentionati
          - get_mime_type - in cadrul temei a trebuit sa ma asigur ca tipul datei fisierelor corespunde cu cel mentionat de tema
          - get_request_body - obtin body-ul cererii
  - error handling : pentru fiecare metoda am luat in considerare tipul de eroare specifica cererii http :
      - 500 eroare interna , scriptul nu functioneaza
      - 403 forbidden - acceseaza fisiere din afara folderului dat ca parametru
      - 405 method not allowed - implementarea este facuta decat pentru methodele de get si post, nu si pentru put sau delete
      - 404 cand fisierul nu exista  
