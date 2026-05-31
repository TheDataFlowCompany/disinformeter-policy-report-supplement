# DisInforMeter — Online Supplement to Policy Report D5.3

**Online supplemental material for [DE-CONSPIRATOR](https://cordis.europa.eu/project/id/101132671) deliverable D5.3, the *DisInforMeter Policy Report*.**

🌐 **Live site:** <https://thedataflowcompany.github.io/disinformeter-policy-report-supplement/>

This repository hosts the **rendered, public static website** that accompanies the
printed D5.3 policy report. The report introduces the **DisInforMeter** — a
validated population indicator for receptivity to, and detection of, Foreign
Information Manipulation and Interference (FIMI), built across five studies and
more than 10,000 respondents. The report is kept short for a policy audience; this
supplement carries everything that does not fit it.

> **Dissemination level:** PU (Public) · **Grant Agreement:** 101132671 ·
> **Work package:** WP5

---

## What the supplement provides

The supplement serves two aims the printed report cannot:

1. **Reproducible annotated code.** Every figure and table is shown together with
   the *actual* R script that produced it (read live from the source repository,
   so the displayed code can never drift from what ran), plus the full data
   lineage and downloadable aggregate tables. A reader can rebuild every number.
2. **In-depth detail.** The complete measured item bank with full English wording,
   the recommended short module to field in future data-collection waves,
   in-detail profiles for all 13 multinational-wave countries, the full
   nomological network, and complete reliability, measurement-invariance, and
   external-validation diagnostics — with machine-readable downloads throughout.

### Site map

| Page | Contents |
|---|---|
| [Home](https://thedataflowcompany.github.io/disinformeter-policy-report-supplement/) (`index.html`) | Framing, scoring direction, boundary of interpretation, how to cite, data & code availability. |
| **How to read this** (`07-overview.html`) | Crosswalk between the report and the supplement, plus a complete figure/table index. |
| **Constructs, full items & short form** (`07b-construct-reference.html`) | Construct architecture, the **full measured item bank** (every item, full wording, per wave), the **recommended 27-item short module** for future waves, the construct reference card, and the language matrix. |
| **Study chain & measurement quality** (`07g-schematics.html`) | Five-study chain, sample composition, reliability/AVE, measurement-invariance ladders, FIMI-variant diagnostics. |
| **FIMI detection across Europe** (`07c-headline-maps.html`) | Detection choropleths, source-origin maps, the Russian−Chinese asymmetry, and the country × item heatmap. |
| **Receptivity profiles** (`07d-construct-profiles.html`) | Overall receptivity composite and the five-domain affective profiles (radars and maps). |
| **Predictors, anchors & networks** (`07e-predictors-and-anchors.html`) | Predictor → detection paths by FIMI variant, civic anchors, S5 external validation, and the full nomological network. |
| **In-detail country profiles** (`07f-country-snapshots.html`) | A data-driven diagnostic profile for **each of the 13 countries**. |
| **Data pipeline & aggregates** (`07a-aggregates-and-geometries.html`) | The reproducible derivation of every country-level aggregate, with previews and downloads. |
| **Annex tables & downloads** (`07h-annex-tables.html`) | Consolidated annex reference, glossary, and a complete CSV/PDF download index. |
| **Reproducibility & methods** (`07i-reproducibility.html`) | Full rebuild sequence, analysis conventions, limitations, and the data-availability statement. |

---

## How to read the findings

The single most important convention is **which side of the instrument a figure
plots**, because the two run in opposite directions:

- **FIMI detection** (the criterion). Respondents rate confirmed FIMI headlines
  from *1 = certainly not manipulated* to *7 = certainly manipulated*.
  **Higher = better detection.** Lower = a detection blind spot.
- **DisInforMeter domains** (Threat, Betrayal/Abandonment, Fear/Pragmatism,
  Foreign-Power Admiration, General). **Higher = more receptivity-relevant
  endorsement.** These are *not* detection scores.

The two must never be collapsed into a single "vulnerability" number.

### Boundary of interpretation

The DisInforMeter is a **population-monitoring and survey-research instrument**. It
is **not** an individual risk-profiling tool, a content-moderation tool, or a
stand-alone basis for enforcement. Country results are evidence for policy
prioritisation and follow-up analysis — **not** country verdicts, and never a
basis for individual-level targeting. Cross-national comparisons are strongest as
profiles, ranks, and associations; absolute latent-mean comparisons carry a
scalar-invariance caveat.

If any figure from this site is reused, it should carry three statements:
(1) FIMI figures show *detection of confirmed FIMI cases*, where higher means
better detection; (2) DisInforMeter domain scores show *receptivity-relevant
endorsement*, where higher means more endorsement; (3) country comparisons are
population-level signals and do not license individual profiling.

---

## How this site is built and published

This repository contains the **rendered output only**. The site is authored as a
[Quarto](https://quarto.org) website whose **source lives in the DisInforMeter
scale-development repository** under `full-annotated-code/07-policy-report/`, and
is rendered here as a sibling output directory:

```bash
# From the scale-development repository root:
quarto render full-annotated-code/07-policy-report
# → writes the static site into this repository (../disinformeter-policy-report-supplement/)
```

The render is intentionally light — it embeds committed, print-ready artefacts
(figures, tables, aggregate CSVs) and shows each producing script as folded,
non-executed code; it does **not** re-fit the underlying SEM / multilevel-Bayesian
models. To rebuild those artefacts from scratch (in the source repository):

```bash
Rscript -e 'renv::restore()'                 # 1. exact package environment
Rscript R/policy_report/00_run_all.R         # 2. country-level aggregates → CSV
for f in scripts/policy_report/F-*.R scripts/policy_report/A-*.R scripts/policy_report/T-*.R; do
  Rscript "$f"                               # 3. print-ready figures + tables
done
quarto render full-annotated-code/07-policy-report   # 4. render this site
```

> ⚠️ **Do not edit the `.html` files in this repository by hand** — they are
> regenerated on every render and changes will be overwritten. Edit the Quarto
> sources in the scale-development repository instead.

### Hosting

The site is served via **GitHub Pages** from the `main` branch root. Static-site
output from Quarto should not be processed by Jekyll, so this repository includes a
`.nojekyll` file. To use a custom domain, add a `CNAME` file (and update
`site-url` in the source project's `_quarto.yml`).

### Viewing locally

Because the site uses relative asset paths, open it through a local web server
rather than `file://`:

```bash
python3 -m http.server 8000   # then open http://localhost:8000
```

---

## Repository contents

```
.
├── index.html                       # landing page
├── 07-overview.html … 07i-…html     # the ten content pages
├── figures/                         # print-ready figures (PNG + vector PDF)
├── tables_raw/                      # machine-readable aggregate data (CSV)
├── assets/, styles.css, site_libs/  # site styling and dependencies
├── search.json, sitemap.xml, robots.txt
└── README.md
```

---

## Studies behind the supplement

| Study | Country / fielding | N | Role |
|---|---|---|---|
| S1 | Lithuania, Dec 2024 | 681 | Item-pool generation and scale construction |
| S2 | Lithuania, Mar 2025 | 582 | Model refinement; first full 8-item FIMI battery |
| S3 | Germany, May 2025 | 782 | Cross-national replication |
| S4 | 13 countries, Dec 2025 | 8,040 fielded; 7,783 in the report cut | Multinational deployment, country profiles, source variants, invariance |
| S5 | Lithuania, Mar–Apr 2026 | 248 | External validation against preregistered anchors |

The 13 in-scope S4 countries are Austria, Belgium, Bulgaria, Estonia, France,
Germany, Hungary, Italy, Latvia, Lithuania, Poland, Serbia, and Turkey.

---

## How to cite

> Baršytė, J., Kaminskienė, Ž., Kreienkamp, J., & Zakarevičiūtė, A. (2026).
> *DisInforMeter Policy Report (Deliverable D5.3) — Online Supplemental Material.*
> DE-CONSPIRATOR Consortium. EU Horizon Europe Grant Agreement No. 101132671.
> <https://thedataflowcompany.github.io/disinformeter-policy-report-supplement/>

---

## Data and code availability

- **Annotated analysis code** is shown inline throughout the site and lives in the
  scale-development repository (`R/policy_report/`, `scripts/policy_report/`).
- **Aggregate data** for every country-level table is downloadable as CSV from the
  [Annex tables & downloads](https://thedataflowcompany.github.io/disinformeter-policy-report-supplement/07h-annex-tables.html)
  page (and from `tables_raw/` in this repository).
- **Participant-level data** will be released where consent, anonymisation, and
  data-protection conditions permit, under an open reuse licence, as a DOI-stamped
  archive.

---

## Authors and contact

Produced by **AdCogito** for the DE-CONSPIRATOR consortium:

- Justina Baršytė
- Živilė Kaminskienė
- Jannis Kreienkamp — <jannis@thedataflowcompany.com>
- Agnė Zakarevičiūtė

*This deliverable is dedicated to the memory of Justina Baršytė, a dear friend and
a valued colleague, whose inspiration and vision made this work possible.*

---

## License

Unless otherwise stated, the content of this supplement (text, figures, and
aggregate tables) is released under a
[Creative Commons Attribution 4.0 International (CC-BY 4.0)](https://creativecommons.org/licenses/by/4.0/)
licence. When reusing material, please cite as above and retain the
interpretation caveats.

---

<sub>Funded by the European Union (Grant Agreement No. 101132671). Views and
opinions expressed are those of the authors only and do not necessarily reflect
those of the European Union. Neither the European Union nor the granting authority
can be held responsible for them.</sub>
