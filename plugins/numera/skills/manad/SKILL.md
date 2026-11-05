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
5. **Löner.** Finns lönekonton (7010-7299) i månaden: påminn om arbetsgivardeklarationen den 12:e månaden efter (17:e i januari och augusti) och att den görs under Löner i Numera.
6. **Moms.** Slutar momsperioden med månaden: erbjud att förbereda momsdeklarationen (skillen `moms`).
7. **Skattekontot.** Saldo på 1630 jämfört med Skatteverkets skattekonto, om användaren har det.

## Resultat

En checklista med bockar för det som är klart och tydliga åtgärder för resten, med var i Numera de görs.

## Regler

- Bara läsning, utom om användaren ber om förslag eller ber dig bokföra ("gör klart månaden"); då gäller reglerna i skillen `bokfor`.
- Låst period: förklara att rättelser görs i en öppen period.
