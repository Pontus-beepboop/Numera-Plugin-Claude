# Numera för Claude

Med det här tillägget kan Claude hjälpa dig med bokföringen i [Numera](https://usenumera.se). Claude kan läsa din bokföring, förklara den på enkel svenska och lägga in förslag på hur kvitton och fakturor ska bokföras.

**Claude bokför när du ber om det, och visar allt den gjort.** Säg "bokför utkasten" eller "gör klart juni", så konterar och bokför Claude och listar varje verifikation den bokfört. Ber du bara om förslag hamnar allt som **utkast** som du bokför själv i Numera.

Det tar ungefär fem minuter att komma igång. Du behöver inte kunna något om programmering.

---

## Det här behöver du

- **Claude-appen** på din dator (Mac eller Windows). Ladda ner den gratis på [claude.com/download](https://claude.com/download).
- **Ett betalt Claude-abonnemang** (Pro, Max, Team eller Enterprise). Tillägg fungerar inte med gratisversionen.
- **Numera**, med ett Numera-konto.

---

## Steg 1: Lägg till Numera i Claude

Det här gör du en gång.

1. Öppna **Claude-appen**.
2. Klicka på **Customize** (Anpassa) i menyn till vänster.
3. Klicka på fliken **Plugins**.
4. Vid **Personal plugins**, klicka på **+** och sedan **Add marketplace**.
5. Välj **Add from a repository**.
6. Klistra in den här texten exakt som den står och klicka på **Sync**:

   ```
   Pontus-beepboop/Numera-Plugin-Claude
   ```

Nu finns **Numera** i listan över tillägg.

> Får du felet "sync failed": kontrollera att du klistrade in texten ovan utan `https://` framför och utan mellanslag.

---

## Steg 2: Koppla Claude till din bokföring

Välj **ett** av sätten nedan.

### A. Du använder Numera-appen på en Mac (enklast)

1. Flytta **Numera** till mappen **Program** om den inte redan ligger där.
2. Öppna Numera och gå till **Inställningar → AI-hjälp**. Slå på **Låt Claude och ChatGPT hjälpa till**.
3. I Claude-appen, gå till **Customize → Plugins**, öppna **Numera** och klicka på **Install** vid **Numera på Mac**.
4. Stäng Claude-appen helt (⌘Q) och öppna den igen.

### B. Du använder Numera på webben, på Windows eller bara på iPhone

1. Logga in på [app.usenumera.se](https://app.usenumera.se) (eller öppna Numera-appen).
2. Gå till **Inställningar → Claude och ChatGPT** (i appen: **Inställningar → Numera-konto → Claude och ChatGPT**).
3. Klicka på **Skapa koppling**, läs varningen och godkänn.
4. **Kopiera adressen** som visas. Den visas bara en gång, så låt fönstret vara öppet tills du är klar.
5. I Claude-appen, gå till **Customize → Connectors**, klicka på **+** och välj **Add custom connector**.
6. Skriv **Numera** som namn, klistra in adressen och klicka på **Add**.
7. Gå sedan till **Customize → Plugins**, öppna **Numera** och klicka på **Install** vid **Numera** (arbetsflödena).

> Adressen är som en nyckel till din bokföring. Dela den inte med någon. Har den kommit ut: ta bort kopplingen i Numera och skapa en ny.

---

## Steg 3: Prova

Starta en ny chatt i Claude och skriv till exempel:

- *Hur går det för mitt företag?*
- *Bokför mina utkast i Numera*
- *Kolla om något saknas i bokföringen*

Du kan också skriva **/** i chatten och välja ett av Numeras kommandon i listan:

| Kommando | Vad det gör |
|---|---|
| **setup** | Kontrollerar att kopplingen fungerar och hjälper dig om något saknas |
| **foretag** | Sätter upp ett nytt företag i chatten: slår upp organisationsnumret och frågar bara det som saknas |
| **start** | Kort översikt: vinst, moms att betala och sista dag, pengar på banken, utkast |
| **bokfor** | Föreslår hur dina kvitton och fakturor ska bokföras och bokför när du ber om det. Ge Claude en bild eller PDF av ett kvitto så läggs den in i Numera |
| **kolla** | Kör Numeras kontroller och letar efter fel och luckor, också i lönerna. Ändrar ingenting |
| **moms** | Hjälper dig förbereda momsdeklarationen |
| **dagskassa** | Dagens försäljning med kort, Swish, kassa, Zettle och Stripe: lägger in dagar som utkast, läser av Z-rapporter och bokar utbetalningar |
| **manad** | Går igenom månaden: utkast, banken, fakturor, löner och moms |

Förslagen dyker upp under **Utkast** i Numera. Öppna dem, kontrollera och tryck på **Bokför**.

---

## Om något inte fungerar

| Problem | Gör så här |
|---|---|
| Claude säger att den inte hittar Numera | Stäng Claude-appen helt och öppna den igen. Skriv sedan *Hjälp mig koppla Numera* och följ instruktionerna. |
| Sätt A: inget händer | Kontrollera att Numera ligger i **Program** och att **Låt Claude och ChatGPT hjälpa till** är påslaget. Numera behöver inte vara öppet, det startar av sig självt. |
| Sätt B: "kan inte ansluta" | Adressen kan ha kopierats fel. Ta bort kopplingen i Claude (**Customize → Connectors**), skapa en ny koppling i Numera och lägg till den igen. |
| Jag hittar inte **Add from a repository** | Uppdatera Claude-appen till senaste versionen. |
| Något annat | Mejla [support@usenumera.se](mailto:support@usenumera.se). |

---

## Bra att veta

- När Claude läser din bokföring skickas den till Anthropic (företaget bakom Claude). Numera varnar och ber om ditt godkännande innan kopplingen skapas.
- Claude bokför bara när du ber om det. Varje verifikation som Claude bokför märks "Bokförd av Claude" och syns i behandlingshistoriken. Claude kan inte ändra något som redan är bokfört och inte ta bort något; ett fel rättar du med knappen Rätta i Numera.
- Numera kontrollerar varje förslag (att debet och kredit går jämnt ut, att kontona finns och att momsen stämmer med företagets inställningar).
- Numera och Claude är hjälpmedel. Kontrollera alltid momsdeklarationen innan du skickar in den, och låt gärna en redovisningskonsult titta på bokslutet.
