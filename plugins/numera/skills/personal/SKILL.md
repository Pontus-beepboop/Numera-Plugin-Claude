---
name: personal
description: Sköter personalen i Numera, frånvaro (sjuk, vab, föräldraledig, semester, tjänstledig), timmar för timlön, övertid och OB, semestersaldo och det som behöver göras för de anställda (provanställning, anställningsbevis, Försäkringskassan). Använd när användaren berättar att någon är sjuk eller ledig, vill rapportera timmar, frågar om semesterdagar eller vad som ska göras för personalen.
---

# Personal, frånvaro och timmar

Numera räknar själv in frånvaron och timmarna i nästa lön. Frånvaro och timmar i en månad betalas med lönen månaden efter. Du lägger bara in vad som hänt, du räknar inte lönen.

## Arbetsgång

1. `list_employees` för att hitta rätt person och `employee_id`. Är det oklart vem som menas: fråga.
2. `personnel_reminders` om användaren vill veta vad som behöver göras, eller som avslutning när du gjort något.
3. `list_absences` visar frånvaron, timmarna, semestersaldot och hur nästa lön blir (rader som sjuklön, karensavdrag och semestertillägg).

## Frånvaro

- `add_absence` med `kind`: `sjuk`, `vab`, `foraldraledig`, `semester`, `tjanstledig` eller `ledig_med_lon`, och första och sista dagen. Halva dagar: `percent: 50`.
- Sjuk: dag 1-14 betalar företaget sjuklön 80 % med ett karensavdrag per sjukperiod. Blir personen sjuk igen inom fem dagar fortsätter samma sjukperiod. Från dag 15 betalar Försäkringskassan, och arbetsgivaren ska anmäla sjukfallet senast sju dagar efter dag 14. Påminn om det när en sjukperiod blir längre än 14 dagar.
- Vab och föräldraledighet: lönen minskas och dagarna följer med till arbetsgivardeklarationen, så att Försäkringskassan kan betala. Den anställda ansöker själv hos Försäkringskassan.
- Fråga om omfattning och datum om det är oklart. Gissa inte.

## Timmar

- `add_hours` med datum, antal timmar och `kind`: `arbete`, `overtid` eller `ob`.
- Timavlönade får semesterersättning (normalt 12 %) med varje lön. Månadsavlönade påverkas bara av övertid och OB.

## Rapporter från de anställda

- Anställda kan ha en egen inloggning (Min anställning) och rapportera frånvaro och timmar själva. Det som de har rapporterat väntar på godkännande (`waiting_for_approval` i `list_absences`).
- Godkänn eller neka aldrig själv: berätta vad som väntar och att användaren godkänner på personalkortet under Löner.

## Regler

- Inget bokförs av de här verktygen. Lönen gör användaren under Löner (eller med `run_payroll` om användaren ber om det).
- Lämna aldrig ut personnummer, och nämn inte varför någon är sjuk.
- Visa efteråt vad du lagt in: person, typ, datum och omfattning.
