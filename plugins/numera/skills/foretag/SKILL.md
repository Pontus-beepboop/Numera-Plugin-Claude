---
name: foretag
description: Sätter upp ett nytt företag i Numera direkt i chatten, slår upp organisationsnumret i Bolagsverkets register, frågar bara det som saknas och lägger upp företaget efter en förhandsvisning. Använd när användaren vill komma igång med en ny bokföring, lägga upp sitt företag eller när get_company säger att Numera inte är konfigurerat.
---

# Sätt upp företaget i Numera

## Arbetsgång

1. Anropa `get_company`. Är ett företag redan upplagt: säg det och avsluta (ändringar görs under Inställningar i Numera).
2. Fråga efter **organisationsnumret** (för enskild firma är det personnumret). Anropa `lookup_company`.
3. Bekräfta det registret hittade (namn, företagsform, adress) med användaren. Hittades inget: fråga efter företagsform och namn.
4. Fråga bara det som står i `still_to_ask`, en sak i taget och på enkel svenska:
   - Momsregistrerat? Om ja: momsperiod (månad, kvartal eller år). Osäker: det står på registreringsbeviset från Skatteverket.
   - Kontantmetoden eller fakturametoden. Förklara kort: kontantmetoden bokför fakturor när de betalas och passar de flesta små enskilda firmor.
   - Användarens namn (sparas i behandlingshistoriken).
   - Aktiebolag: vilken månad räkenskapsåret börjar.
5. Anropa `setup_company` **utan** `confirm` och läs upp förhandsvisningen.
6. Först när användaren sagt ja: anropa `setup_company` igen med samma uppgifter och `confirm: true`.
7. Berätta att företaget är upplagt i testläge och föreslå nästa steg: lägga in första kvittot, läsa in kontoutdraget, eller importera gammal bokföring med SIE om användaren byter från Fortnox, Visma, Bokio, Spiris eller ett annat program (Inställningar → Importera SIE i Numera).

## Principer

- Gissa aldrig organisationsnummer, momsperiod eller metod. Fråga.
- Lägg aldrig upp företaget utan att användaren sagt ja till förhandsvisningen.
- Inget bokförs här. Allt går att ändra i Numera efteråt.
