# Meklētāja funkcionālo pārbaužu žurnāls

Šeit ir uzskaitītas veiktās pārbaudes, kuras neuzrādīja kļūdas (Passed Tests):

* ✅ **XSS Drošības tests:** Ievadot `<script>alert('QA')</script>`, kods netiek izpildīts.
* ✅ **Pārlūka 'Back' pogas tests:** Pēc atgriešanās no rezultātu lapas, meklēšanas frāze saglabājas.
* ✅ **Diakritiskās zīmes:** Meklētājs saprot latviešu burtus ar garumzīmēm.
* ✅ **SQL Injection (Basic):** Ievade `' OR 1=1 --` netiek izpildīta kā kods.
* ⚠️ **Speciālo simbolu apstrāde:** Ievadot "!!!", tiek atrastas publikācijas, kuru tekstā ir šī simbolu kopa. Secinājums: Sistēma nefiltrē pieturzīmes no meklēšanas vaicājuma.
