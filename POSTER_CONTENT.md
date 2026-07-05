# Poster Content Pack
**From Style to Cultural Calibration: Evaluating Institutional Voice in LLM-Generated News**

All numbers are the current results: **n = 40 headlines/desk (80 total)**, three model families
(**GPT-4o-mini, Gemini-2.5-Flash, Claude-Haiku-4.5**), prompts **V.A** (default NYT-staff instruction) and
**V.E** (strongest: desk-specific frame + anti-brochure constraints), 3 reps, temperature 0.7. Affective
register = chunked DistilBERT-SST2 in [−1, +1], paired Wilcoxon within headline. Figures in
`data/results/figures/*.pdf`.

> **Put on poster (small print near title):** *Results expanded from the paper's pilot
> (n = 10 → 40 headlines/desk; 2 → 3 model families).* Poster numbers supersede the paper's;
> if someone quotes the paper's §4.5 over-correction result (Gemini 3, V.E), the answer is FIG 1b:
> prompt effects are model-version-specific.

---

## BANNER (top of poster, one line)
> LLMs reproduce a newsroom's **who & what** for free and can be **prompted** to its Business tone — but its
> **Foreign-desk affect resists prompting**, across GPT, Gemini, and Claude. They imitate the **form** of
> institutional voice and skip its **substance**; form is prompt-movable, substance is not.

---

## 1 · The question
LLMs increasingly write in institutionally recognizable registers (press releases, legal summaries, "in the
style of the NYT"). We ask whether they reproduce not just *journalistic style* but **institutional voice** —
which actors a newsroom attends to, and what **affective register** it deploys per desk.

**Calibrated case — NYT China coverage, 2020–2024.** A 5,396-article corpus shows a counterintuitive
desk asymmetry: **Business coverage is *more negative* than Foreign** (it routes China through corporate risk,
supply chains, systemic exposure). A model that has the NYT's voice should reproduce that asymmetry, not just
sound "NYT-ish."

## 2 · Method  *(small box)*
80 headlines (40 Business / 40 Foreign; event-window–excluded, seed-controlled). Each → 3 models × {V.A, V.E}
× 3 reps. Two axes: **entity/topic** (data-driven log-odds lexicon) and **affect** (DistilBERT-SST2).
Triangulated with **VADER**, **reported-detail counts**, and a manual audit.

## 3 · The framework  →  **FIG 0**  *(concept anchor)*
Institutional voice decomposes into three layers by sensitivity to prompting:
**Reproduced** (spontaneous) → **Recoverable** (via prompt scaffolding) → **Miscalibrated** (survives prompting).

---

## 4 · Main result  →  **FIG 1c (dumbbell — THE money figure)**
**All three models are more positive than NYT, and always more so on Foreign than Business.**

**Reproduced — entity/topic vocabulary.** All 3 models, both prompts: positive desk fidelity.
Business ≈ NYT (models **+8.4–11.3** vs NYT **+8.5**); Foreign positive (**+6.5–7.3** vs NYT +8.9). Holds under
default V.A — no prompting needed. *(3-model numbers: `results_axis1_crossmodel3.csv`.)*

**Recoverable — Business-desk affect.** Affective center vs NYT's −0.64:
GPT +0.26/+0.06 ▸ Gemini −0.04/−0.14 ▸ **Claude −0.27/−0.47 (closest to NYT)**.
Under V.E the Business tone is recovered: **Claude V.E Business = NYT (dev +0.08, p = 0.23, n.s.)**;
direction-consistent under VADER. *(Don't lead with VADER p-values: VADER is a direction-only check —
by its p-values several other cells also go n.s., so quoting p = 0.85 invites a cherry-picking question.)*

**Miscalibrated — Foreign-desk affect.** Foreign stays significantly more positive than NYT in all 3 families
even under the strongest prompt. **Foreign > Business in all 6 model×prompt cells; all 12 cells positive.**
Per-headline deviation (paired Wilcoxon):
- GPT: A Biz +0.77 / For +1.04 ; E Biz +0.56 / For +0.84  (all p < 0.001)
- Gemini-2.5: A Biz +0.50 / For +0.69 ; E Biz +0.42 / For +0.59  (all p < 0.001)
- Claude: A Biz +0.27 / For +0.47 ; E **Biz +0.08 (n.s.)** / For +0.25 (p = 0.01)

**Also: the paradox's *direction* is reproduced, its *calibration* is not.** Every model keeps NYT's
counterintuitive ordering (Business more negative than Foreign) but over-widens the gap up to 4× (models
−0.26…−0.38 vs NYT −0.09) and shifts the whole baseline positive. Models "know" the desk relationship; they
mis-set the zero point and the scale.

## 5 · Calibration is model-version-specific  →  **FIG 1b**
On the *same* 20 headlines, **gemini-3-flash-preview** is near-calibrated on Business (dev **+0.11**, n.s.)
while **gemini-2.5-flash** drifts to **+0.40**. Magnitude depends on the model version; **the Foreign
bottleneck is robust in both.**

---

## 6 · Form vs substance: what "sounding like NYT" hides  →  **FIG 4 + FIG 5**  *(unifying, high-impact)*
> **Header for this panel:** *Models imitate the form of institutional voice and skip its substance — and
> prompting can move the form, not the substance.*

**FIG 4 — Substance is thinned out.** Generated articles keep the topic and a plausible register but carry far
less *reported particularity* than NYT (% of NYT, all 3 models):
**numbers/stats 39–55%**, named entities 54–68%, direct quotes 76–93% — in **longer sentences (114–123%)**.
Flattening = **loss of reported detail, not loss of fluency.** (Manual audit agrees: abstract-over-concrete
18/20; omitted particulars 17/20; generic sources 15/20; softened critical edge 13/20.)

**FIG 5 — The form is *over*-produced.** All three models over-use the *same* abstract analytical register vs
real NYT: **"underscores" 29×**, navigate 26×, implications 24×, commitment 23× — plus **generic attribution**
(**"spokesperson" 20×, "observers" 18×**) where NYT names specific sources. The register is what fills the hole
left by the missing reporting: lacking specific facts, the model defaults to genre-plausible abstraction.

**Why this is a *finding*, not just description (the "so what"):**
1. **Form and substance are dissociable and quantifiable.** Models pass "does it sound like the NYT?" while
   delivering < half its reportorial density. Fluency ≠ institutional voice.
2. **The abstraction is a *substitute* for grounding.** Under-grounded generation doesn't leave gaps — it fills
   them with confident analysis ("this underscores the complexities…"). The 29× "underscores" is the fingerprint.
3. **You can prompt a register/tone, but not particularity.** Affect is partly prompt-recoverable (Business);
   the analytical register + detail deficit survives even the anti-brochure prompts (V.D/V.E) — you cannot prompt
   facts the model does not have. This is the deepest, least-recoverable layer.
4. **Not a mechanism for the affect result** — we checked: reported-detail does *not* predict tone
   (numbers r ≈ 0; entities +0.14 in generated, +0.30 in NYT — identical direction in both). So affect
   miscalibration and substance thinning are **two independent deficits**, not one — which is exactly why the
   picture is "form imitated, substance skipped" rather than a single failure.

## 7 · Robustness  *(small box)*
- **VADER cross-check (direction-only):** direction agrees **16/16 cells (100%)**; per-headline correlation
  with DistilBERT **mean r = 0.29 (all p < 0.05)**; consistent with the Claude V.E Business recovery.
- **Balanced design:** adversarial/soft ≈ 50/50 per desk; within-topic-class check (GPT, all prompts):
  the Foreign>Business asymmetry holds in *both* classes → a desk effect, not a topic-charge artifact.
- **Triangulation as method:** DistilBERT + VADER + entity lexicon + reported-detail counts + manual audit all
  converge → robust to "it's just one sentiment classifier."

---

## TAKEAWAY  *(bottom banner)*
**Reproduction → Recovery → Miscalibration** is a portable diagnostic for cultural AI. Across three model
families, the **Foreign desk is the consistently resistant layer**: prompting recovers *codifiable*
(vocabulary-based) negativity but not the *situated*, framing-based negativity of foreign-affairs reporting.
The root is one thing: models perform **style transfer without the underlying reporting** — they imitate the
form of institutional voice (even over-signaling "analysis") and skip its substance (concrete particularity and
situated affect). **Form is prompt-movable; substance is not.** Calibrating institution-specific voice likely
needs grounding / fine-tuning / human review, not better prompts.

---

## KEY NUMBERS CHEAT-SHEET  *(print these)*
- Affective center vs NYT (−0.64): GPT +0.26/+0.06 · Gemini −0.04/−0.14 · Claude −0.27/−0.47
- Foreign > Business deviation in **6/6** model×prompt cells; **12/12** cells positive vs NYT
- Recovery: Claude V.E Business **p = 0.23 (DistilBERT, n.s. = calibrated)** — recovered; Foreign never
  recovered on the primary metric (all 6 Foreign cells significant, max p = 0.010)
- Reported detail vs NYT: **numbers 39–55%**, entities 54–68%, quotes 76–93%; sentences 114–123%
- Shared register: **"underscores" 29× NYT**, "spokesperson"/"observers" ~18–20×
- VADER robustness: **16/16 direction**, headline **r = 0.29**
- Entity fidelity reproduced (both desks positive); Foreign also lower than NYT → Foreign harder at every layer

## FIGURE → POSTER SLOT
| Figure | Slot | Role |
|---|---|---|
| **fig0_framework** | top-center | the thesis (concept) |
| **fig1c_desk_asymmetry** | center, largest | the whole result in one image |
| **fig4_reported_detail** | form/substance panel | substance thinned (fig4+fig5 = one panel) |
| **fig5_shared_register** | form/substance panel | form over-produced |
| **fig1b_gemini_model_sensitivity** | side | model-version sensitivity |
| fig3 (GPT lexical), fig1 (forest), fig2 (scatter) | backup / paper | too detailed for a poster |

*Use the .pdf (vector, 300 dpi). To (re)generate: Restart & Run All `05_figures.ipynb` (reads CSVs; no API).*
