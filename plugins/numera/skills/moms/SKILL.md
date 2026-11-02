---
name: moms
description: Förbereder momsdeklarationen i Numera, visar momsen för perioden, deklarationsdatum och vad som ska kontrolleras innan filen skapas i Numera. Använd när användaren frågar om moms, momsdeklaration eller vad som ska betalas till Skatteverket.
---

# Momsen inför deklarationen

## Arbetsgång

1. `get_company`: momsregistrering, momsperiod (månad, kvartal eller år), pågående period, moms att betala eller få tillbaka och sista dag. Är företaget inte momsregistrerat: säg det och avsluta.
2. `account_balances` för periodens datum och `accounts: "2610-2650"`. Utgående moms ligger på 2610-2639 (kredit), ingående på 2640-2649 (debet). Kontrollera att summan stämmer med Numeras siffra. Stämmer den inte: säg det, gissa inte varför.
3. `list_drafts`: utkast med datum i perioden ska bokföras först, annars blir deklarationen fel.
4. Kontrollera omvänd moms: `list_vouchers` för perioden med `account: 2614` (och 4535/4531/4515). Varje rad på 2614 ska ha en motsvarande rad på 2645.
5. Sammanfatta: belopp att betala eller få tillbaka, sista dag, och en kort lista med det som måste göras innan.

## Så lämnas deklarationen

Användaren skapar filen i Numera: **Moms, Skapa fil**. Den laddas upp på skatteverket.se, Lämna momsdeklaration, Lämna via fil, och signeras med BankID. Därefter bokför Numera momsavräkningen (mot 2650). Claude lämnar aldrig in något själv.

## Regler

- Momsbelopp och rutor kommer från Numera, aldrig ur minnet.
- Skriv "ruta 05", "ruta 10" osv. bara när Numera eller kontots momsruta visar det.
- Vid tveksamhet om en affärshändelse är momspliktig: förklara att det behöver kontrolleras och hänvisa till Skatteverket eller redovisningskonsult.
