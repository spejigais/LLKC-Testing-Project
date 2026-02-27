# Meklētāja testēšanas kopsavilkums (Test Summary)

Šajā dokumentā apkopoti rezultāti no LLKC meklētāja funkcionālajām pārbaudēm, drošības testiem un lietojamības analīzes.

---

### Veiktās pārbaudes (Passed Tests)
*Šīs funkcijas darbojas stabili un atbilst pamatstandartiem.*

* ✅ **XSS & HTML Injection drošība:** Ievadot vaicājumus ar skriptiem `<script>alert('QA')</script>` vai HTML tagiem `<h1>Test</h1>`, sistēma tos neizpilda. Tagi tiek ignorēti vai izfiltrēti, un meklēšana tiek veikta tikai pēc burtiskās teksta vērtības. Tas apliecina, ka ievades lauks ir drošs pret koda injekcijām.
* ✅ **Pārlūka 'Back' pogas tests:** Pēc atgriešanās no rezultātu lapas, meklēšanas frāze saglabājas meklēšanas laukā.
* ✅ **Diakritiskās zīmes:** Sistēma korekti apstrādā un atrod vārdus ar latviešu valodas raksturīgajām zīmēm (ā, č, ē, ģ u.c.).
* ✅ **SQL Injection (Basic):** Ievade `' OR 1=1 --` netiek izpildīta kā datubāzes komanda.

---

### Novērojumi un Ieteikumi (Observations & Improvements)
*Šeit fiksētas lietas, kuras tehniski strādā, bet kuru loģika nav caurspīdīga vai lietotājam draudzīga/ saprotama.*

* **Speciālo simbolu apstrāde:**
    * ⚠️ **Novērojums:** Ievadot vaicājumu `!!!`, sistēma atrod rakstus, kuros burtiski ir šī simbolu kopa.
    * 💡 **Ieteikums:** Ieviest *noise character* filtrēšanu, lai meklētājs ignorētu liekas pieturzīmes un fokusētos uz jēgpilnu teksta saturu.
    * ⚠️ **Novērojums: Ievadot vaicājumu `--`, meklētājs to vizuāli apvieno garākā domuzīmē un atgriež rezultātus. Tāpat rezultāti tiek parādīti, meklējot `__`
    * 💡 **Ieteikums: Saskaņot simbolu filtrēšanas loģiku – ja tādi simboli kā `@`, `#`, `$`, `%`, `&` tiek ignorēti, arī pieturzīmēm bez teksta nevajadzētu atgriezt nejaušus rezultātus.
* **Rezultātu kārtošanas loģika:**
    * ⚠️ **Novērojums:** Meklēšanas rezultātu kārtošanas princips nav pašsaprotams. Nav novērojama konsekventa secība ne pēc relevances (vārda pozīcijas virsrakstā), ne pēc stingras hronoloģijas (piemēram, novembra datumi rezultātos parādās sajauktā secībā).
    * 💡 **Ieteikums:** Definēt un ieviest skaidru rezultātu prioritizēšanu (piemēram, aktuālākie raksti ar precīzāko atbilstību saraksta sākumā) vai pievienot kārtošanas filtru lietotājam.
* **Frāžu meklēšana un satura indeksācija (Exact Match):**
    * ⚠️ **Novērojums:** Sistēma atbalsta meklēšanu ar pēdiņām (piem. `"lauksaimniecības politika"`). Novērots, ka meklētājs indeksē arī raksta beigās esošo **tehnisko informācijas bloku** (atsauces uz līgumiem un finansējumu slīprakstā), kas atrodas virs galvenās lapas kājenes (*footer*). Tas būtiski ietekmē rezultātu skaitu vaicājumiem bez pēdiņām.
    * 💡 **Ieteikums:** Pievienot paskaidrojošu informāciju (piem. "tooltip") par pēdiņu izmantošanu precīzākai meklēšanai un izvērtēt iespēju samazināt prioritāti tehniskajiem informācijas blokiem meklēšanas rezultātos.
* **Testa dati produkcijas vidē:**
    * ⚠️ **Novērojums:** Meklējot specifiskus atslēgvārdus (piem. `test`), rezultātos parādās izstrādes procesa testa dati `test1, test2 utt.`.
    * 💡 **Ieteikums:** Veikt datubāzes tīrīšanu produkcijas vidē, lai lietotājiem netiktu rādīti sistēmas testēšanas raksti.
* **Maksimālā vaicājuma garuma validācija (Stress Test):**
    * ⚠️ **Novērojums:** Sistēma ļauj meklēšanas laukā ievadīt un apstrādāt pārmērīgi lielu datu apjomu (testēts ar 25 000 vārdiem). Programma neuzkārās, kas ir pozitīvi, taču meklēšanas laukam nav noteikts rakstzīmju ierobežojums (*maxlength*).
    * 💡 **Ieteikums:** Ieviest saprātīgu rakstzīmju ierobežojumu meklēšanas laukam (piemēram, 200–500 simboli), lai novērstu lieku servera noslodzi un potenciālus pakalpojuma atteices (*DoS*) riskus nākotnē.

---

### Tehniskā veiktspēja (PageSpeed Insights analīze)
Veikta automatizētā analīze LLKC sākumlapai (Desktop skatā):

### **Desktop**
* **Performance:** **70** (Apmierinošs rādītājs)
* **Accessibility:** **84**
* **LCP (Ielādes ātrums):** **4.1 s** (Virs ieteicamajām 2.5 s)
* **CLS (Lapas stabilitāte):** **0.004** (Izcila stabilitāte)
* **Secinājums:** Desktop versija nodrošina stabilu un pietiekami ātru piekļuvi meklētājam, lai gan ielādes laiks nedaudz pārsniedz optimālo robežu.

### **Mobilā versija**
* **Performance:** **49** (Nepieciešami uzlabojumi)
* **Accessibility:** **83**
* **LCP (Ielādes ātrums):** **37.4 s** (Kritiski zems rādītājs mērījumā)
* **CLS (Lapas stabilitāte):** **0** (Lapa ielādes laikā ir pilnīgi stabila)
* ⚠️**Secinājums:** Veicot manuālo pārbaudi uz reālas mobilās ierīces, faktiskais lapas ielādes laiks ir aptuveni 2-4 sekundes, kas krasi atšķiras no PageSpeed Insights uzrādītajām 37.4 sekundēm.

**Kāpēc rādītāji atšķiras?**
* **Trešo pušu saturs:** Lapā iestrādātie uznirstošie paziņojumi iespējams ietekmē automatizētos mērījumus.
* **Simulētais lēnums:** PageSpeed Insights izmanto "Worst-case scenario". Reālos apstākļos ar 4G+/5G vai WiFi pieslēgumu lapa ir gatava lietošanai krietni ātrāk.
