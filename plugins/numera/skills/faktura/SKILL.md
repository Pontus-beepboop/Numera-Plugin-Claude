---
name: faktura
description: Skapar en faktura eller offert i Numera från det användaren berättar (kund, vad som sålts, pris), gör den klar när användaren ber om det och säger hur den kan skickas. Använd när användaren vill fakturera en kund, skapa en offert eller undrar hur en faktura skickas.
---

# Ny faktura

## Arbetsgång

1. Anropa `get_company` för företagsform, metod och om företaget är momsregistrerat.
2. Hitta kunden med `list_customers`. Finns den inte: fråga användaren om namn, organisationsnummer och e-post, och skapa den med `create_customer` först när användaren har sagt ja.
3. Skapa utkastet med `create_invoice_draft`: en rad per vara eller tjänst, med antal, enhet, à-pris utan moms och momssats. Fråga om något avgörande saknas (pris, antal, moms på tjänsten). Utkastet får inget nummer och bokförs inte.
4. Visa utkastet kort: kund, rader, summa med och utan moms, förfallodag.
5. Gör fakturan klar med `issue_invoice` **bara när användaren ber om det** ("gör den klar", "skicka den"). Den får då nummer och OCR och bokförs med fakturametoden (med kontantmetoden bokförs den när den är betald).
6. Anropa `invoice_send_options` och säg hur den kan skickas och vad Numera föreslår:
   - E-faktura och e-post: e-fakturan går in i kundens ekonomisystem och kunden får samma faktura som PDF i mejlen.
   - E-faktura (Peppol): kommuner, regioner och myndigheter tar bara emot e-faktura.
   - E-post från Numera.
   - Ladda ner som PDF och skicka själv.
7. Avsluta med att användaren skickar den själv: öppna fakturan under Fakturor i Numera och välj **Skicka fakturan**.

## Principer

- Du skickar aldrig fakturan, och du utfärdar den bara när användaren ber om det.
- Priser och belopp kommer från användaren eller Numeras artikelregister, gissa inte.
- Fel i en utfärdad faktura rättas med en kreditfaktura (`create_credit_note`), inte genom att ändra den.
