# Bestaat "AI Page Manager" al? — Onderzoek

> Doel van dit onderzoek: kijken of er op GitHub al een open-source tool bestaat
> die doet wat jij wilt bouwen (AI-wijzigingen op simpele statische sites voor
> niet-technische klanten, met staging-preview, goedkeuren naar productie en
> rollback, git intern verborgen).

## Korte antwoord

**Ja, het concept bestaat al meerdere keren** — er is in 2025/2026 een hele golf
aan "AI-CMS / chat-to-edit"-tools ontstaan. Bijna allemaal delen ze jouw
kernidee: niet-technische klant typt in gewone taal → AI past de echte bestanden
aan → live preview → publiceren met goedkeuring → git-historie voor rollback.

**Maar:** geen enkele tool combineert exact jouw specifieke keuzes:
- **Deploy via SFTP naar staging/productie-mappen** (de meeste tools doen
  `git push` + Vercel/Netlify/Cloudflare CI, niet SFTP).
- **Git volledig verborgen voor de klant** met SFTP als enige deploy-kanaal.
- **Multi-client agency-model** (meerdere klanten, elk meerdere projecten) in
  combinatie met de simpele HTML/CSS/JS + SFTP-aanpak.

Die specifieke niche (klassieke shared-hosting / SFTP + simpele statische pagina
+ agency met meerdere klanten) is **nog niet 1-op-1 ingevuld**. Er is dus ruimte,
maar je concurreert wel met volwassen alternatieven voor het AI-edit-gedeelte.

## Documenten

- `01-bestaande-tools.md` — overzicht van de gevonden projecten, per stuk.
- `02-vergelijking-en-gaten.md` — feature-vergelijking met jouw idee, wat ontbreekt,
  en conclusie/opties.

## Belangrijkste gevonden projecten (samenvatting)

- **Quillra** (`kanbon/quillra`) — staat het dichtst bij jouw idee: GitHub-native
  CMS, klant chat → AI edit → live preview → Publish; rollen per project; staging
  branch op de roadmap. Deploy = git push naar jouw CI, niet SFTP.
- **Avocado Studio** (`avocadostudio-ai/avocado`) — AI content-ops voor Next.js,
  plan-review + goedkeuring, undo/redo, git-snapshots, pluggable `PublishTarget`.
- **SiteBuilder** (`dx-tooling/sitebuilder-webapp`) — chat-edit → GitHub PR, gericht
  op marketingteams; engineers houden git/PR-workflow.
- **A3lix** (`a3lix/a3lix`) — AI Agent CMS voor Jamstack; wijziging aanvragen,
  YES/NO goedkeuren, deploy via Cloudflare Pages.
- **agntcms**, **GitCMS**, **Barka**, **Decap CMS** — git-based (AI-)CMS-varianten,
  meest markdown-georiënteerd.
- **Sigil CMS**, **Webiny**, **KernCMS** — multi-tenant/agency headless CMS (één
  deployment, veel klanten), maar database/headless i.p.v. "AI edit raw static files".
- **htmlctl**, **apod**, **gitftp-deploy** — deploy/hosting-laag: staging→prod
  promote, rollback, SFTP-backups (relevant voor jouw SFTP-deploy-deel).
- **Claude CMS** (claudecms.com) — Git-free deploy met auto-backup + rollback,
  bestands-whitelist, MCP-tools; conceptueel sterk vergelijkbaar (niet open-source).

Details en links staan in `01-bestaande-tools.md`.
