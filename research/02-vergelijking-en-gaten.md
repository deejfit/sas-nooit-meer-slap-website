# Vergelijking met jouw idee, gaten & conclusie

## Jouw kernfeatures vs. bestaande tools

Legenda: Ja = aanwezig, Deels = gedeeltelijk/roadmap, Nee = afwezig.

- **Plain-language change request (klant typt wens)**
  - Quillra: Ja · Avocado: Ja · SiteBuilder: Ja · A3lix: Ja · agntcms: Ja
- **AI past echte bestanden aan (gestructureerd)**
  - Quillra: Ja · Avocado: Ja (plan+validate) · SiteBuilder: Ja · A3lix: Ja
- **Staging-preview vóór live**
  - Quillra: Deels (roadmap) · Avocado: Ja (live preview) · SiteBuilder: Ja (PR/preview)
    · A3lix: Deels · htmlctl: Ja (pinned preview)
- **Expliciet goedkeuren naar productie**
  - Quillra: Deels (approval-queue roadmap) · Avocado: Ja · SiteBuilder: Ja (merge)
    · A3lix: Ja (YES/NO)
- **Rollback naar eerdere versie**
  - Quillra: Ja (git history) · Avocado: Ja (undo/redo + version log) · agntcms: Ja
    · htmlctl: Ja (symlink) · apod: Ja · Claude CMS: Ja
- **Git intern, verborgen voor klant**
  - Quillra: Deels (klant logt in met GitHub) · Avocado: Ja · SiteBuilder: Deels (PR-model)
    · Claude CMS: Ja (git-free voor klant)
- **Deploy via SFTP naar staging/prod-mappen**
  - Quillra: Nee · Avocado: Nee (wel pluggable) · SiteBuilder: Nee · A3lix: Nee
    · apod: Deels (SFTP backups) · gitftp-deploy: Ja (FTP/SFTP) · Ultra docs: Ja (patroon)
- **Multi-client agency (klanten × projecten, isolatie)**
  - Sigil: Ja (RLS) · Webiny: Ja · KernCMS: Ja · Quillra: Deels (per-project members)
    · Avocado: Nee (per-site)
- **Simpele losse HTML/CSS/JS (geen framework/SSG vereist)**
  - Quillra: Deels (kan Astro-migratie forceren) · Avocado: Nee (Next.js SDK)
    · htmlctl: Ja · Claude CMS: Ja · gitftp-deploy: Ja

## Wat opvalt

1. **Het AI-edit + approve + rollback-concept is "solved territory".** Meerdere
   actieve, soms productie-rijpe projecten doen dit al goed (Quillra, Avocado,
   SiteBuilder, A3lix). Het pure idee is dus niet nieuw.

2. **Bijna iedereen deployt via git push + CI (Vercel/Netlify/Cloudflare/Pages).**
   Dat is de moderne Jamstack-aanname. Jouw aanpak — **SFTP naar `public_html`-style
   mappen** — is juist gericht op **klassieke/shared hosting**, en dat doet vrijwel
   geen enkele AI-CMS out-of-the-box.

3. **Multi-tenancy bestaat**, maar in de zwaardere headless-CMS-hoek (Sigil, Webiny,
   KernCMS), niet gecombineerd met "AI edit raw static files + SFTP".

4. **Veel safety-eisen van jou (whitelist extensies, backup vóór write, syntax-check,
   path-veiligheid)** zie je terug bij Claude CMS en Avocado — goede blauwdrukken.

## Het echte "gat" (jouw mogelijke onderscheid)

De combinatie die **niemand** kant-en-klaar levert:

> **Agency-tool voor niet-technische klanten met simpele statische pagina's op
> klassieke (S)FTP-hosting**, waar AI de bestanden bewerkt, git volledig verborgen
> blijft, en deploy/rollback via **SFTP naar staging- en productie-mappen** gaat —
> met meerdere klanten en projecten in één installatie.

Vooral het **SFTP-deploy-kanaal** + **shared-hosting-doelgroep** + **multi-client**
is de niche die open-source nog niet invult.

## Opties / conclusie

- **Optie A — Niet zelf bouwen, bestaande tool gebruiken/forken.** Als git-push +
  Vercel/Netlify acceptabel is, is **Quillra** of **Avocado Studio** waarschijnlijk
  sneller dan from-scratch. Avocado's `PublishTarget`-interface zou je naar SFTP
  kunnen uitbreiden i.p.v. alles zelf te schrijven.

- **Optie B — Wel bouwen, maar bewust voor de niche.** Bouw je MVP juist omdat je
  doelgroep op **shared hosting met SFTP** zit (geen CI/Vercel). Dan is je
  onderscheidende waarde de **SFTP-deploy + verborgen git + multi-client agency**.
  Leen ideeën van htmlctl (staging→promote→rollback) en Claude CMS (whitelist,
  auto-backup, syntax-check).

- **Optie C — Hybride.** Gebruik een bestaande AI-edit-laag/agent voor het edit-deel
  en bouw zelf alleen de **deploy/rollback-orchestratie over SFTP + multi-tenant
  beheer** (het stuk dat ontbreekt).

## Aanrader voor vervolgonderzoek (indien gewenst)

- Quillra en Avocado lokaal draaien en testen of SFTP-deploy + multi-client
  haalbaar/uitbreidbaar is.
- Licenties checken vóór fork/hergebruik: Quillra (self-host), SiteBuilder (BSL),
  Frontman (Apache/AGPL), Decap (MIT), Sigil/KernCMS (AGPL). AGPL/BSL kan
  commercieel beperkend zijn.
