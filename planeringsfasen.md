# Inlämning 1 - Planeringsfasen

SYSTEMFLÖDE - STRIDE/ESTRID
```text
                                           --------------------------------------------------------------------------------------------------------------------------------------------------
         O                                 |           1ES                       T                              3E                               T                          5E              |
+-----------------+      TRD / Öppnar      |  +----------------------+      HTTP-anrop      +--------------------------------------+     Läser / sparar data      +----------------------+  |
|                 |                        |  |                      | -------------------> |                                      | -------------------------->  |                      |  |
|     Browser     | ---------------------> |  |       Frontend       |                      |        Express / Backend & API       |                              |       Databas        |  |
|                 |                        |  |                      | <------------------- |                                      | <--------------------------  |                      |  |
+-----------------+                        |  +----------------------+           I          +--------------------------------------+             I                +----------------------+  |
                                           |                                 JSON-svar                                                      Svar med data                                   |
                                           --------------------------------------------------------------------------------------------------------------------------------------------------
```
Kommentar: I ursprunglig bild var det bara en enkel pil mellan Browser och Frontend. Därför har vi utgått från det.

Uppgift 1 — Identifierade hot & säkerhetsrisker
-autentisering
-behörighet
-datainmatning
-datalagring
-användarmissbruk

1. Obehörig åtkomst till konto
    Hot: Angripare försöker logga in på andra användares konton genom gissade lösenord eller läckta uppgifter. t.ex. genom cridential stuffing eller brute force.
    Risk: Kontokapning och åtkomst till privata meddelanden.
2. Användare redigerar någon annans meddelanden
    Hot: En användare manipulerar anrop eller ID:n för att redigera meddelanden som tillhör andra användare.
    Risk: Integritetsproblem och manipulation av innehåll.
3. Skadlig kod i meddelanden (XSS)
    Hot: Användare skickar JavaScript eller HTML i meddelanden som körs i andra användares webbläsare.
    Risk: Stulna sessioner eller omdirigering till skadliga sidor.
4. SQL-injection
    Hot: Angripare skickar manipulerad input i formulärfält för att påverka databasen.
    Risk: Datastöld, modifiering eller borttagning av information.
5. Spam eller missbruk av meddelandefunktion
    Hot: Automatiserade konton skickar stora mängder meddelanden.
    Risk: Belastning på systemet och försämrad användarupplevelse.

Uppgift 2 — Säkerhetskrav i kravspecifikationen
1. Systemet ska kräva autentisering med användarnamn och lösenord innan användaren får skapa, redigera eller ta bort meddelanden.
2. Användare ska endast kunna redigera och ta bort sina egna meddelanden. Viktigt att detta även valideras i backend så att det inte bara tar bort “ändraknappen” i frontend.
3. Lösenord ska lagras hashade (gärna med salting) och inte i klartext i databasen.
4. Systemet ska validera och sanera användarinmatning för att förhindra XSS och SQL-injection.
5. Meddelanden ska vara minst 3 och maximalt 140 tecken långa. Både frontend och backend.
6. Systemet ska automatiskt logga ut användaren efter en period av inaktivitet.
7. Systemet ska begränsa antalet misslyckade inloggningsförsök från samma konto eller IP-adress.
8. All kommunikation skall ske krypterat över HTTPS.