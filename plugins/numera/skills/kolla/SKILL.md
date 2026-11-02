---
name: kolla
description: Kontrollerar bokföringen i Numera utan att ändra något och ger en prioriterad åtgärdslista, gamla utkast, möjliga dubbletter, saldon som ser fel ut och kommande deadlines. Använd när användaren vill veta om bokföringen är i ordning.
---

# Kontrollera bokföringen

Bara läsning. Anropa aldrig `propose_booking` i den här skillen.

## Kontroller

1. `get_company`: företagsform, metod, momsperiod, låst läge, deklarationsdatum och antal utkast.
2. **Gamla utkast.** `list_drafts`. Ett utkast vars datum ligger mer än 50 dagar efter månadens slut ska bokföras snarast (bokföringslagen 5 kap. 2 §).
3. **Möjliga dubbletter.** `list_vouchers` för perioden. Flagga verifikationer med samma motpart, samma belopp och datum inom några dagar. Säg "möjlig dubblett", inte "dubblett".
4. **Saldon som ser fel ut.** `account_balances` för innevarande år:
   - 1930 (företagskontot) i kredit, dvs. negativt saldo på banken.
   - Aktiebolag: 2893 i debet betyder att bolaget har lånat ut pengar till ägaren, vilket normalt är förbjudet (ABL 21 kap.).
   - 1510 och 2440 med gamla poster (fakturametoden): obetalda kund- och leverantörsfakturor.
   - 2650 eller 1630 som inte går ihop med det Numera visar för momsen och skattekontot.
5. **Deadlines** från `get_company` (moms, och arbetsgivardeklaration den 12:e om det finns löner).

## Resultat

En åtgärdslista sorterad efter allvar och datum: **Måste göras**, **Bör kontrolleras**, **Bra att veta**. Varje punkt: vad, varför (en mening) och var i Numera det rättas. Avsluta med vad som ser bra ut, så att användaren vet vad som är kontrollerat.

## Regler

- Påstå inget som verktygen inte visar. Skriv "kunde inte kontrolleras" när en kontroll inte går att göra med verktygen.
- Ge ingen juridisk eller skatterättslig bedömning utöver att peka på regeln; hänvisa till redovisningskonsult vid tveksamhet.
