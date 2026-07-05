# Institutional Voice in LLM-Generated News

Code for **"From Style to Cultural Calibration: Evaluating Institutional Voice in LLM-Generated News."**
We use NYT China coverage (2020-2024) as a calibrated case and test whether LLMs reproduce a newsroom's
desk-level entity and affective patterns, via a **reproduction / recovery / miscalibration** diagnostic.
Models: GPT-4o-mini, Gemini-2.5-Flash, Claude-Haiku-4.5. n = 40 headlines/desk.

> ✏️ **Before publishing, fill in the placeholders:** author name in `LICENSE`, and author/venue in the citation below.

## Layout
```
notebooks/   01 data prep · 02 GPT · 03 Gemini · 04 Claude · 05 figures · 06 qualitative · vader_check
data/processed/   lexicons, sample manifest, NYT sentiment/entity scores  (NO NYT article text)
data/generations/ LLM-generated article text (model outputs)
data/results/     scores, cross-model tables, robustness CSVs, figures/
POSTER_CONTENT.md poster copy + key numbers
```

## Run
```bash
pip install -r requirements.txt
# generation notebooks need API keys in your environment:
export OPENAI_API_KEY="sk-..."         # notebooks 02, 06
export GOOGLE_API_KEY="AIza..."        # notebook 03
export ANTHROPIC_API_KEY="sk-ant-..."  # notebook 04
# run notebooks from inside notebooks/ (paths are relative: ROOT = Path(".."))
```
DistilBERT-SST2 downloads automatically. The released scores + generations reproduce all figures
(run `05_figures.ipynb`) without any API calls.

## Data note
**NYT article full text is NOT redistributed** (copyright). `data/raw/` and any `full_text` columns are
git-ignored. Notebook 01 rebuilds the sample from the NYT corpus (obtain via the NYT Article Search API);
everything downstream runs from the derived scores and generations included here.

## Keys
Never hardcode API keys. All notebooks read them from the environment. If you fork/commit, keep them out.

## Citation
```bibtex
@inproceedings{institutional_voice_llm_2026,
  title     = {From Style to Cultural Calibration: Evaluating Institutional Voice in LLM-Generated News},
  author    = {<Author Name(s)>},
  booktitle = {<ICML 2026 Workshop name>},
  year      = {2026}
}
```

## License
Code released under the [MIT License](LICENSE). NYT article content is not included and is not covered by
this license.
