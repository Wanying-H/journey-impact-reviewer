# Journey Impact

When something changes — a regulation, a pricing model, a platform migration — someone has to work out which parts of your customer journeys are affected, and how much work that means.

This is a small tool for doing that assessment, and for showing your working.

**[Open the tool →](https://wanying-h.github.io/journey-impact-reviewer/)**

---

> ### The example data is made up
>
> Everything in `example-pricing-change.md` and `example-journey.json` is fictional. It describes an invented bike hire operator called *Ridewise* changing its pricing. It is not from any real organisation, and it is not connected to any real programme of work. It exists so you can click around and see how the tool behaves before putting your own material in.

---

## How it works

You bring two things: a **change model** — a numbered list of what's changing — and a **journey map**.

An AI assistant matches them. For each step of the journey it says which changes land there, quotes the wording that makes it relevant, and says how sure it is. Then a person goes through and decides.

The assistant narrows things down. It does not decide.

## Nothing leaves your machine

A single HTML file. No build step, no server, no analytics, no network calls. Everything you type stays in your browser.

That matters because journey maps and change models usually contain internal material. If you use an AI assistant for the extraction step, use whichever one your organisation has approved — the tool itself never sends anything anywhere.

## Try it

1. Open the tool
2. Click **Paste JSON**, paste the contents of [`example-journey.json`](example-journey.json), choose **Create new map**
3. Click **Key** in the toolbar to see what every label means

You'll see six steps of a bike hire journey, with eight fictional changes matched against them. One change isn't covered by any step — the coverage panel flags it. That's the part worth paying attention to.

## Using it for real

**1. Write your change model**

A numbered list, one entry per change. [`example-pricing-change.md`](example-pricing-change.md) shows the shape:

```
## CH-01 · Per-minute pricing replaces day pass

- Before: One flat price buys 24 hours of unlimited rides.
- After: Riders are charged per minute of active hire, with a daily cap.
- What changes: price, data
- Who is affected: customers, systems
- Source: Pricing Review deck — slide 4
- Confidence: Stated
```

This part is human work. An assistant can draft it from your documents, but somebody who understands the change has to check it. Everything downstream is only as good as this list — if a change is described too vaguely here, the matching later will be vague too.

Keep it wherever your organisation keeps internal documents. Not in a public repository.

**2. Match it against a journey**

Copy [`prompt.md`](prompt.md), paste your change model into the placeholder at the bottom, and give the whole thing to your assistant along with the journey map.

**3. Review**

Paste the JSON into the tool. Then go through it:

- Sort by **Check** first — those are the ones the assistant knew it couldn't answer
- Then **Implied** — the assistant reasoned these out, so the reasoning is worth reading
- **Stated** ones just need the quote glancing at

Nothing counts as reviewed until someone clicks. If you overrule the assistant, the tool keeps what it originally said next to your decision — so the exported file shows where the machine and the person disagreed.

**4. Check what isn't covered**

The coverage panel shows how many of your changes appear anywhere in this journey. The ones that don't are the interesting ones: either they belong to a different journey, or nobody has thought about them yet.

A missed change is invisible until you go looking for it. This is the going-looking.

## What you can filter by

Click anything to filter the table:

- A number in the summary bar — new steps, changed steps, wording-only, awaiting review
- A change tag inside a step — shows every step that change touches
- An affected-group tag — shows everything the billing team, or advisors, or brokers have to act on

Useful when handing over: filter to one group, export, send them only their part.

## Export

- **Export PDF** — one continuous page, sized to the map. The map is embedded as an image, so the text isn't selectable.
- **Export JPG** — for slides
- **Save copy** — an HTML file with your data written into it. Reopen it, or send it to someone.

Filters apply to exports, so you can produce a view containing only what one team needs.

## Saving your work

Two layers:

- **Automatic** — saves to your browser as you type
- **Save copy** — downloads a file. Browser storage gets cleared eventually; a file doesn't. Do this at the end of a session.

One HTML file can hold as many journeys as you like; switch between them from the dropdown.

⚠️ **A saved copy contains your data.** It looks identical to the blank tool. Don't commit one to a public repository — the included `.gitignore` covers the default filenames, but check before you push.

## Hosting your own copy

1. Fork this repo
2. **Settings → Pages → Source: deploy from branch → main → / (root)**
3. It appears at `https://wanying-h.github.io/journey-impact-reviewer/`

Or download `index.html` and double-click it. Works the same offline.

## Changing it

One self-contained file, no framework, no build. Colours are CSS custom properties at the top:

```css
:root{
  --navy:#002D72;        /* step headers, primary actions */
  --insight-bg:#F1F4FA;  /* insight row */
  --wait-bg:#FDFBF6;     /* awaiting review */
  --done-bg:#F6FAF7;     /* reviewed */
}
```

The four impact categories — new step, changed, wording, no change — are `CHANGE_TYPE` in the script. If your organisation already has language for this, use yours instead. Change the labels there and the definitions in `prompt.md` to match.

The affected groups are `PARTY`, in the same place.

## The idea, in one line

The machine narrows the field and shows its evidence. The person decides and the decision is recorded. What nobody has looked at yet stays visible.

## Known limits

- Very large journeys may fail to export as an image — filter first, or use PDF
- The save dialog needs a recent Chrome or Edge; elsewhere files go to your downloads folder
- Exported PDFs contain the map as an image, so the text isn't searchable

## Licence

MIT. Use it, change it, ship it.
