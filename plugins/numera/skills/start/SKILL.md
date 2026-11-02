---
name: start
description: Ger en kort översikt över företaget i Numera på enkel svenska, vinst, moms att betala, pengar på banken, utkast och vad som behöver göras härnäst. Använd när användaren frågar hur det går för företaget eller vill börja jobba med bokföringen.
---

# Översikt över företaget

## Arbetsgång

1. Anropa `get_company`. Läs företagsform, metod (faktura- eller kontantmetoden), momsperiod, testläge/låst läge och översikten.
2. Skriv en kort översikt, högst tio rader, på enkel svenska utan facktermer som inte förklaras:
   - Resultat hittills i år (vinst eller förlust).
   - Moms för pågående period och **sista dag att deklarera och betala**. Räkna inte om momsen själv, använd Numeras siffra.
   - Pengar på banken, vad kunder är skyldiga och vad företaget är skyldigt leverantörer.
   - Beräknad skatt att spara till, om Numera visar en.
   - Hur många utkast som väntar.
3. Avsluta med de en till tre viktigaste sakerna att göra nu, i ordning efter datum. Exempel: "Bokför de 4 utkasten", "Momsen för juli till september ska vara inne 12 november".

## Principer

- Siffrorna kommer alltid från Numera, aldrig från minnet eller egna uppskattningar.
- Säg tydligt om bokföringen är i **testläge** (då är siffrorna övningsdata).
- Ge inga råd om skatteplanering som kräver en redovisningskonsult; säg det i stället.
- Verktygen är bara läsning här. Föreslå `/numera:bokfor`, `/numera:kolla`, `/numera:moms` eller `/numera:manad` som nästa steg.
