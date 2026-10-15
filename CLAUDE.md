# DevisArtisans (devisartisans.shmor.ai)

A Shmor marketplace (shared rules in `../../CLAUDE.md`): its own brand, design and SEO. **The network's first French-language site, for the French market.** It helps homeowners in mainland France find an artisan (plombier, électricien, couvreur…) and compare free quotes, then refers them to quote platforms for a lead commission. Modelled on ProFinders (`../shmor-profinders/`), with trades and regions taken from **Travaux.com** (Instapro group), the main referral target. Repo: `Shmorai/shmor-devisartisans` (private until launch). Status: **building**, no referral links yet.

## Language
- **Everything is in French**, including meta, breadcrumbs ("Accueil"), FAQs, 404 and search. `shmor-site.json` → `seo.locale: "fr"` switches the site kit's built-in French word pack (kit `tools/build.js` → `WORDS.fr`; any word can be overridden with `seo.strings`). `ogLocale: "fr_FR"`, `<html lang="fr">`.
- Write in French with "vous", French typography (no-break space before `: ? !`, « guillemets », ’ apostrophes) and French terms (devis, SIRET, décennale, RGE, MaPrimeRénov’). The US/UK/EU wording rule in `../../CLAUDE.md` does not apply here.
- Footer legal links point to shmor.ai's English pages. Before launch, consider French "Mentions légales" / "Politique de confidentialité" pages (French law requires mentions légales: publisher identity, host).

## Where things are
| What | Where |
|---|---|
| Card on shmor.ai, search keywords, **referral links**, offers, SEO defaults | `shmor-site.json` |
| Pages (1 JSON file = 1 Google landing page) | `content/` (`home.json` = homepage) |
| Design: header, logo, footer (footer lists are **hand-written**) | `templates/layout.html` |
| Design: styles | `assets/site.css` (kit defaults at the top; **DevisArtisans theme** block at the bottom) |
| Generated output (don't edit by hand) | `index.html`, `*/index.html`, `sitemap.xml`, `robots.txt`, `404.html`, `search/`, `search-index.json` |

## Pages (77)
- Home · `comment-ca-marche` · `metiers` hub · `regions` hub · `guides` hub · `blog` index.
- **30 trades** `metiers/<slug>` (the most-requested categories on Travaux.com): plombier, electricien, couvreur, peintre, macon, chauffagiste, pompe-a-chaleur, climatisation, menuisier, carreleur, plaquiste, jardinier-paysagiste, serrurier, renovation, isolation, charpentier, facadier, cuisiniste, salle-de-bain, pisciniste, vitrier, terrassier, ramoneur, nettoyage, demenageur, diagnostiqueur, panneaux-solaires, poele-a-bois, parquet, veranda. Each covers: ce que fait…, quand faire appel…, questions à poser, ce qui fait varier le prix, règles et précautions, plus FAQs.
- **Service cards**: 53 popular "prestations" (from Travaux.com's activity list) as icon cards (`deals` blocks with class `svc`), grouped into 8 categories on the `metiers` hub. The 16 most requested are also on the homepage. Each card links to its trade page.
- **13 regions** `regions/<slug>`: every region of mainland France, Corsica included (Travaux.com covers mainland France; no DROM). Each lists its departments with numbers and its main cities, then covers local building styles and materials, natural risks (linked to Géorisques), France Rénov’/ADIL advice and a region-specific FAQ.
- **4 guides** `guides/<slug>`: verifier-un-artisan, devis-travaux, garanties-travaux, aides-renovation.
- **Blog**: 24 posts `blog/<slug>` (about 280–500 words each, with sources), dated every 9–10 days from 2026-03-03 to 2026-10-10 at the user's request ("backdated"). Content is evergreen, so the facts don't depend on the date shown. Homepage shows the 3 latest. RSS at `/blog/feed.xml`.
- Top menu: Métiers, Régions, Guides, Blog, Comment ça marche + "Demander un devis" pill (written in `layout.html`, links to /metiers/ until a referral link exists).
- **French typography**: content strings use a no-break space before `? ! : ;` and inside « ». Keep doing this when editing content, or the "?" can wrap onto its own line.

## Facts and sources (keep content genuine)
Checked 2026-10-15: devis obligatoire avant dépannage/réparation/entretien (arrêté du 24 janvier 2017, in force since 1 April 2017, 150 € threshold removed); décennale (service-public.gouv.fr F2034: insurance before the site opens, certificate attached to devis and factures); parfait achèvement 1 an / biennale 2 ans / décennale 10 ans (Code civil 1792-6, 1792-3, 1792); TVA 5,5 % rénovation énergétique / 10 % amélioration (logement > 2 ans); démarchage téléphonique rénovation énergétique interdit depuis 2020; entretien chaudière annuel (4–400 kW), PAC tous les 2 ans (4–70 kW); Consuel; IRVE > 3,7 kW; A2P; art. 671 Code civil.
**MaPrimeRénov’ amounts are deliberately not quoted** because sources disagreed for 2026. Pages describe the schemes and link to france-renov.gouv.fr. No prices, review counts or artisan numbers anywhere.

## Design (v2, 2026-10-15: "professionnel français", modelled on cj.com's layout)
The user asked for a more professional French look using CJ Affiliate (cj.com) as the guide. It now has very large tight headings, airy light sections, round photo crops with a terracotta disc and pill buttons. Palette: marine #0B2545 (text, footer, CTA card), bleu #1D4E9E actions (dark #163C7A), terracotta #D9663F accents (soft #FBE9E2), cream #F8F5EF and sky #EAF1F8 section bands, plus a thin tricolore strip above the white header. Fonts: Plus Jakarta Sans 700/800 headings, Inter text. Logo: marine rounded square with a terracotta roof chevron and an ochre check, plus "Devis**Artisans**" and a "par Shmor.ai" pill. Hero: light sky band; above 980px the page photo is a 430px circle on the right (340px on inner pages); below that it moves under the text as a 220px circle. Home visual order is set with CSS `order` (hero → benefits → service cards and blocks → latest posts → rest). Checked at 320, 375, 768, 1024 and 1280 px on all 77 pages, with no horizontal scroll.
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
- 2026-10-15 (same day): the user asked for a lot more work: a redesign that looks more professionally French using cjaffiliates.com (= cj.com) as the design guide, at least 20 backdated blog posts, and many more service cards for Travaux.com's most popular services. Result: design v2, 15 more trades (30 in total), 53 service cards and 24 dated posts. The new kit icons were copied to every site.
- Honesty rules: footer and FAQs say DevisArtisans is an information and referral service that doesn't employ or vet artisans and may earn commissions. General information only, not legal or tax advice.

## Ideas / next
Travaux.com affiliate link · French legal pages (mentions légales, confidentialité, cookies with CNIL-compliant consent) · more trades from Travaux.com's activity list (VMC, volets roulants, portail, alarme/vidéosurveillance, désamiantage, dératisation, fosse septique, ascenseur/monte-escalier) · city pages (Paris, Marseille, Lyon, Toulouse…) only with genuinely local content · deepen blog posts towards 600–900 words · new posts on current topics (MaPrimeRénov’ when official barèmes are published).
