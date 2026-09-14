# The Hidden Cost of Free Browsing
**An independent audit of privacy policies versus observed behaviour across the 100 most-visited websites in Europe.**
Weronika Nitecka and Dr. Estera Kot - September 2026

---

## What this is

European data-protection law assumes that people are **informed** (by the privacy policy) and on that basis **consent** (through the cookie banner). This study tested that assumption against evidence: we measured what each of the 100 most-visited European websites actually does on arrival, and independently scored each site's written privacy policy against the seven data-protection principles of GDPR Article 5.

**The two are unrelated.** Policy quality shows no meaningful correlation with third-party tracking (r = 0.05), cookies set before consent (r = 0.04), or whether a site offers any means of refusal (r = −0.14). Meanwhile 94% of measured sites set cookies before the visitor interacts with anything, 71% offer no first-layer way to reject, and reading all 77 unique policies once would take about 35 hours.

> A well-written privacy policy is not evidence of privacy-respecting behaviour. It is evidence of a well-written privacy policy.

**[Read the full report](report/hidden-cost-of-free-browsing.pdf)**

This repository contains the observations, the derived data behind every figure, the full appendices, and a pointer to the open-source crawler that produced them. 

---

## Contents

| Path | What it is |
|---|---|
| `report/` | The report as published (PDF) |
| `data/results.json` | **Raw crawl observations** — one record per site, exactly as measured on 19–21 July 2026. This is the evidentiary record; because it observes a live web, it cannot be regenerated identically. |
| `data/report-data.json` | Derived aggregates: distributions, per-principle scores, concentration, correlations. Every figure in the report is computed from this. |
| `data/gdpr-scores.json` | The human-reviewed GDPR principle scores, keyed by registrable domain. |
| `appendices/appendix-A-full-site-table.csv` | Every measured site with its trackers, policy length, CMP, cookies-before-consent, and reviewed score. |
| `appendices/appendix-C-failed-sites.csv` | The 17 sites that produced measurement errors. |
| `appendices/charts/` | The four report figures (PNG) and their underlying data (CSV). |

---

## Methodology in brief

Each site was assessed **twice, independently**:

- **Measured** — an instrumented Chromium browser (Playwright) loaded each homepage from a clean profile and recorded third-party domains, cookies set before consent, the consent-management platform present, TCF/GPP interfaces, whether a first-layer "reject all" existed, and permission prompts. The linked policy was fetched, extracted, word-counted, and hashed.
- **Reviewed** — each policy was scored 0–10 against each of the seven GDPR Article 5(1) principles using a structured rubric applied with large-language-model assistance under author review.

Full method, limitations, and the scoring rubric are in the report (§2 and Appendix B). The measured figures are reproducible from the crawler; the reviewed scores are expert-guided judgement and are labelled as such throughout.

**Provenance:** crawl window 19–21 July 2026 / Chromium 149.0.7827.55 / Playwright 1.61.1.

---

## Reproducing the measurement

The crawler is open source and lives in the Guardatum extension repository:

**→ [github.com/guardatum/guardatum](https://github.com/guardatum/guardatum)** — see `packages/analyser/`

```bash
git clone https://github.com/guardatum/guardatum
cd guardatum/packages/analyser
npm install
npx playwright install chromium
npm run crawl        # re-measures the live web (results will differ as sites change)
npm run aggregate    # regenerates report-data.json
```

Because the web changes, a fresh crawl will not reproduce `results.json` byte-for-byte — that file is the record of what was observed in July 2026. The *method* reproduces; the *observations* are a point-in-time snapshot, which is why they are version-controlled here.

---

## Citing this work

> Nitecka, W., & Kot, E. (2026). *The Hidden Cost of Free Browsing* Guardatum.

---

## Licence

- **Report, data, and appendices:** [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/) — use freely with attribution.
- **Crawler and analysis code** (in the linked repository): AGPL-3.0.
