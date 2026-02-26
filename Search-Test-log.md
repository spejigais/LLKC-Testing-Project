# Meklētāja funkcionālo pārbaužu žurnāls

Šeit ir uzskaitītas veiktās pārbaudes, kuras neuzrādīja kļūdas (Passed Tests):

* [x] **XSS Drošības tests:** Ievadot `<script>alert('QA')</script>`, kods netiek izpildīts.
* [x] **Pārlūka 'Back' pogas tests:** Pēc atgriešanās no rezultātu lapas, meklēšanas frāze saglabājas.
* [x] **Diakritiskās zīmes:** Meklētājs saprot latviešu burtus ar garumzīmēm.
* [x] **SQL Injection (Basic):** Ievade ' OR 1=1 -- netiek izpildīta kā kods.
