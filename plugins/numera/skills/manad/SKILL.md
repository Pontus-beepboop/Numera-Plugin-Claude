---
name: manad
description: Går igenom månadsavslutet i Numera steg för steg, utkast, bankavstämning mot kontoutdraget, obetalda fakturor, löner och kommande deklarationer. Använd när användaren vill stänga en månad eller undrar vad som ska göras i slutet av månaden.
---

# Månadsavslut

Fråga vilken månad det gäller om användaren inte har sagt det (standard: förra månaden).

## Steg

1. `get_company`: metod, momsperiod, låst läge och deadlines.
2. **Utkast i månaden.** `list_drafts`, filtrera på månaden. Alla ska bokföras eller tas bort i Numera. Erbjud att bokföra dem (skillen `bokfor`).
3. **Bankavstämning.** `account_balances` med `to` = månadens sista dag och `accounts: "1930"`. Be användaren om saldot på kontoutdraget samma dag. Skiljer det: lista månadens verifikationer på 1930 (`list_vouchers` med `account: 1930`) och hjälp till att hitta skillnaden. Bokför inget, föreslå i stället vad som saknas.
4. **Obetalda fakturor.** Fakturametoden: saldon på 1510 och 2440. Kontantmetoden: obetalda fakturor ligger som utkast och bokförs när de betalas.
5. **Löner.** `payroll_summary` för månaden: bruttolön, skatt, arbetsgivaravgift, om arbetsgivardeklarationen är lämnad och betald, och lönebesked som inte är bokförda. Påminn om arbetsgivardeklarationen den 12:e månaden efter (17:e i januari och augusti), som görs under Löner i Numera. Är arbetsgivaravgiften 0 kr för någon med lön: be användaren kontrollera personnumret (född 1937 eller tidigare ger 0 kr, Skatteverkets testnummer 19121212-1212 också).
6. **Moms.** Slutar momsperioden med månaden: erbjud att förbereda momsdeklarationen (skillen `moms`).
7. **Skattekontot.** Saldo på 1630 jämfört med Skatteverkets skattekonto, om användaren har det.

## Resultat

En checklista med bockar för det som är klart och tydliga åtgärder för resten, med var i Numera de görs.

## Regler

- Bara läsning, utom om användaren ber om förslag eller ber dig bokföra ("gör klart månaden"); då gäller reglerna i skillen `bokfor`.
- Låst period: förklara att rättelser görs i en öppen period.
