# Bestaande tools (GitHub & vergelijkbaar)

Per tool: link, wat het is, en hoe het zich verhoudt tot jouw idee.
(Verzameld via web/GitHub-zoekopdrachten, juni 2026.)

---

## Dichtst bij jouw idee

### Quillra — `kanbon/quillra`
https://github.com/kanbon/quillra

- **Wat:** "GitHub-native CMS" om sites aan klanten over te dragen. Klant opent
  chat, zegt bv. *"verander de homepage-hero naar 'Welkom lente'"*, ziet live
  preview, klikt **Publish**, bestaande CI deployt.
- **Lijkt op jou:** chat-first editen in gewone taal, live preview, echte
  git-commits per wijziging, leden zien alleen hun eigen projecten, self-host.
- **Verschil:** Publish = `git push` naar **jouw bestaande pipeline** (Pages,
  Vercel, Netlify, Cloudflare, VPS). **Geen SFTP-deploy.** Staging-branch +
  preview-URL en een approval-queue staan op de **roadmap**, nog niet af.
- **Relevantie:** Hoogste. Bekijk dit eerst — qua UX bijna jouw product.

### Avocado Studio — `avocadostudio-ai/avocado`
https://github.com/avocadostudio-ai/avocado

- **Wat:** "AI content-ops voor websites." Plant, valideert en past
  gestructureerde edits toe met live preview, undo/redo en one-click publish.
- **Lijkt op jou:** **plan-review + goedkeuring** (niets gaat live zonder akkoord),
  **gestructureerde edits**, SQLite-state met backups, versie-log + rollback.
- **Verschil:** gericht op **Next.js 15+ via een Site SDK** (geen losse
  HTML/CSS/JS-bestanden + SFTP). Publishen via git-snapshots + Vercel/Netlify
  deploy hooks. Wel `PublishTarget`-interface (zou je naar SFTP kunnen uitbreiden).
- **Relevantie:** Hoog, vooral als referentie voor architectuur (plan→approve→publish).

### SiteBuilder — `dx-tooling/sitebuilder-webapp`
https://github.com/dx-tooling/sitebuilder-webapp · https://dx-tooling.org/sitebuilder/

- **Wat:** Symfony-webapp voor AI-content-editen. Niet-technische teams editen via
  chat; engineers houden git/PR-review.
- **Lijkt op jou:** projecten met git-repos, geïsoleerde workspaces, chat-edit,
  review vóór live, transparante AI-kosten.
- **Verschil:** wijzigingen landen als **GitHub PR** (review/merge-flow), PHP/Symfony
  i.p.v. Next.js, geen SFTP-deploy, geen multi-client agency-model expliciet.
- **Relevantie:** Middel — sterk als het om "git verborgen achter review" gaat.

### A3lix — `a3lix/a3lix`
https://github.com/a3lix/a3lix · https://a3lix.com

- **Wat:** open-source "AI Agent CMS" voor Jamstack/statische sites. Vraag wijziging
  aan → agent edit code in GitHub → aanvrager bevestigt deploy met **YES/NO**.
- **Lijkt op jou:** plain-language request, expliciete goedkeuring, live-URL terug.
- **Verschil:** deploy via **Cloudflare Pages** op push naar main; werkt via
  Telegram-achtige flow; geen SFTP, geen staging-map-aanpak.
- **Relevantie:** Middel — goede referentie voor approve-gate.

---

## AI-CMS varianten (meest git/markdown-based)

### agntcms — `agntcms/agntcms`
https://github.com/agntcms/agntcms — Next.js + Claude Code. Drafts, version
history, asset management, inline-edit, **section replace**, **rollback = één
skill-call**. Drafts in git. Gedreven door Claude Code Desktop (skills-based).

### GitCMS — https://gitcms.dev/
Markdown-first, repo-backed CMS. Content board met drafts/approvals, AI-agent
update bestanden, git = source of truth. Vooral voor blog/docs/changelog.

### Barka — `barkajs/barka`
https://github.com/barkajs/barka — "AI-native content-as-code CMS". Markdown/YAML,
git-versionering, optioneel SQLite-adminpaneel, deploy als statische site.

### Decap CMS — `decaporg/decap-cms`
https://github.com/decaporg/decap-cms — Klassieke git-based CMS voor static site
generators (geen AI-kern, wel referentie voor git-as-backend + content-UI).

---

## Multi-tenant / agency headless CMS

### Sigil CMS — `Netrun-Systems/sigil-cms`
https://github.com/Netrun-Systems/sigil-cms — **Native multi-tenancy** via
PostgreSQL Row-Level Security: één deployment, oneindig klanten, geïsoleerde
sites/users/media, tenant-switcher, **site cloning** (klant onboarden in één klik),
audit-log. AI design-generatie. **Maar:** headless DB-CMS, geen "AI edit raw
HTML/CSS/JS + SFTP".

### Webiny — https://www.webiny.com/headless-cms
Enterprise headless CMS, **multi-tenant** (één instance, vele projecten),
versiebeheer met rollback en approval-flows. Zwaarder/enterprise.

### KernCMS — `fiioonnn/kerncms`
https://github.com/fiioonnn/kerncms — Next.js + SQLite/Drizzle, git-based,
**multi-project dashboard voor agencies/freelancers**, "Smart Scan" zet
hardcoded strings om naar CMS-content.

---

## Deploy/hosting-laag (relevant voor jouw SFTP + staging→prod + rollback)

### htmlctl — https://futurelab.studio/htmlctl/
"Website publishing for agents." Push naar **staging** eerst, controleer exact
artifact, **promote** datzelfde artifact naar **prod** (geen rebuild = geen drift),
**rollback via symlink-switch**, expiring preview-URL, builds vanaf gepinde git-SHA.
Go-binaries + SQLite + Caddy. Heel dicht bij jouw staging→approve→prod→rollback-deel.

### apod — `aystro-com/apod`
https://github.com/aystro-com/apod — Eén binary die een VPS in hostingplatform
verandert. **Git deploys met rollback + automatische pre-deploy backup**, backups
naar **S3/R2/SFTP/local**, multi-user met isolatie + ownership enforcement,
chrooted SFTP per user. Relevant voor het deploy/backup/rollback-mechanisme.

### gitftp-deploy — https://gitftp-deploy.com/
Tracker die git-wijzigingen via **FTP/FTPS/SFTP** naar shared hosting pusht
(alleen gewijzigde bestanden). Bevestigt dat "git lokaal houden + via SFTP
deployen naar `public_html`" een gangbaar patroon is.

### Ultra Web Hosting — AI + (S)FTP deploy docs
https://docs.ultrawebhosting.com/ai/ftp-deployment — Beschrijft exact jouw
staging→prod-patroon met SFTP: `remotePath` naar `/public_html/staging`, na
goedkeuring naar `/public_html`. `.git` wordt genegeerd bij upload (git blijft
lokaal/verborgen). Goede referentie, geen product.

---

## In-browser / overlay edit-agents (ander UX-model)

- **Frontman** — `frontman-ai/frontman` (https://frontman.sh): open-source AI
  coding agent in de browser; klik element, beschrijf wijziging, edit bronbestand
  met hot-reload. Alleen in **dev mode**, geen klant-deploy-flow.
- **Pyanchor** — `pyanchor/pyanchor`: Express-sidecar met in-page overlay; modus
  `apply` of `pr`. Prod-attached, self-hosted.

---

## Niet open-source maar conceptueel bijna identiek

### Claude CMS — https://claudecms.com/
CMS volledig bediend door Claude. Maakt pagina's, schrijft CSS, beheert bestanden
op je server, deployt direct. **Git-free deploy met automatische backups +
rollback-support**, **bestands-whitelist** (toegestane extensies), beschermde
bestanden read-only, PHP syntax-check vóór write, **auto-backup bij elke write**.
Dit raakt heel veel van jouw "safety"-eisen — closed source, maar sterke
referentie voor het ontwerp.
