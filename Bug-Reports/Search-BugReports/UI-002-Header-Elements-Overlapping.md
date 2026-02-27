# UI Kļūdas ziņojums: UI-002

**Nosaukums:** Header elementu pārklāšanās pie vidēja ekrāna platuma (Tablet/Small Desktop)
**Tips:** UI / Responsive Design Issue
**Prioritāte:** Vidēja (Medium)

## 💻 Vide (Environment)
* **OS:** Windows 11
* **Pārlūks:** Firefox
* **Izšķirtspēja:** Aptuveni 1200px platums (Breakpoint tests)

## 🎯 Apraksts
Samazinot pārlūka loga platumu (pirms pārejas uz mobilo "hamburgeru" izvēlni), galvenes (*header*) elementi nesaglabā nepieciešamo distanci. Telefona numura ikona saduras ar uzņēmuma nosaukumu, un e-pasta adrese saduras ar meklēšanas lauku.

## 🛠️ Soļi kļūdas izsaukšanai
1. Atvērt mājaslapu `llkc.lv` pilnā ekrānā.
2. Lēnām sašaurināt pārlūka logu no labās puses uz kreiso vai otrādi.
3. Novērot augšējo kontaktu joslu un meklētāja novietojumu brīdī, kad logs sasniedz aptuveni 1200px platumu.

## 📈 Faktiskais rezultāts
Elementi vizuāli pārklājas (overlapping), radot nekārtīgu iespaidu un apgrūtinot informācijas nolasīšanu. Dizains nav adaptīvs šajā specifiskajā "lūzuma punktā" (*breakpoint*).

## ✅ Gaidāmais rezultāts
Elementiem pie mazāka platuma būtu:
1. Jāsamazina starpas (padding/margin).
2. Jāpāriet jaunā rindā (stacking).
3. Vai jāsamazina teksta izmērs, lai novērstu pārklāšanos.

## 📸 Pierādījums
![Header elementu pārklāšanās](../images/UX-002-header-overlap.png)

---
**Piezīme:** Šis defekts ietekmē zīmola vizuālo tēlu un liecina par nepilnībām CSS adaptīvajos stilos.
