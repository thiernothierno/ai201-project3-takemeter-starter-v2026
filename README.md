# TakeMeter

> ### 👋 Start here
>
> **New to this repo? Read [RUNNING.md](RUNNING.md) first** — setup, the
> notebook, the baseline, and what to do when something breaks.
>
> Once `python test.py` passes:
>
> ```bash
> head -5 data/practice_labels.csv     # the shape your labels.csv needs
> ```
>
> Then open `takemeter.ipynb` **in this folder** — in VS Code, or with
> `jupyter notebook` if you prefer. Pick the kernel: the `.venv` inside this
> project. Run section 1, which reports the hardware you'll be training on.
> Everything else waits until you have data.
>
> Nothing to upload, nothing to connect, no accounts and no keys. The notebook
> runs on your machine and writes next to your code.
>
> **The rest of this file is your submission.** Fill it in as you go.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     HOW TO USE THIS FILE

     Unit 5 asks for the first five sections. Unit 6 adds the five below them.

     Everything is pasted as TEXT. No screenshots, no images.

     ⚠️ The confusion matrix especially. The notebook prints one as a markdown
     table, ready to copy. A screenshot of a matrix earns nothing. Paste the
     table.
     ───────────────────────────────────────────────────────────────────────── -->

<!-- ═══════════════════════ UNIT 5 — THE BUILD ═══════════════════════ -->

## What This Does

<!-- Your community, and what your classifier sorts posts into. Three or four
     sentences. -->

This a public soccer community place that highlight information related to soccer's event such as player transfer, games.
Link: https://www.reddit.com/r/soccer

1. Gives a reason vs. just states an opinion ( Nation League Competition)
   Some comments explain why they hold their view. In the Nations League thread, for example, people argued that the extra games leave players too little rest and raise the risk of injury. Others just state their opinion with no explanation, like calling the competition ridiculous.

2. References a specific event vs. stays general (Red card issued to both Real Madrid men and women tean and Carlos Baleba transfer to United State)
   Some comments point to a real event to make their point, such as mentioning Cucurella as an earlier hair-pulling victim, Liverpool fans booing City, or Casemiro leaving Manchester United. Other comments react in general terms without naming any event, player, or moment.

3. Joke/taunt vs. serious point (Red card issued to both Real Madrid men and women tean and Manchester City current cheating claim)
   Some comments make fun of the situation or the other team’s fans. Examples are joking that Cucurella taught Real Madrid’s players to pull hair, or mocking how City fans should feel after the verdict. Others make a serious point, such as arguing that this kind of behavior is part of Real Madrid’s identity.

4. Cites a number vs. doesn’t ( Carlos Baleba transfer price tag)
   A few comments use a number to support their argument, such as saying Baleba’s $70m price tag is too high. Most comments don’t use any numbers and rely only on opinion or general observations.

---

## Label Taxonomy

### Hot_take

**Definition:**
“States a confident opinion with no support”
**Example 1:**

> Yeah we don’t need or want these international friendlies. Only qualification matches should be played. Glad players are starting to fake injuries.

**Example 2:**

> Finally!! Lets go United!! Finally can be hopeful about our midfield.

### Reaction

**Definition:**
"Jokes about or taunts a team, player, or fans instead of making a point"
**Example 1:**

> Did Cucurella teach them this tactic after years of being the victim of it?

**Example 2:**

> That's why they brought in Cucurella. They use him for training.

### Analysis

**Definition:** "Supports its opinion with a reason, number, or specific event"
**Example 1:**

> Some data insights on Baleba compared to other Premier League DMs based on last season's performances:

- 9th in defending
- 15th in tackling
- 21st in dribbling
- 36th in overall rating
- 40th in shooting
- 41st in passing
- 60th in creativity

His biggest strengths are his defensive impact, ball winning and aerial duels. His biggest weaknesses are chance creation, final ball and shot accuracy..

**Example 2:**

> Happy with that. He’s had an off year but the talent was obvious in the season before last. Just have to hope he can refind his form.

### The hardest boundary

**Which two labels:**

> analysis and hot_take

**Borderline comment:**

> You can't have a break in December. Some countries don't even play football during winter at all.

**The decision rule I used every time:**

> If a comment offers any reason, number, or specific event, it's `argued`, even if the reason is weak or doesn't fully support the claim. I label whether support is present, not whether it's convincing. This comment gives a reason ("some countries don't play during winter"), so it's `argued`.

---

## The Dataset

<!-- Where you collected from, how you labelled, your counts, and three hard
     cases. -->

**Where the posts came from:**
[r/soccer](https://www.reddit.com/r/soccer/): comments from the Liverpool vs Man City post-match thread, the Nations League discussion, the Carlos Baleba transfer post, and the Real Madrid red cards post.

**How I labelled them:**
Cold: you read each comment and picked the label yourself, with no AI.

**Counts per label:**

| Label     | Count | Share |
| --------- | ----- | ----- |
| Analysis  | 30    | 15%   |
| Hot_take  | 120   | 60%   |
| Reaction  | 50    | 25%   |
| **Total** | 200   | 100%  |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**

> _The post:_
> Finally!! Lets go United!! Finally can be hopeful about our midfield
> _Could have been:_
> Analysis or hot_take
> \_I chose, hot_take because: It states a confident opinion with no support.

**2.**

> _The post:_
> Some data insights on Baleba compared to other Premier League DMs based on last season's performances:

- 9th in defending
- 15th in tackling
- 21st in dribbling
- 36th in overall rating
- 40th in shooting
- 41st in passing
- 60th in creativity

His biggest strengths are his defensive impact, ball winning and aerial duels. His biggest weaknesses are chance creation, final ball and shot accuracy...

> _Could have been:_
> Analysis or hot_take
> \_I chose, analysis because: It provide support on why Babeba could be a best fit to handle United midfield issue.

**3.**

> _The post:_
> Did Cucurella teach them this tactic after years of being the victim of it?

> _Could have been:_
> hot_take or banter
> \_I chose, banter because: It taunt a player instead of making a point.

---

## The Training Run

<!-- Your starting model, your settings, and anything you changed and why. -->

**Base model:**
"distilbert-base-uncased"

**Settings:**
EPOCHS = 3
LEARNING_RATE = 2e-5
BATCH_SIZE = 16
MAX_LENGTH = 128
SEED = 42

**Anything I changed from the defaults, and why:**

**Split sizes:**
70% train, 15% validation, 15% test.

---

## How I Used AI

**Moment 1**

- \_What I asked for:\_to better understand what is project is about.
- _What came back:_ A great explanation of each step of the project.
- _What I changed:_ I did not change anything.

**Moment 2**

- _What I asked for:_ Why do we need a decision rule between comments.
- \_What came back:\_The decision rule keeps your labels consistent, and a model can only learn from consistent labels
- _What I changed:_ Nothing.

**Pre-labelling disclosure:**

<!-- ═══════════════════════ UNIT 6 — THE TEST ═══════════════════════

     Don't fill these in during unit 5.
     ═══════════════════════════════════════════════════════════════════ -->

---

## Baseline vs. Trained

<!-- Both models on the same posts. `python baseline.py --trained results.json`
     prints this table for you. -->

| Measure          | Baseline | Trained | Difference |
| ---------------- | -------- | ------- | ---------- |
| Overall accuracy | 0.467    | 0.533   | +0.067     |
| Macro F1         | 0.381    | 0.413   | +0.032     |
| F1 — `analysis`  | 0.571    | 0.606   | +0.035     |
| F1 — `hot_take`  | 0.571    | 0.000   | -0.571     |
| F1 — `reaction`  | 0.000    | 0.632   | +0.632     |

**What I predicted before I looked:**

**What I predicted before I looked:**

I didn't record a prediction before running the comparison, so I can't claim one here. Looking back, I would have expected the trained model to do better on `reaction`, since it saw many r/soccer jokes and taunts during training, but that expectation was formed after seeing the results and doesn't count as a prediction.

**What the gap actually means:**

## The trained model beat the baseline by only 0.067 accuracy, which is 2 comments out of 30, so fine-tuning added very little overall. The bigger finding is that each model fails on a different label: the trained model never got hot_take right (F1 0.000), while the baseline never got reaction right (F1 0.000). Fine-tuning taught the model r/soccer’s sarcasm and taunts, which the general model took literally, but it lost the ability to recognize unsupported opinions, my smallest label with only 38 training and 8 test examples. With just 30 test comments, these differences are fragile, and a few comments either way would change them.

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

## Run Log — Before

| Criterion                                                     | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict      |
| ------------------------------------------------------------- | ------ | ------- | ------ | --------- | ------------ |
| 1. `hot_take` has an F1 of at least 0.62 on the held-out set. | 0.62   | 0.000   | 0.000  | 0.000     | Fail         |
| 2. `reaction` has an F1 of at least 0.58 on the held-out set. | 0.58   | 0.632   | 0.706  | 0.727     | Pass         |
| 3. `analysis` has an F1 of at least 0.51 on the held-out set. | 0.51   | 0.606   | 0.629  | 0.733     | Pass         |
| 4. Overall accuracy is at least 0.60 on the held-out set.     | 0.60   | 0.533   | 0.567  | 0.633     | Inconclusive |
| 5. Each label makes up at least 15% of the 200 comments.      | 15%    | 27%     | 27%    | 27%       | Pass         |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted | analysis | hot_take | reaction |
| ---------------- | -------- | -------- | -------- |
| **analysis**     | 10       | 0        | 1        |
| **hot_take**     | 7        | 0        | 1        |
| **reaction**     | 5        | 0        | 6        |

**My biggest off-diagonal number, and what it means:**

7 real `hot_take` comments were predicted as `analysis`, and 0 went the other way. The model never learned the `hot_take`/`analysis` boundary. The entire `hot_take` column is 0, so it never predicts `hot_take` at all, and anything that looks like an opinion gets pushed into `analysis`. The same pull shows up with `reaction`: 5 real `reaction` comments were called `analysis`, while only 1 `analysis` comment was called `reaction`. The model treats `analysis` as its default answer.

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| #   | Criterion                | Target | Verdict | How I decided                                                                                                      |
| --- | ------------------------ | ------ | ------- | ------------------------------------------------------------------------------------------------------------------ |
| 1   | `hot_take` F1            | ≥ 0.62 | MISSED  | 0.000 on all three seeds (42, 7, 2024).                                                                            |
| 2   | `reaction` F1            | ≥ 0.58 | MET     | Lowest seed was 0.632 (seed 42), above target on all three.                                                        |
| 3   | `analysis` F1            | ≥ 0.51 | MET     | Lowest seed was 0.606 (seed 42), above target on all three.                                                        |
| 4   | Overall accuracy         | ≥ 0.60 | MISSED  | Only seed 2024 reached it (0.633). Seeds 42 (0.533) and 7 (0.567) fell short, so it doesn't hold across all three. |
| 5   | Each label ≥ 15% of data | ≥ 15%  | MET     | Smallest label is `hot_take` at 54/200 = 27%. This is a dataset property, so it's the same for every seed.         |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

**Miss 1: `hot_take` F1 = 0.000**

Cause: a boundary I applied inconsistently between `hot_take` and `analysis`, made worse by `hot_take` being my smallest label (38 training examples).

How I know: The confusion matrix shows the model sends every `hot_take` comment somewhere else, mostly to `analysis` (7 of 8). My agreement report shows [INSERT: agreement on `hot_take`, e.g. "I agreed with my own earlier labels on only X of Y hot_take comments"], compared with [INSERT: agreement on analysis/reaction]. Low agreement on `hot_take` means the labels themselves were inconsistent, so this is a labelling problem, not only a model problem. My decision rule ("any reason, even a weak one, makes it `analysis`") also made the boundary hard to apply: many confident opinions contain a half-reason, so similar comments ended up on both sides.

**Miss 4: Overall accuracy below 0.60 on 2 of 3 seeds**

Cause: mostly a knock-on effect of Miss 1.

How I know: `hot_take` is 8 of the 30 test comments, and the model gets all 8 wrong on every seed. Even if everything else were perfect, the best possible accuracy would be 22/30 = 0.733. The real ceiling is lower, because 5 `reaction` comments also go to `analysis`. Fixing the `hot_take` boundary would fix most of this miss.

---

## Agreement Report

<!-- Your rate against the staff set, and every disagreement adjudicated.

     Remember you labelled these 30 under the STAFF taxonomy in
     data/staff_taxonomy.md, not your own — so every argument below is made
     from those definitions and those decision rules. -->

**Agreement rate:** **_ / 30 = _**%

<!-- Nobody grades this number. A 60% who argues every disagreement from the
     stated rules beats a 95% who wrote "staff was right" nine times. Several
     of the 30 were chosen because they're genuinely ambiguous — you should be
     winning some of these. -->

**Disagreements**

<!-- Three lines each: the post, both labels, and who you think is right and
     why — grounded in the staff definitions you were both applying.

     Then sort each into one of three piles:
       (a) the rule covered it and I applied it loosely → a consistency problem
       (b) the rule genuinely doesn't say               → a gap in the definitions
       (c) the rule is ambiguous here and my reading is defensible → argue it.
           This is a legitimate win.

     Pile (a) is the one that matters most for your diagnosis: if you applied a
     written rule two different ways on 30 posts, that is direct evidence about
     what you did across your own 200. -->

**1.**

> _The post:_
>
> _Staff said / I said:_
>
> _My call, and why:_
>
> _Which pile:_

**2.**

> _The post:_
>
> _Staff said / I said:_
>
> _My call, and why:_
>
> _Which pile:_

**What the pattern in my disagreements tells me:**

---

## The Improvement

**What I changed:**

**Which diagnosis pointed at it:**

### Run Log — After

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
| --------- | ------ | ------- | ------ | --------- | ------- |
| 1.        |        |         |        |           |         |
| 2.        |        |         |        |           |         |
| 3.        |        |         |        |           |         |
| 4.        |        |         |        |           |         |
| 5.        |        |         |        |           |         |

**Did it help, and how do I know:**

<!-- If it didn't, say so. Relabelling that didn't help is a genuinely
     interesting result and earns full credit. -->

---

## What's Still Broken

<!-- For each criterion still missed: what you'd do, and why you stopped. -->

**The gap between what I meant my labels to capture and what the model
learned:**

<!-- Two sentences. Your confusion matrix is the evidence. -->

<!-- ═════════════════════════════════════════════════════════════════════

     SUBMISSION CHECKLIST — unit 5

       [ ] criteria.md has five numbered criteria, each naming a NUMBER
       [ ] Each has a reason underneath tied to your data or taxonomy
       [ ] labels.csv: at least 150 rows, text/label/note, ONE file not split
       [ ] No label above 70%
       [ ] All five unit 5 sections have real content
       [ ] Label Taxonomy includes the decision rule for your hardest boundary
       [ ] The Dataset includes three hard cases
       [ ] results.json and test_split.csv committed (the notebook does this)
       [ ] At least four new commits
       [ ] Repository URL submitted — WRITE IT DOWN

     SUBMISSION CHECKLIST — unit 6

       [ ] Baseline vs. Trained table, with your prediction written beforehand
       [ ] Run Log — Before, five criteria across three seeds
       [ ] Confusion matrix TYPED AS A MARKDOWN TABLE
       [ ] A verdict on every criterion
       [ ] A diagnosis for every miss, using the agreement report as evidence
       [ ] Agreement Report with every disagreement adjudicated
       [ ] One improvement, with Run Log — After
       [ ] What's Still Broken
       [ ] results_three_seeds_before.json, results_three_seeds_after.json,
           baseline_results.json and
           agreement_results.json committed
       [ ] At least four new commits
       [ ] The SAME repository URL as last unit

     Do not delete and recreate this repository.
     ═════════════════════════════════════════════════════════════════════ -->

---

📖 **How to run this project: [RUNNING.md](RUNNING.md)**
