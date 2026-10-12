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

<!-- Each label: a one-sentence definition and two real examples from your
     reading. Then your decision rule for the hardest boundary.

     The decision rule is worth a point on its own and it's the thing most
     people leave out. Every taxonomy has a hardest boundary. Name yours. -->

### Hot_take

**Definition:**
“States a confident opinion with no support”
**Example 1:**

> Yeah we don’t need or want these international friendlies. Only qualification matches should be played. Glad players are starting to fake injuries.

**Example 2:**

> Finally!! Lets go United!! Finally can be hopeful about our midfield.

### Banter

**Definition:**
"Jokes about or taunts a team, player, or fans instead of making a point"
**Example 1:**

> Did Cucurella teach them this tactic after years of being the victim of it?

**Example 2:**

> That's why they brought in Cucurella. They use him for training.

### Argued

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

> Argued and hot_take

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
| Argued    | 30    | 15%   |
| Hot_take  | 120   | 60%   |
| Banter    | 50    | 25%   |
| **Total** | 200   | 100%  |

**Three hard cases**

<!-- Any post that made you pause: what it was, which two labels it could have
     been, and what you chose. These are worth more than the easy 190. -->

**1.**

> _The post:_
> Finally!! Lets go United!! Finally can be hopeful about our midfield
> _Could have been:_
> Argued or hot_take
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
> Argued or hot_take
> \_I chose, argued because: It provide support on why Babeba could be a best fit to handle United midfield issue.

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
| Overall accuracy |          |         |            |
| Macro F1         |          |         |            |
| F1 — `label_one` |          |         |            |
| F1 — `label_two` |          |         |            |

**What I predicted before I looked:**

<!-- Milestone 1 asks you to write this BEFORE seeing the trained numbers. A
     prediction made afterwards isn't one. -->

**What the gap actually means:**

<!-- If the baseline matched your trained model, your fine-tuning added
     nothing — and that is a real finding, not a failure. Say it plainly. -->

---

## Run Log — Before

<!-- Five criteria across three seeds. The notebook's section 6 prints the
     spread table; the Target and Verdict columns are yours. -->

| Criterion | Target | Seed 42 | Seed 7 | Seed 2024 | Verdict |
| --------- | ------ | ------- | ------ | --------- | ------- |
| 1.        |        |         |        |           |         |
| 2.        |        |         |        |           |         |
| 3.        |        |         |        |           |         |
| 4.        |        |         |        |           |         |
| 5.        |        |         |        |           |         |

### Confusion matrix

<!-- ⚠️ TYPED AS A MARKDOWN TABLE. The notebook prints one ready to paste.
     An image of a matrix earns nothing. -->

| true \ predicted |     |     |     |
| ---------------- | --- | --- | --- |
| \*\*\*\*         |     |     |     |
| \*\*\*\*         |     |     |     |
| \*\*\*\*         |     |     |     |

**My biggest off-diagonal number, and what it means:**

<!-- Not "the model made mistakes" — WHICH boundary it didn't learn, and which
     direction. "7 real analysis posts were called hot_take and only 3 went the
     other way" is a direction, not just an error rate. -->

---

## Verdicts and Diagnoses

<!-- MET or MISSED against LAST UNIT's target. The target has to hold across
     all three seeds, not turn up sometimes. -->

| #   | Criterion | Target | Verdict | How I decided |
| --- | --------- | ------ | ------- | ------------- |
| 1   |           |        |         |               |
| 2   |           |        |         |               |
| 3   |           |        |         |               |
| 4   |           |        |         |               |
| 5   |           |        |         |               |

**Diagnoses**

<!-- For each miss: the cause, and how you know. The four common causes are:
     too few examples for a label, a boundary you applied inconsistently, a
     genuinely hard label pair, and a task the model can't reach from this
     much data.

     ⚠️ Use your agreement report as evidence. It is the only instrument you
     have that can tell a LABELLING problem from a MODEL problem, and this
     section is graded on whether you used it that way. -->

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
