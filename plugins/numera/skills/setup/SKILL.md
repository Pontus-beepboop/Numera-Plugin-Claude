---
name: setup
description: Kopplar Claude Code till bokföringsprogrammet Numera och kontrollerar att kopplingen fungerar. Använd när användaren vill komma igång med Numera i Claude Code eller när Numeras verktyg saknas.
---

# Koppla Claude Code till Numera

Numera är ett svenskt bokföringsprogram för enskild firma och aktiebolag. Claude kan läsa bokföringen och lägga in förslag som **utkast**, men aldrig bokföra, ändra bokförda verifikationer eller ta bort något. Användaren granskar och bokför själv i Numera.

## 1. Finns kopplingen redan?

Leta efter Numeras verktyg (namnen slutar på `get_company`, `list_drafts`, `get_voucher`, `list_vouchers`, `search_accounts`, `account_balances` och `propose_booking`). Finns de: anropa `get_company` och gå till steg 3.

## 2. Om verktygen saknas

Förklara de två sätten och låt användaren välja. Installera bara ett av dem, båda heter `numera` i Claude Code.

**Via Numeras server (fungerar på alla datorer):**
1. I Numera: Inställningar, Numera-konto, Claude och ChatGPT (appen) eller Inställningar, Claude och ChatGPT (webben). Skapa en koppling, läs varningen och kryssa i att bokföringen delas med Claude.
2. Kopiera adressen som visas (den visas bara en gång).
3. I Claude Code: `/plugin install numera-server@numera` och klistra in adressen när Claude Code frågar efter "Adress från Numera". Den sparas i datorns nyckelring.

**Via Numera-appen på Macen:**
1. Lägg Numera i Program-mappen.
2. I Numera: Inställningar, AI-hjälp, slå på "Låt Claude och ChatGPT hjälpa till".
3. I Claude Code: `/plugin install numera-mac@numera`.

Be användaren starta om Claude Code (eller köra `/reload-plugins`) och kör sedan `get_company`.

## 3. Bekräfta

Visa i två eller tre meningar: företagets namn, företagsform, om bokföringen är i testläge eller låst läge, och hur många utkast som väntar. Föreslå sedan `/numera:start` för en översikt eller `/numera:bokfor` om det finns utkast.

## Säkerhet

- Adressen till servern är en nyckel. Skriv aldrig ut den i svaret, spara den inte i filer och lägg den aldrig i ett git-repo. Har den kommit ut: ta bort kopplingen i Numera och skapa en ny.
- Bokföringen skickas till Anthropic när Claude läser den. Det har användaren godkänt i Numera.
