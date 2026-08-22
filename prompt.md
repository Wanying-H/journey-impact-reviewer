# The prompt

Copy the block below, paste your change model into the placeholder at the bottom, and send the whole thing to your AI assistant along with the journey map.

The assistant returns JSON. Paste that into the tool via **Paste JSON**.

> Use whichever assistant your organisation has approved for internal documents. Journey maps and change models usually contain material that shouldn't leave your organisation.

---

```
You are assessing how a set of known changes affects a customer journey.

I am giving you two things: a CHANGE MODEL (a numbered list of changes) and a customer journey map.

Your job is to match them. You are not judging how important anything is — you are finding which changes touch which steps, and showing me the evidence.

Return ONLY a JSON object. No commentary, no code fences.


READ THE MAP FIRST

A journey map is a grid. The columns running left to right are the STEPS. The rows are different KINDS of content — what the customer does, what they feel, their pain points, their questions, opportunities. Identify both before reading any cell. Every piece of text belongs to one column and one row. Keep that mapping.


FOR EACH STEP

name — the column's short label, under 8 words. It names the phase, not its contents. Never append actions or pain points into it.
  Wrong: "Learn from reps and trainers, in addition to lunch boxes, closed FB groups"
  Right: "Learn about the product"

action — an array of what the customer does, taken from the actions row of that column only. Verb-first, one per item, in the order the map shows. If there are arrows or numbers inside the step, follow that sequence. No feelings or complaints here.

insight — an array of at most 4 items, synthesising the pains, needs, questions and opportunities shown for that column. Merge near-duplicates. Drop anything that just restates an action. Prioritise pain points, then unmet needs, then open questions, then opportunities. Write each as a statement of what is true for the customer — "Can't tell whether the price is competitive", not "Pricing". Keep the customer's own words where the map quotes them.

changes — an array of the changes from the CHANGE MODEL that affect this step. For each:
  - id: the change ID exactly as written in the model
  - quote: the wording from the CHANGE MODEL that makes it relevant, under 20 words
  - evidence: "stated" if the model explicitly covers this situation
              "implied" if you reasoned it out
              "check" if a person who knows the change has to decide
  Use [] if nothing in the model touches this step. An empty array is a valid and expected answer.

changeType — what has to happen to this step. One of:
  "new"      — a step that does not exist today has to be added around here
  "changed"  — the step exists but what happens inside it changes
  "wording"  — the process is identical; only what we say to the customer changes
  "none"     — this step is unaffected
  ""         — you cannot tell
  Leave it "" rather than guessing. If changes is empty, changeType should be "none" or "".

affected — an array of who must do something because of the matched changes. Only these values:
  "customers" — what the customer sees, does or receives at this step changes
  "advisors"  — support advisors need new knowledge, scripts or training
  "TPIs"      — third-party intermediaries have to do something differently
  "billing"   — the billing team's process or checks change
  "systems"   — a system change is needed: data, configuration or code
  Only include a party if a matched change forces them to act. Being present in the step is not enough — a customer appears in almost every step, but "customers" applies only when what they see or do actually changes. [] is valid. Listing all five should be rare; if you find yourself doing it, check whether you are describing presence rather than action.

reason — one sentence under 30 words. Why these changes land on this step, pointing at the step's own content. If changes is empty, say what you looked for and didn't find.

reviewStatus — always "ai_suggested". Never "confirmed". Only a person confirms.


ALSO RETURN

changeModel — every change from the model I gave you, as {"id": "...", "name": "..."}, whether or not it matched anything. This is used to see what the journey does not cover.


OUTPUT SHAPE

{
  "title": "",
  "subtitle": "",
  "changeModel": [{"id": "CH-01", "name": ""}],
  "steps": [
    {
      "name": "",
      "action": [""],
      "insight": [""],
      "changes": [{"id": "", "quote": "", "evidence": "stated"}],
      "changeType": "",
      "affected": [""],
      "reason": "",
      "reviewStatus": "ai_suggested"
    }
  ]
}


BEFORE YOU OUTPUT, CHECK

- Every change ID you cite exists in the CHANGE MODEL. Never invent one.
- Every quote is text from the CHANGE MODEL, not your paraphrase.
- changeModel is complete, including changes that matched nothing.
- You have used nothing you know about this subject from outside the CHANGE MODEL.
- Step names are free of action content and under 8 words.
- No step has more than 4 insights.
- The number of steps matches the number of columns in the map.

If the map groups steps under stages or phases, ignore the grouping and return one flat list in the original order.
Ignore screenshots, internal system swimlanes, and anything outside these fields.

---

CHANGE MODEL:

[paste your change model here]
```

---

## If the result isn't right

**Steps and actions are mixed together** — the assistant read the text without reading the grid. Send the map again in two or three chunks of four or five columns each.

**Insights are missing** — ask:

> Which steps did you leave with an empty insight array, and what was on the map at those positions?

If it says it wasn't sure which column an insight belonged to, that's a layout problem, not a content one. Tell it which row holds the insights.

**Insights are transcribed rather than summarised** — ask:

> Reduce every insight array to at most three items by merging near-duplicates. Keep the customer's wording where the map quotes them.

**Almost everything is "implied"** — this usually means the change model is written too abstractly, not that the assistant is guessing badly. Go back to the model and make the entries concrete: which action, which data, which moment.

**Every step lists all five affected groups** — the assistant is describing presence rather than action. Ask:

> For each party you listed, name the change that forces them to act. Remove any you can't attribute to a specific change.

**Nothing is marked as affected at all** — ask:

> Which changes in the model did you consider and rule out for each step, and why?

That question is often more revealing than the original answer.

## Adapting it

The five affected groups and the four impact categories are a starting point, not a standard. If your organisation already has language for who does what, use yours — change the definitions here and `PARTY` / `CHANGE_TYPE` in `index.html` to match.

What's worth keeping is the shape: the assistant narrows the field and cites its evidence, a person decides, and whatever nobody has looked at stays visible.
