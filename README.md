# ICT-chatbot Maaswaal College – prototype

## Inhoud
- `index.html`, `styles.css`, `app.js`: website, werkt met 38 antwoorden ook zonder AI.
- `faq.json`: 38 items geëxtraheerd uit het aangeleverde PDF-document.
- `functions/api/chat.js`: beveiligde serverfunctie voor Gemini AI en optioneel Google Search.
- `source.txt`: geëxtraheerde tekst uit PDF om controle mogelijk te maken.

## Testen op eigen computer
Open een terminal in deze map en start `python -m http.server 8000`. Ga naar `http://localhost:8000`. Let op: de FAQ werkt; de AI is dan nog niet beschikbaar.

## Publiceren met Cloudflare Pages
1. Maak een gratis Cloudflare-account of gebruik je bestaande.
2. Zet alle bestanden, inclusief de map `functions`, in een nieuwe GitHub-repository. Zet geen API-sleutels in GitHub.
3. Maak in Cloudflare bij **Workers & Pages > Create > Pages > Connect to Git** een project met deze repository. Gebruik geen buildcommand en stel de output directory in op `.` (de root van de repository).
4. Publiceer. De site krijgt een `*.pages.dev`-adres. Dan werkt de schoolkennisbank zonder AI.
5. Voor AI: maak bij https://aistudio.google.com/apikey een Gemini API-sleutel aan. Controleer de privacyvoorwaarden en limieten; gratis gebruik en Google Search zijn niet onbeperkt.
6. Voeg bij Cloudflare Pages **Settings > Variables and Secrets** de versleutelde secret `GEMINI_API_KEY` toe. Maak daarna een nieuwe deployment. Optioneel `GEMINI_MODEL` aanpassen als het standaardmodel niet meer beschikbaar is. De sleutel hoort uitsluitend op de server.
7. Test beide modi en vraag de FG/privacyfunctionaris om een privacy- en leveranciersbeoordeling vóór gebruik met leerlingen. Schakel voor productielancering een rate-limit binding `RATELIMIT` en eventueel botbescherming in. Beperk kosten via je Google-project indien beschikbaar.

## Technische beperkingen en aandachtspunten
- De internetzoekfunctie gebruikt Gemini Google Search grounding als die beschikbaar is in het gekozen API-abonnement/model. De AI werkt pas na configuratie van de API-sleutel. Beschikbaarheid en gratis limieten veranderen.
- De client geeft zes relevant geachte kennisbankregels mee als context. Een ongebruikelijke formulering kan daardoor een schoolantwoord missen. Test daarom alle 38 vragen en varianten vóór schoolbreed gebruik.
- De chatbot kan inhoudelijk fouten maken. Controleer AI-bronnen en laat leerlingen geen persoonlijke gegevens invoeren.
- Bij activatie van AI worden leerlingvragen naar Google's Gemini API verzonden. Een gratis AI-API kan voor een school-AVG-beoordeling ongeschikt zijn. Laat dit eerst beoordelen.
- Geen server-side gespreksopslag ingebouwd. Cloudflare en Google kunnen wel technische logging of gegevensverwerking uitvoeren; raadpleeg de voorwaarden.
- Bevestig dat de openingstijden en overige schoolprocedures uit de PDF nog actueel zijn. De bron vermeldde 38 en geen 60 vragen.
- Enkele bronantwoorden noemen Teams of uniFLOW zonder een expliciete URL. Die worden niet als officiële URL verzonnen.
- Gebruik Git-integratie: een statische drag-and-drop Pages-upload neemt niet zonder meer Pages Functions mee.
