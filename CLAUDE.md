# DevisArtisans (devisartisans.shmor.ai)

A Shmor marketplace (shared rules in `../../CLAUDE.md`): its own brand, design and SEO. **The network's first French-language site, for the French market.** It helps homeowners in mainland France find an artisan (plombier, électricien, couvreur…) and compare free quotes, then refers them to quote platforms for a lead commission. Modelled on ProFinders (`../shmor-profinders/`), with trades and regions taken from **Travaux.com** (Instapro group), the main referral target. Repo: `Shmorai/shmor-devisartisans` (private until launch). Status: **building**, no referral links yet.

## Language
- **Everything is in French**, including meta, breadcrumbs ("Accueil"), FAQs, 404 and search. `shmor-site.json` → `seo.locale: "fr"` switches the site kit's built-in French word pack (kit `tools/build.js` → `WORDS.fr`; any word can be overridden with `seo.strings`). `ogLocale: "fr_FR"`, `<html lang="fr">`.
- Write in French with "vous", French typography (no-break space before `: ? !`, « guillemets », ’ apostrophes) and French terms (devis, SIRET, décennale, RGE, MaPrimeRénov’). The US/UK/EU wording rule in `../../CLAUDE.md` does not apply here.
- Legal pages are French and on this site (see "Legal pages" below); the footer's "À propos" column links to them.

## Where things are
| What | Where |
|---|---|
| Card on shmor.ai, search keywords, **referral links**, offers, SEO defaults | `shmor-site.json` |
| Pages (1 JSON file = 1 Google landing page) | `content/` (`home.json` = homepage) |
| Design: header, logo, footer (footer lists are **hand-written**) | `templates/layout.html` |
| Design: styles | `assets/site.css` (kit defaults at the top; **DevisArtisans theme** block at the bottom) |
| Generated output (don't edit by hand) | `index.html`, `*/index.html`, `sitemap.xml`, `robots.txt`, `404.html`, `search/`, `search-index.json` |

## Pages (107)
- Home · `comment-ca-marche` · `metiers` hub · `regions` hub · `guides` hub · `blog` index.
- **30 trades** `metiers/<slug>` (the most-requested categories on Travaux.com): plombier, electricien, couvreur, peintre, macon, chauffagiste, pompe-a-chaleur, climatisation, menuisier, carreleur, plaquiste, jardinier-paysagiste, serrurier, renovation, isolation, charpentier, facadier, cuisiniste, salle-de-bain, pisciniste, vitrier, terrassier, ramoneur, nettoyage, demenageur, diagnostiqueur, panneaux-solaires, poele-a-bois, parquet, veranda. Each covers: ce que fait…, quand faire appel…, questions à poser, ce qui fait varier le prix, règles et précautions, plus FAQs.
- **Service cards**: 53 popular "prestations" (from Travaux.com's activity list) as icon cards (`deals` blocks with class `svc`), grouped into 8 categories on the `metiers` hub. The 16 most requested are also on the homepage. Each card links to its trade page.
- **13 regions** `regions/<slug>`: every region of mainland France, Corsica included (Travaux.com covers mainland France; no DROM). Each lists its departments with numbers and its main cities, then covers local building styles and materials, natural risks (linked to Géorisques), France Rénov’/ADIL advice and a region-specific FAQ.
- **10 guides** `guides/<slug>`: verifier-un-artisan, devis-travaux, garanties-travaux, aides-renovation, preparer-son-projet, budget-travaux, urgence-depannage, travaux-locataire-proprietaire, assurances-et-travaux, renovation-energetique-par-ou-commencer.
- **Astuces** hub `astuces`: 36 tip cards in 6 themes (avant de signer, pendant le chantier, économies d’énergie, entretien, urgences, voisinage), each linking to a guide, post or trade page. Every trade page also has an "Astuces de pro" section (3 tips).
- **Blog**: 44 posts (24 in the first batch, plus 20 more on 2026-10-15 dated between them, 2026-03-08 → 2026-10-14) `blog/<slug>` (about 280–500 words each, with sources), dated every 9–10 days from 2026-03-03 to 2026-10-10 at the user's request ("backdated"). Content is evergreen, so the facts don't depend on the date shown. Homepage shows the 6 latest. RSS at `/blog/feed.xml`.
- **3 legal pages**: `mentions-legales`, `confidentialite`, `cookies` (see below).
- Homepage blocks: key-figures strip under the hero, 16 popular services, 6 trade photo tiles, 6 "Astuces du moment", 13 region pills, steps, 10 guide pills, 6 latest posts.
- Top menu: Métiers, Régions, Guides, Astuces, Blog, Comment ça marche + "Demander un devis" pill (written in `layout.html`, links to /metiers/ until a referral link exists).
- **French typography**: content strings use a no-break space before `? ! : ;` and inside « ». Keep doing this when editing content, or the "?" can wrap onto its own line.

## Legal pages (French law / CNIL)
- `content/mentions-legales.json` (LCEN: éditeur, directeur de la publication, hébergeur GitHub Pages, contact, activité, responsabilité, propriété intellectuelle; it also stands in for "conditions d'utilisation"), `content/confidentialite.json` (RGPD art. 13: responsable, données, bases légales, destinataires, transferts DPF/CCT, durées, droits incl. directives post-mortem, CNIL complaint), `content/cookies.json` (site sets **no** cookies or storage, so no banner).
- **Placeholders** are `<mark class="todo">[À compléter : …]</mark>` (styled in `site.css`): company name, legal form and capital, registration number, registered office, TVA number, phone, directeur de la publication, GitHub's phone number, the email provider, and the EU representative (RGPD art. 27, needed if the company is outside the EU, e.g. a UK company). Fill them **only with details the user gives**; master `../../shmor-ai/assets/js/config.js` → `SITE.company` is still unfilled. Remove the marks before launch.
- Contact emails used: hello@shmor.ai, privacy@shmor.ai (from master `SITE.emails`); make sure these mailboxes exist.
- What the privacy/cookie pages say must stay true: no cookies, no localStorage, no analytics, no forms; IPs go to GitHub (host), Google Fonts and Unsplash (images). If any of that changes (a form, self-hosted fonts, analytics), update both pages.
- **If analytics or any consent-based tracker is ever added**: follow CNIL rules: nothing loads before consent; "Tout refuser" as easy and visible as "Tout accepter" (same level, same look); browsing on ≠ consent; choice kept 6 months; a "Gérer mes cookies" footer link to change it at any time; list each cookie (name, émetteur, finalité, durée ≤ 13 months) on `/cookies/`. Rewrite the cookies page's "Si nous ajoutons…" section into the real list.

## Facts and sources (keep content genuine)
Checked 2026-10-15: devis obligatoire avant dépannage/réparation/entretien (arrêté du 24 janvier 2017, in force since 1 April 2017, 150 € threshold removed); décennale (service-public.gouv.fr F2034: insurance before the site opens, certificate attached to devis and factures); parfait achèvement 1 an / biennale 2 ans / décennale 10 ans (Code civil 1792-6, 1792-3, 1792); TVA 5,5 % rénovation énergétique / 10 % amélioration (logement > 2 ans); démarchage téléphonique rénovation énergétique interdit depuis 2020; entretien chaudière annuel (4–400 kW), PAC tous les 2 ans (4–70 kW); Consuel; IRVE > 3,7 kW; A2P; art. 671 Code civil.
**MaPrimeRénov’ amounts are deliberately not quoted** because sources disagreed for 2026. Pages describe the schemes and link to france-renov.gouv.fr. No prices, review counts or artisan numbers anywhere.

## Design (v2, 2026-10-15: "professionnel français", modelled on cj.com's layout)
The user asked for a more professional French look using CJ Affiliate (cj.com) as the guide. It now has very large tight headings, airy light sections, round photo crops with a terracotta disc and pill buttons. Palette: marine #0B2545 (text, footer, CTA card), bleu #1D4E9E actions (dark #163C7A), terracotta #D9663F accents (soft #FBE9E2), cream #F8F5EF and sky #EAF1F8 section bands, plus a thin tricolore strip above the white header. Fonts: Plus Jakarta Sans 700/800 headings, Inter text. Logo (v3, 2026-10-15): blue gradient rounded square (#2F6FD6 → #163C7A) with a white house, a blue check inside and a terracotta notification dot (#F07A4F, "quote received"). Wordmark: "Devis" in bleu #1D4E9E and "Artisans" in marine #0B2545 (light blue #8DB4F0 / white on the dark footer), plus a "par Shmor.ai" pill. The same SVG is used in layout.html, the favicon and the shmor.ai card.
**Photo cards:** service, tip and trade cards use the site-specific `cards` block in `tools/blocks.js` (photo, round icon overlapping it, title, text, CTA). The photo comes from the item's `image` or, if none, the linked page's photo; services that share a trade page have their own photos. The homepage has a "Tous nos métiers" grid with all 30 trades. Hero: light sky band; above 980px the page photo is a 430px circle on the right (340px on inner pages); below that it moves under the text as a 220px circle. Home visual order is set with CSS `order` (hero → benefits → service cards and blocks → latest posts → rest). Checked at 320, 375, 768, 1024 and 1280 px on all 77 pages, with no horizontal scroll.
**Photos:** free-licence Unsplash images, credited, with French alt text. Region photos come from Unsplash searches of each region; alt texts describe only what is visible.

## Search routing on shmor.ai
French `keywords` in `shmor-site.json`, both accented and unaccented (électricien/electricien), because the master router does plain substring matching. Unaccented "renovation" is deliberately left out so English "home renovation" stays with TradesStation. Tested: "plombier paris", "devis toiture", "pompe à chaleur", "électricien lyon", "isolation des combles" → DevisArtisans; "plumber near me" → LocalPlumbers, "roofer quote" → TradesStation, "heat pump" → EnergySavers.

## Commands (run here)
```bash
node tools/build.js           # rebuild after ANY change to content/, templates/ or shmor-site.json
node tools/serve.js 4019      # preview http://localhost:4019  (preview config "devisartisans")
```
After changing `shmor-site.json`, also run `node tools/sync-network.js` in `../../shmor-ai`.

## Referral links (the money)
None yet. **Travaux.com** runs an affiliate programme ("Devenez affilié", travaux.com/blog/devenez-affilie): you sign up through the **Netslave** platform, it pays a commission per quote request (lead), and you can contact affiliate@instapro.com. Allowed: display, text links, email (with conditions). **Not allowed: cashback, promo codes, vouchers, keyword bidding (SEA), site-unders.** This site's organic SEO is fine, but never buy search ads on Travaux.com terms. Once the user has the tracking link:
1. Add it to `shmor-site.json` → `"links"`, e.g. `"travaux-com": { "merchant": "Travaux.com", "network": "direct", "url": "<exact link from the user>", "blurb": "Publiez votre projet gratuitement et recevez des devis" }`. Use `"direct"` unless the link runs through a network that has automatic sub-IDs.
2. Add `"partners": ["travaux-com"]` to the trade and region pages (the heading is already set: "Comparez les devis gratuits de nos partenaires"), and optionally `"fallback": "travaux-com"`.
3. Rebuild, sync the master, commit both repos.

## History & decisions
- 2026-10-15: the user asked for "another site like ProFinders, completely in French for the French market, genuine, using French regions and services as offered on Travaux.com". Brand **DevisArtisans** ("devis artisan" is a core French search term). The kit gained French support (`seo.locale: "fr"`) in the same change, and English sites build unchanged.
- 2026-10-15 (same day): the user asked for a lot more work: a redesign that looks more professionally French using cjaffiliates.com (= cj.com) as the design guide, at least 20 backdated blog posts, and many more service cards for Travaux.com's most popular services. Later the same day, the user asked for more blogs, cards, guides, tips and advice so the site looks busy and active before applying to Travaux.com: 20 more posts, 6 guides, the Astuces hub and trade tips were added (107 pages). Earlier: design v2, 15 more trades (30 in total), 53 service cards and 24 dated posts. The new kit icons were copied to every site.
- Honesty rules: footer and FAQs say DevisArtisans is an information and referral service that doesn't employ or vet artisans and may earn commissions. General information only, not legal or tax advice.

- 2026-10-15: French legal pages added (mentions légales, confidentialité, cookies) and the footer now links to them instead of shmor.ai's English pages; Contact → `/mentions-legales/#contact`, "Notre rémunération" → `/comment-ca-marche/`.

## Ideas / next
Travaux.com affiliate link · fill the legal-page placeholders once the user gives company details · consider self-hosting fonts (drops the Google Fonts IP transfer) · more trades from Travaux.com's activity list (VMC, volets roulants, portail, alarme/vidéosurveillance, désamiantage, dératisation, fosse septique, ascenseur/monte-escalier) · city pages (Paris, Marseille, Lyon, Toulouse…) only with genuinely local content · deepen blog posts towards 600–900 words · new posts on current topics (MaPrimeRénov’ when official barèmes are published).
