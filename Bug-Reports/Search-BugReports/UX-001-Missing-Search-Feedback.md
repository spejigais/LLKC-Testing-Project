# UX Kļūdas ziņojums: UX-001

**Nosaukums:** Informatīva paziņojuma trūkums pie 0 meklēšanas rezultātiem
**Tips:** UX / Usability Issue
**Prioritāte:** Vidēja (Medium)

## 💻 Vide (Environment)
* **OS:** Windows 11
* **Pārlūks:** Mozilla Firefox 147.0.4 (64-bit)
* **Ierīce:** Desktop

## 🎯 Apraksts
Ja meklētājā tiek ievadīts vaicājums, kuram sistēma nevar atrast nevienu atbilstību, lietotājs nesaņem nekādu atgriezenisko saiti. Meklēšanas rezultātu logs neatveras.

## 🛠️ Soļi kļūdas izsaukšanai
1. Atvērt mājaslapu `llkc.lv`.
2. Augšējā meklēšanas logā ievadīt nesaistītu simbolu virkni (piemēram: `vēstule`).
3. Novērot meklēšanas/rezultātu logu.

## 📈 Faktiskais rezultāts
Meklēšanas/rezultātu logs neatveras. Netiek izvadiīts nekāds teksts.

## ✅ Gaidāmais rezultāts
Sistēmai būtu jāizvada informatīvs ziņojums, piemēram: *"Diemžēl nekas netika atrasts. Mēģiniet izmantot citus atslēgvārdus."* Pretējā gadījumā lietotājs var domāt, ka sistēma nestrādā. 

## 📸 Pierādījums
![Meklētājs bez rezultātiem](../images/UX-001-Missing-Search-Feedback.png)

---
*Piezīme: Šis atradums ir daļa no LLKC platformas manuālā audita.*
