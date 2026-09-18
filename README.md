# Talk Shop na GitHub Pages (besplatno, bez servera)

Dvije datoteke: `index.html` (cijela aplikacija) i `sw.js` (offline cache). Nema backend koda.
Na GitHub Pagesu mikrofon radi normalno (stranica nije u iframeu), AI feedback ide s tvojim
Claude API ključem izravno iz preglednika, a napredak se sprema u tajni GitHub gist pa ga
mobitel i računalo dijele.

## 1. Repo i Pages (5 minuta)
1. github.com -> New repository -> ime `talk-shop` -> Public (Pages je besplatan samo za javne repoe; u kodu nema tajni) -> Create.
2. U repou: Add file -> Upload files -> povuci `index.html`, `sw.js` i ovaj README -> Commit changes.
3. Settings -> Pages -> Build and deployment -> Source: "Deploy from a branch" -> Branch: `main`, folder `/ (root)` -> Save.
4. Za minutu-dvije: `https://TVOJ-USERNAME.github.io/talk-shop/` (piše na istoj Pages stranici).

## 2. Mobitel (2 minute)
- iPhone: otvori link u Safariju -> Share -> "Add to Home Screen". Otvori ikonu s početnog ekrana.
- Android: otvori link u Chromeu -> meni (tri točke) -> "Add to Home screen" / "Install app".
- Prvi put kad stisneš mikrofon, dopusti pristup.

## 3. Ključevi u aplikaciji (Deck -> Settings)
- Claude API key: console.anthropic.com -> API Keys -> Create key. U Billing -> Limits postavi mjesečni limit (npr. 10 USD; jedan feedback košta par centi). Zalijepi ključ u "Claude API key". Ostaje samo u tom pregledniku.
- Model: ostavi prazno (koristi `claude-sonnet-5`). Ako Anthropic povuče taj model, upiši noviji s docs.claude.com.
- GitHub token (sync): github.com -> Settings -> Developer settings -> Personal access tokens -> Tokens (classic) -> Generate new token -> označi samo `gist` -> Expiration: No expiration -> Generate -> kopiraj (počinje s `ghp_`). Zalijepi u "GitHub token (sync)". Aplikacija sama napravi tajni gist `talk-shop-state.json` i sprema napredak u njega.
- Na računalu: otvori isti link, zalijepi isti token (i API ključ ako želiš feedback i tamo). Točkica gore desno zelena = sinkronizirano.

## 4. Kako radi sync i backup
- Pri otvaranju app povuče stanje iz gista; ako je gist noviji, uzme njega, inače pošalje svoje.
- Svaka promjena se šalje 2 sekunde nakon zadnje akcije. Zadnji zapis pobjeđuje: ne vježbaj istovremeno na dva uređaja.
- Backup bez gista: Deck -> Export or import -> Copy backup (JSON).

## 5. Ažuriranje aplikacije
Zamijeni `index.html` u repou (Upload files -> isti naziv -> Commit). Pages se sam ponovno objavi.
Napredak je u gistu, ne dira se. Ako stara verzija ostane u cacheu, zatvori app i otvori ponovno.

## 6. Vlastita domena (opcionalno, kasnije)
Settings -> Pages -> Custom domain -> upiši domenu, kod registrara dodaj CNAME na `TVOJ-USERNAME.github.io`. Uključi "Enforce HTTPS".

## Ako nešto ne radi
- "API key was rejected": ključ je krivo zalijepljen ili nema kredita.
- "Claude API error: ... model": upiši ispravan model u Settings.
- Sync crvena točkica: token nema `gist` scope ili je istekao.
- Mikrofon: Deck -> Settings -> "Test the mic" kaže što je. Firefox nema živu transkripciju; koristi Chrome ili Safari.
