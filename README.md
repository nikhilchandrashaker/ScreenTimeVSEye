# Screens and Sight — Screen Time & Eye Health Project

An evidence-anchored look at how daily screen time relates to eye strain, myopia risk, and sleep — built entirely from named, cited studies rather than a scraped or synthetic dataset.

## What's in this project

| File | What it is |
|---|---|
| `screen_time_eye_model.html` | **The interactive model.** Open it in any browser. Move the hours slider (or click a preset) and see myopia risk, digital-eye-strain likelihood, blink/tear-film effects, and sleep notes update live — each one traced to a specific study. |
| `Screens_and_Sight_Research_Paper.docx` | A ~2,500-word research paper covering digital eye strain, the blinking/tear-film mechanism, the myopia dose-response evidence, blue light and sleep, at-risk populations, mitigations, and an explicit limitations section. Full reference list included. |
| `Screens_and_Sight_Slides.pptx` | A 13-slide deck version of the same material, built for presenting — charts, stat cards, and a sources slide. |
| `data/research_data.csv` | The raw compiled dataset: every number used anywhere in this project, with population, reported hours, the exact study, publication year, source type, and a URL. |
| `README.md` | This file. |

## Why there's no "real dataset" in the traditional sense

There is no public, individual-level dataset linking personal screen-time logs to personal eye outcomes — this isn't something anyone's simply sitting on. So instead of fabricating one, this project compiled **real, published, cited numbers** from peer-reviewed studies, meta-analyses, and reputable health organizations, and treated *that* as the dataset (`data/research_data.csv`). That's a legitimate and increasingly common way to build a model when no raw dataset exists: you make the evidence base itself the data, and you're transparent about it.

## How the interactive model actually works

**Myopia risk** is the most rigorous part of the tool. It's built on a real dose-response meta-analysis (Ha et al., *JAMA Network Open*, 2025 — 45 studies, 335,524 participants) that reported actual odds ratios at specific hour marks: 1.05× at 1 hour/day, 1.97× at 4 hours/day. The tool interpolates smoothly between the study's own data points (0–4 h/day, solid line on the chart) using a monotonic curve fit, and — only beyond 4 hours/day, where the meta-analysis itself doesn't report exact figures — extends the curve gently based on the study's qualitative description ("rises more gradually"). That extrapolated portion is dashed and explicitly labeled as illustrative, not a reported value.

**Digital eye strain likelihood** is *not* smoothed into one fake continuous curve, on purpose. The underlying studies use different populations (adolescents, university students, older adults, general U.S. adults) and different symptom definitions (self-report vs. the CVS-Q questionnaire), so forcing them into a single regression would imply more precision than the evidence supports. Instead, the tool shows the closest matching real study or studies for whatever hour range you select, cited by name.

**Blink rate and tear film** intentionally surfaces a tension in the literature: patient-education sites widely claim blink rate drops from ~15–20/min to ~5–7/min on screens, but the one controlled, hard-copy-matched lab study in this dataset (Portello, Rosenfield & Chu, 2013) found blink rate barely changed — the real, statistically significant finding was a rise in *incomplete* blinks (7.0% vs. 4.3%), which is arguably the more precise mechanism for screen-related dryness.

**Sleep/circadian** is deliberately *not* hours-based like the others — melatonin suppression from blue light depends much more on timing (how close to bedtime) than on cumulative daily hours, so the tool treats it as a separate note rather than forcing it onto the same x-axis.

## Limitations, stated plainly

- Most of the digital-eye-strain studies are cross-sectional and self-reported.
- Definitions of "digital eye strain" vary between studies (self-report vs. CVS-Q ≥6, etc.) — the numbers aren't strictly apples-to-apples.
- Association is not causation, including for the myopia odds ratios — screen time correlates with other near-work and reduced outdoor time, which are themselves independently linked to myopia.
- The model is a research-informed estimator for a general population, not a personal medical prediction. It shouldn't replace an eye exam or a clinician's advice.

Full source-by-source detail on all of this is in Section 8 of the research paper.

## Sources at a glance

Core sources include: Ha et al., *JAMA Network Open* (2025, myopia dose-response meta-analysis); Portello, Rosenfield & Chu, *Optometry and Vision Science* (2013, blink patterns); peer-reviewed cross-sectional studies on digital eye strain in adolescents (India), university students (Saudi Arabia), nursing students (Peru), and older adults; a Cambridge-affiliated meta-analysis on outdoor time and myopia; a Harvard Health summary of blue-light/melatonin research; and industry/professional-association reports (AOA, CooperVision, Vision Center) for population-level screen-time statistics. Every individual figure, with its full citation and URL, is in `data/research_data.csv` and in the References section of the research paper.

## Opening the files

- **Interactive model:** double-click `screen_time_eye_model.html`, or drag it into any browser. No install, no server, no internet connection needed — everything is self-contained in the one file.
- **Paper / slides:** open with Word / PowerPoint (or Google Docs / Slides, or LibreOffice).
- **Data:** open `research_data.csv` in Excel, Sheets, or pandas (`pd.read_csv("data/research_data.csv")`).
