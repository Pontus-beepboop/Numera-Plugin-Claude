---
name: bokfor
description: Går igenom kvitton och fakturor som väntar som utkast i Numera och lägger in en komplett kontering med förklaring i varje utkast. Bokför aldrig själv. Använd när användaren vill bokföra sina utkast, kvitton eller underlag i Numera.
---

# Bokför utkasten i Numera

Claude föreslår, användaren bokför. Varje förslag blir ett utkast som användaren granskar i Numera.

## Arbetsgång

1. **Företaget först.** Anropa `get_company`. Notera företagsform (enskild firma eller aktiebolag), momsregistrering, faktura- eller kontantmetoden och om bokföringen är låst. Den informationen styr kontona.
2. **Hämta utkasten.** `list_drafts` (gärna `only_with_document: true` först). Gruppera dem per motpart, så att alla kvitton från samma butik bokförs likadant.
3. **För varje utkast:**
   1. `get_voucher` med `include_document: true`. Läs underlaget: datum, säljare, totalbelopp, moms per sats, valuta och om det står "reverse charge".
   2. **Hur har bolaget bokfört motparten förut?** `list_vouchers` med motpartens namn som `query`. Följ samma kontering om inget talar emot det.
   3. Behövs ett konto: `search_accounts`. Använd bara konton som finns i Numeras kontoplan.
   4. `propose_booking` med `voucher_id`, alla rader (debet = kredit på öret), `explanation` på enkel svenska (2-4 meningar), `warnings` för det användaren måste kontrollera och `questions` om något avgörande saknas. Sätt `confidence` ärligt.
   5. Om svaret visar fel: rätta och anropa igen. Ge inte upp efter ett fel, men gissa inte heller.
4. **Rapportera** i en tabell: utkast, motpart, belopp, föreslagna konton, säkerhet, och vad användaren behöver kontrollera. Påminn om att bokföringen sker i Numera.

## Auktoritetsordning

1. Företagets inställningar och regler i Numera (instruktionerna som Numeras server skickar).
2. Hur bolaget själv har bokfört samma motpart förut (`list_vouchers`).
3. Först därefter allmän kunskap om BAS-kontoplanen och svensk moms.

## Regler

- **Moms aldrig ur minnet.** Momsbeloppen ska komma från underlaget. Står ingen moms på underlaget, fråga i `questions` i stället för att räkna fram den.
- **Representation, privata köp, utländska tjänster och inventarier** är vanliga fel: lägg en varning och förklara regeln kort.
- Är perioden **låst** (bokslut gjort eller moms avräknad): stoppa, förklara varför och föreslå att användaren rättar i en öppen period i Numera.
- Löner föreslås inte här, de görs under Löner i Numera (Numera stoppar lönekonton i förslag).
- Hitta aldrig på kvitton, belopp eller motparter. Kan underlaget inte läsas: säg det och hoppa över utkastet.
- Skapa nya utkast (utan `voucher_id`) bara när användaren uttryckligen ber om det.
