# Acceptance criteria — The Unofficial Guide

Five criteria that say what "working" means for this system, written in unit 1
**before** any results existed.

An acceptance criterion names a target: a number, a count, a rate, or something
a person could plainly observe. *"Retrieval works"* is an opinion. *"For at
least 4 of my 5 test questions, the top results include a chunk containing the
answer"* is a criterion.

Under each one, write a sentence or two on **why that target** and not a
stricter or looser one. A reason that says something about your corpus or your
pipeline earns credit; *"80% seemed reasonable"* does not.

> Missing your own targets next unit costs you nothing. Setting a target so
> easy you can't miss it does.

---

## 1. Retrieved chunks contain the answer

For at least 4 of my 5 test questions, the retrieved chunks include one that
contains the answer.

**Why this target:**
<!-- e.g. "One of my questions is about a topic only two documents mention, so
     I expect that one to be hard." -->
I picked 4 of 5 because one of my questions is about a topic only two documents mention
---

## 2. Every answer names a source

Every answer the system produces names at least one source document.

**Why this target:**
I set this at 5 of 5, not 4, because source naming isn't something the model has to get right on its own: `app.py` builds the `sources` list directly from the metadata on the retrieved chunks, not from anything the model generates.

---

## 3. The relevance gate stops out-of-corpus questions

When I ask a question my documents clearly don't cover, the relevance gate
stops it and the system returns "I don't have enough information about that" —
in at least 4 of 5 tries.

<!-- The five questions are the ones in `OUT_OF_SCOPE` at the bottom of
     `questions.py`, and `run_eval.py` puts them through the gate and writes
     what happened into your run log. Swap them for your own if you'd rather —
     just keep five of them, or the "4 of 5" above has nothing to be 4 of. -->

**Why this target:**
I set 4 of 5 instead of 5 of 5: one borderline case slipping past the gate is realistic, and I'll come back with the actual numbers once I've run the Milestone 4 comparison.

---

## 4. Chunks read as complete thoughts

For at least 4 of 5 chunks I sample by hand, the chunk reads as a complete
thought, with no sentence cut in half at either end.

**Why this target:**
My chunker splits on a fixed `CHUNK_SIZE` of 800 characters (`config.py`)
rather than on sentence or paragraph boundaries, so I expect some chunks to
land mid-sentence. I picked 4 of 5 instead of 5 of 5 because a hard 800-
character cutoff will occasionally cut a sentence in half no matter where the
window falls, and I'd rather set a target I can actually hit than one that
fails on the first bad split.

---

## 5. Named sources are the right sources

For at least 4 of my 5 test questions, the source the system names is a
document that actually contains the answer, not just any retrieved document.

**Why this target:**
Criterion 2 only checks that a source is named, which a system could satisfy
by citing an unrelated chunk. I care more about whether the citation is
trustworthy than whether one exists, so this criterion checks correctness on
top of presence. I used 4 of 5 rather than 5 of 5 for the same reason as
criterion 1: one of my test questions touches a topic with thin coverage in
the corpus, so I expect attribution to be shakier there.

---

<!-- ─────────────────────────────────────────────────────────────────────────
     UNIT 2 — read this before you change anything above.

     If a criterion turns out to be BROKEN rather than merely unmet, you can
     revise it, and that earns credit. But never delete or edit the original
     line. Add the revision underneath it, like this:

         ## 1. Retrieved chunks contain the answer

         For at least 4 of my 5 test questions, the retrieved chunks include
         one that contains the answer.

         **Why this target:** ...

         > **Revised in unit 2:** For at least 4 of 5 questions, the top three
         > results contain the answer.
         >
         > **Why revised:** I couldn't judge "the chunks include one that
         > contains the answer" the same way twice — I scored two questions
         > differently on Monday than on Wednesday. The new version is
         > something I can actually check.

     That's a revision because the criterion couldn't be MEASURED.

     Lowering a target because you missed it is not a revision, and it costs
     you the point:

         ✗ "I said 4 of 5 but got 2 of 5, so 2 of 5 is more realistic."

     A number you missed stays where it is, gets diagnosed, and gets a fix
     attempted. That's where the points are.

     The whole reason the originals stay visible is so someone can see what you
     said before you knew the answer.
     ───────────────────────────────────────────────────────────────────────── -->
