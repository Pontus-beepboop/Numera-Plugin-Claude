---
name: dagskassa
description: Sköter dagskassan i Numera, alltså dagens försäljning med kort, Swish, kassa och betaltjänster som Zettle och Stripe. Lägger in dagar som utkast, läser av en Z-rapport, gör dagskassor av Swish på kontoutdraget och bokar utbetalningar från kortföretaget. Använd när användaren pratar om dagskassa, kassa, Z-rapport, kortbetalningar, Swish-försäljning, Zettle eller Stripe.
---

# Dagskassan

Företag med många små köp bokför inte varje köp. De lägger in en dagskassa per dag: vad som såldes per momssats och hur kunderna betalade. Kort ligger på konto 1580, Swish på 1581 och betaltjänster på nätet på 1582 tills pengarna kommer till banken.

## Arbetsgång

1. `list_day_cash`: se vilka dagar som finns, vilka som är utkast, dagar som saknas, vad som ligger på väg till banken, bankrader som ser ut som utbetalningar (`payouts_on_bank`) och Swish på banken (`swish_on_bank`).
2. Berätta kort vad som behöver göras och fråga vad användaren vill börja med.

## Lägga in en dag

- Har användaren en Z-rapport (bild eller siffror): läs av datum, försäljning per momssats (belopp inklusive moms) och betalningar per betalsätt. Visa siffrorna och fråga om de stämmer.
- `add_day_cash` skapar ett utkast. Summan av försäljningen och summan av betalningarna ska vara lika. Går det inte ihop: fråga, gissa inte.
- Bokför med `book_vouchers` först när användaren har godkänt siffrorna.

## Zettle och Stripe

- `fetch_day_cash` hämtar dagarna till och med i går som utkast, om användaren har kopplat tjänsten under Dagskassa i Numera.
- Be aldrig om API-nyckeln i chatten. Nyckeln lägger användaren in själv i Numera under Dagskassa, Hämta automatiskt.
- Svarar verktyget att hämtningen görs i Numera: be användaren öppna Dagskassa och trycka Hämta försäljning, och fortsätt sedan med `list_day_cash`.

## Swish som kommer direkt in på banken

- Finns det rader i `swish_on_bank` och Swish inte ligger i dagskassan: fråga vilken moms försäljningen har (25, 12, 6 eller 0 procent) och kör `swish_to_day_cash`. Det blir ett utkast per dag och bankraderna kopplas till det.

## Utbetalningar från kortföretaget

- För varje rad i `payouts_on_bank`: `propose_payout` skapar utkastet (banken i debet, 1580, 1581 eller 1582 i kredit och en eventuell avgift på 6570). Visa raderna och anteckningen.
- När användaren har godkänt: `match_bank_transaction` med bankradens id och utkastets id. Då bokförs utkastet och raden kopplas.
- Stämmer beloppet inte med dagskassorna som väntar: säg det och fråga om en avgift har dragits eller om en dag saknas.

## Regler

- Allt blir utkast. Bokför bara när användaren ber om det, och visa alltid vad som bokfördes: verifikationsnummer, datum, belopp och konton.
- Momssatsen bestämmer användaren. Mat och fika är oftast 12 procent och det mesta annat 25 procent, men fråga.
- Saknas en dag som borde ha försäljning: påminn, men lägg aldrig in påhittade siffror.
