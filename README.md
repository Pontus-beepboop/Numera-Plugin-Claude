# Numera för Claude Code

Plugin-marknad för [Numera](https://usenumera.se), ett enkelt svenskt bokföringsprogram för enskild firma och aktiebolag. Med pluginen kan Claude Code läsa din bokföring och lägga in förslag som **utkast**. Claude bokför aldrig, ändrar aldrig bokförda verifikationer och tar aldrig bort något. Du granskar och bokför själv i Numera.

## Installera

```
/plugin marketplace add Pontus-beepboop/Numera-Plugin-Claude
```

Välj sedan **ett** av sätten att koppla till Numera:

| Plugin | När | Vad som behövs |
|---|---|---|
| `numera-server` | Alla datorer, webben | En adress från Numera: Inställningar, Claude och ChatGPT, skapa koppling. Klistras in när Claude Code frågar och sparas i nyckelringen. |
| `numera-mac` | Numera-appen på samma Mac | Numera i Program-mappen och "Låt Claude och ChatGPT hjälpa till" påslaget under Inställningar, AI-hjälp. |

```
/plugin install numera-server@numera
```

eller

```
/plugin install numera-mac@numera
```

Arbetsflödena (`numera`) installeras automatiskt med.

## Kommandon

| Kommando | Gör |
|---|---|
| `/numera:setup` | Kopplar och kontrollerar att allt fungerar |
| `/numera:start` | Översikt: vinst, moms med sista dag, banken, utkast |
| `/numera:bokfor` | Lägger in kontering med förklaring i utkasten |
| `/numera:kolla` | Kontrollerar bokföringen utan att ändra något |
| `/numera:moms` | Förbereder momsdeklarationen |
| `/numera:manad` | Månadsavslut med bankavstämning |

## Säkerhet

- Bokföringen skickas till Anthropic när Claude läser den. Numera varnar och ber om ett godkännande innan kopplingen skapas.
- Adressen till Numeras server är en nyckel. Ta bort kopplingen i Numera om den kan ha kommit ut.
- Allt Claude föreslår kontrolleras av Numera (debet = kredit, kontona finns, metod och momsregistrering) och visas som utkast.

## Ansvar

Numera är ett hjälpmedel. Låt gärna en redovisningskonsult granska bokslutet.
