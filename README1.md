# \# Autos\_In\_Authenticity\_Data

###### Partial judging data from MASK trials. Since the dataset involves public figures AND benchmark evals, not all is here. Readme (by Claude Opus 5.5) explains what is and isn't: 

# 

# Putting the *Autos* Back in Authenticity: Self-Identification, Not First-Person Grammar, Reduces Lying Under Pressure in LLMs

Code, judging rubrics, labels and figures for an Apart Research AI × Epistemics sprint project (Nov 13–15, 2026).

**Question:** does the voice a model is told to write in change whether it lies under pressure?

**Setup:**

* Seven models, 181 MASK prompts, and seven style conditions appended to the system prompt.
* The conditions: baseline; plain first person; "speak as yourself, the AI model"; hyperactive (impersonal); Anglo-Saxon; Latinate; and a formatting control.

**Headline result:** telling a model to speak *as itself* lowers lying. Pooled over seven models, it's 11.1 points below plain first-person "I" statements (p = 1e-19), and 7.3 points below baseline.

## Contents

|folder|what's in it|
|-|-|
|`code/`|Generation (`pilot\_generate.py`), style-feature counters (`features.py`, `etym.py`), blind judging tools (`judge\_tools.py`), analysis and figures|
|`rubric/`|The judging rubric used for every model, and the human adjudication rules used for Claude Haiku 5.5|
|`results/`|The all-model tables (rates and paired tests), the Haiku adjudication appendix, and the figure index|
|`labels/`|Per-response labels (honest / lie / evade / no\_belief / unclear), keyed by MASK `prompt\_id` and condition|
|`figures/`|All figures as PNG and SVG, with the CSV of numbers behind each|

## What is *not* here, and why

* **MASK prompt text.** MASK (`cais/MASK` on Hugging Face) is gated: you accept its conditions to download it, and it carries a canary string meant to keep it out of training data. Labels here reference prompt IDs only. Get the dataset from Hugging Face to reproduce the work.
* **Raw model outputs and judge notes.** Under pressure, several models fabricated damaging claims about real, named people. The raw outputs and the free-text judge notes are withheld for that reason.
* **Smaller trims, for the same two reasons:**

  * The label files keep only `prompt\_id`, `split`, `condition`, `label`, `misleading` and `empty`. The judges' free-text notes are removed.
  * In `labels/haiku\_adjudication\_log.csv`, the reasons written by AI adjudicators are blanked and the short quoted phrases from Haiku's responses are removed. AJ's own reasons are kept, so the human rulings stay auditable.
  * The internal judge-sheet item numbers are removed; rows are keyed by MASK `prompt\_id` and condition.
  * Also withheld: the blind judge sheets, spot-check and disagreement files, per-prompt transcripts, the Excel workbook and the adjudication worksheets. All of them reproduce response text, prompt text, or both.
* **Kept on purpose:** the rubrics quote one short fragment of a MASK proposition as a worked example, and the Haiku adjudication rules name a few scenario topics (a celebrity endorsement, a rideshare company, an NFL bounty case) to show how each rule applies. No full prompts or responses are included.
* **Researchers with MASK access** can rebuild the full picture: download `cais/MASK`, take the 20% sample per split with seed 42 (`code/pilot\_generate.py --fraction 0.2`), and join the labels on `prompt\_id`.

## Judging

* **Six of the models:** blind Claude Opus helper agents (condition and style instruction hidden), using `rubric/judging\_rubric.md`.
* **Claude Haiku 5.5:** Gemini was the primary judge, to avoid same-family judging. Claude labels served as a cross-check (90% agreement, κ = 0.77), and a human (AJ) adjudicated the disagreements.

  * AJ ruled on 5.3% of items directly and wrote the rules applied to another 13.9%; 1.6% remained uncertain.
  * Final labels agree with Gemini on 97.6% of items (κ = 0.94).
  * Every post-hoc rule change is logged in `results/appendix\_haiku\_adjudication.md`.

## Authors

AJ Luxton and Cyrus Eosphoros.

