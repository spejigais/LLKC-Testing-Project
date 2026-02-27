# UX Kļūdas ziņojums: UX-004

**Nosaukums:** Lapas ritināšanas pozīcija netiek atiestatīta pie jauna meklējuma
**Tips:** UX / Functional Defect
**Prioritāte:** Vidēja (Medium)

## 💻 Vide (Environment)
* **OS:** Windows 11
* **Pārlūks:** Mozilla Firefox 147.0.4 (64-bit)
* **Ierīce:** Desktop

## 🎯 Apraksts
Veicot jaunu meklēšanu laikā, kad lietotājs ir patinis iepriekšējos rezultātus uz leju, lapas ritināšanas (*scroll*) pozīcija netiek atiestatīta uz sākumu. Lietotājs paliek lapas vidū vai apakšā, neredzot jaunā vaicājuma pirmos rezultātus.

## 🛠️ Soļi kļūdas izsaukšanai
1. Meklētājā ierakstīt vārdu "saimniecība".
2. Patīt rezultātus uz leju (piemēram, līdz 10. rezultātam).
3. Neuzbraucot augšā, ierakstīt meklētājā jaunu vārdu "graudi".

## 📈 Faktiskais rezultāts
Lapa ielādē jaunos rezultātus, bet saglabā iepriekšējo ritināšanas pozīciju. Lietotājam manuāli jābrauc uz augšu, lai redzētu saraksta sākumu.

## ✅ Gaidāmais rezultāts
Sistēmai pie katra jauna meklēšanas pieprasījuma automātiski jāpārvieto lietotājs uz lapas sākumu (*Scroll to top*).
