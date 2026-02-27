# LLKC Meklētāja Testēšanas Scenāriji (Test Cases)

Šajā dokumentā ir apkopoti strukturēti testēšanas scenāriji, kas balstīti uz LLKC platformas auditā veiktajām pārbaudēm.

## TC-01: Vaicājuma Normalizēšana un Variācijas
**Mērķis:** Pārbaudīt sistēmas spēju atpazīt un apstrādāt dažāda formāta teksta vaicājumus.

| Ievades dati (Input) | Pārbaudes tips | Sagaidāmais rezultāts | Statuss |
| :--- | :--- | :--- | :--- |
| `mežsaimniecība` | Standarta (mazie burti) | Atrod precīzas sakritības | ✅ Passed |
| `MEŽSAIMNIECĪBA` | Reģistrjutība | Ignorē reģistru, atrod saturu | ✅ Passed |
| `Mezsaimnieciba` | Bez diakritikas | Atrod rezultātus (normalizē ā, č, ē...) | ✅ Passed |
| `   Mežsaimniecība   ` | Atstarpes malās (Trim) | Automātiski "nogriež" atstarpes, atrod saturu | ✅ Passed |
| `M e ž s a i m n i e c ī b a` | Atstarpes starp burtiem | Sistēma normalizē vārdu un atrod saturu | ❌ Failed |
| `Mež saimniecība` | Atstarpe vārda vidū | Sistēma atpazīst vārdu vai meklē abus | ✅ Passed |
| `@, ?, #, $, %, ^, *, (), _, +` | Speciālie simboli | Sistēma ignorē simbolus vai parāda kļūdas paziņojumu | ✅ Passed |
| `!!! , -- , __` | Speciālie simboli | Sistēma ignorē simbolus vai parāda kļūdas paziņojumu | ⚠️ Observation |

---

## TC-02: Drošības un Stresa Testēšana
**Mērķis:** Pārbaudīt sistēmas noturību pret koda injekcijām un pārmērīgu datu apjomu.

| Ievades dati | Pārbaudes tips | Sagaidāmais rezultāts | Statuss |
| :--- | :--- | :--- | :--- |
| `<script>alert('QA')</script>` | XSS Injection | Kods netiek izpildīts (tiek izfiltrēts) | ✅ Passed |
| `<h1>Test</h1>` | HTML Injection | Teksts netiek formatēts kā virsraksts | ✅ Passed |
| `' OR 1=1 --` | SQL Injection | Netiek ietekmēta datubāzes darbība | ✅ Passed |
| `25 000 vārdu teksts` | Stress Test (DoS) | Sistēma ierobežo ievadi vai neuzkaras | ⚠️ Observation |

---

## TC-03: UX un Responsīvā Dizaina Testi
**Mērķis:** Pārbaudīt meklētāja pieejamību un uzvedību dažādās ierīcēs un lietošanas scenārijos.

| Scenārijs | Pārbaudes darbība | Sagaidāmais rezultāts | Statuss |
| :--- | :--- | :--- | :--- |
| **0 rezultāti** | Ievadīt nesaistītu tekstu | Parādās ziņojums: "Diemžēl nekas netika atrasts" | ❌ Failed (UX-001) |
| **Pārklāšanās** | Sašaurināt logu uz ~1200px | Header elementi nesaduras | ❌ Failed (UI-002) |
| **Mobilais skats** | Atvērt lapu platumā < 768px | Meklētājs ir pieejams galvenē vai menu | ❌ Failed (UX-003) |
| **Scroll Reset** | Meklēt -> Patīt lejā -> Jauns meklējums | Meklēšanas rezultāti automātiski atgriežas augšpusē | ❌ Failed (UX-004) |
| **Navigācija** | Atvērt rakstu -> Nospiest "Back" | Meklēšanas laukā saglabājas ievadītā frāze | ✅ Passed |

---

### 💡 Piezīmes:
* **✅ Passed:** Funkcija strādā atbilstoši standartiem.
* **❌ Failed:** Konstatēta kļūda (detalizētu aprakstu skatīt mapē `Bug-Reports/`).
* **⚠️ Observation:** Sistēma strādā, bet ir ieteicami uzlabojumi lietojamībai vai drošībai.
