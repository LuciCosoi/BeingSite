# Publicarea site-ului pe Cloudflare Pages

Folderul `site/` este site-ul complet, gata de publicat: `index.html`, `resurse.html`, `retea.html`, `styles.css`. Nu are build, nu are dependințe — se încarcă așa cum e.

## Varianta rapidă (fără GitHub, ~10 minute)

1. Creează un cont gratuit pe https://dash.cloudflare.com.
2. În meniu: **Workers & Pages → Create → Pages → Upload assets**.
3. Dă un nume proiectului (ex. `being-ecosystem`) și trage folderul `site/` în fereastră.
4. Deploy. Site-ul e live la `https://being-ecosystem.pages.dev`.

Pentru actualizări: repeți uploadul. Suficient pentru lansare, dar varianta cu GitHub e mai comodă pe termen lung.

## Varianta recomandată (cu GitHub, ~30 minute)

1. Creează un repository pe https://github.com (ex. `being-ecosystem-site`) și urcă conținutul folderului `site/` în rădăcina lui.
2. În Cloudflare: **Workers & Pages → Create → Pages → Connect to Git** → alege repo-ul.
3. Build settings: lasă totul gol (fără framework, fără build command, output directory `/`).
4. Deploy.

De acum, orice `git push` publică automat în ~30 de secunde. Acesta e și fluxul natural cu Claude Code: modifici textele sau layout-ul local, push, live.

## Domeniu propriu

În proiectul Pages: **Custom domains → Set up a custom domain**. Dacă domeniul e administrat tot în Cloudflare, se configurează automat; altfel primești un CNAME de setat la registrar. Gratuit, cu HTTPS inclus.

## Activarea formularelor (HubSpot gratuit)

Formularele (newsletter pe `index.html`, înscrierea în rețea pe `retea.html`) afișează acum un mesaj „se activează la lansare". Ca să le pornești:

1. Cont gratuit pe https://www.hubspot.com (Free Tools — include CRM + formulare).
2. **Marketing → Forms → Create form** — creează două formulare:
   - *Newsletter*: doar câmpul de email.
   - *Înscriere în rețea*: numele organizației, județ (dropdown), email, ce oferă (checkboxes).
3. La fiecare formular: **Share → Embed code** — notează `portalId` (număr) și `formId` (UUID).
4. Completează valorile în `window.HUBSPOT` din `<head>`:
   - `index.html`: `portalId` + `newsletterFormId`
   - `retea.html`: `portalId` + `networkFormId`
   - `region`: `"eu1"` pentru cont european (verifică URL-ul HubSpot: `app-eu1.hubspot.com` → `eu1`; `app.hubspot.com` → `na1`).
5. Push / re-upload. Formularele apar în locul mesajului, iar înscrierile intră direct în CRM-ul HubSpot.

## Imagini

Pozele și logo-urile sunt deocamdată placeholder-e gri. Pentru fiecare există un comentariu în HTML exact deasupra, cu tagul `<img>` de folosit. Pune fișierele într-un folder `assets/` lângă pagini și înlocuiește placeholder-ul cu tagul din comentariu.

## Ce mai e de știut

- Harta județelor (`retea.html`) încarcă geometria din `code.highcharts.com` și D3 din `unpkg.com` — funcționează de oriunde, fără chei API.
- Organizațiile de pe hartă sunt date de lucru, scrise direct în `retea.html` (variabila `ORGS`). Se editează acolo — sau cu Claude Code: „adaugă organizația X în județul Y".
- Footer-ul încă spune „mockup conceptual, iulie 2026" — de schimbat înainte de lansare.
- Cifrele din secțiunea „Ecosistemul în cifre" sunt orientative — de înlocuit cu datele reale.
