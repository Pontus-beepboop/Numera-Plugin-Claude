---
name: setup
description: Kopplar Claude till bokföringsprogrammet Numera och kontrollerar att kopplingen fungerar. Använd när användaren vill komma igång med Numera, frågar hur Claude kopplas till Numera, eller när Numeras verktyg saknas.
---

# Koppla Claude till Numera

Numera är ett svenskt bokföringsprogram för enskild firma och aktiebolag. Claude kan läsa bokföringen och lägga in förslag som **utkast**, men aldrig bokföra, ändra bokförda verifikationer eller ta bort något. Användaren granskar och bokför själv i Numera.

Användaren är ofta inte van vid datorer eller bokföring. Skriv kort, på enkel svenska, ett steg i taget, och säg exakt vad som ska klickas på.

## 1. Finns kopplingen redan?

Leta efter Numeras verktyg (namnen slutar på `get_company`, `list_drafts`, `get_voucher`, `list_vouchers`, `search_accounts`, `account_balances` och `propose_booking`). Finns de: anropa `get_company` och gå till steg 3.

## 2. Om verktygen saknas

Fråga först: **"Använder du Numera-appen på en Mac?"** Välj sedan ett av sätten. Gör bara ett av dem.

**Ja, Numera-appen på Mac:**
1. Flytta Numera till mappen Program om den inte redan ligger där.
2. I Numera: Inställningar → AI-hjälp, slå på "Låt Claude och ChatGPT hjälpa till".
3. I Claude-appen: Customize → Plugins, öppna Numera och klicka på Install vid "Numera på Mac".
4. Stäng Claude-appen helt (⌘Q) och öppna den igen. Starta en ny chatt.

**Nej (webben, Windows eller bara iPhone):**
1. I Numera: Inställningar → Claude och ChatGPT (webben) eller Inställningar → Numera-konto → Claude och ChatGPT (appen). Klicka på Skapa koppling, läs varningen och godkänn.
2. Kopiera adressen som visas. Den visas bara en gång.
3. I Claude: Customize → Connectors, klicka på + och välj Add custom connector. Skriv Numera som namn, klistra in adressen och klicka på Add.
4. Starta en ny chatt.

Fungerar det inte efter det: be användaren starta om Claude-appen och försöka igen. Hjälper inte det, hänvisa till support@usenumera.se.

## 3. Bekräfta

Visa i två eller tre meningar: företagets namn, företagsform, om bokföringen är i testläge eller låst läge, och hur många utkast som väntar. Erbjud sedan en översikt över företaget (skillen `start`) eller att föreslå bokföring för utkasten (skillen `bokfor`) om det finns utkast.

## Säkerhet

- Adressen från Numera är en nyckel till bokföringen. Be aldrig användaren klistra in den i chatten och skriv aldrig ut den. Har den kommit ut: ta bort kopplingen i Numera och skapa en ny.
- Bokföringen skickas till Anthropic när Claude läser den. Det har användaren godkänt i Numera.
