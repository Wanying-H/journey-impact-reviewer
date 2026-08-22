# Example change model — a pricing change

> ## This is made up
>
> Every entry below is invented. *Ridewise* is not a real company. The documents cited — "Pricing Review deck", "Ops policy draft v2", "Finance note" — do not exist. None of this comes from any organisation, and it is not connected to any real programme of work.
>
> It exists for one reason: so you can load something into the tool and see how it behaves before you put real material in.

**The scenario:** *Ridewise*, a fictional bike hire operator, is moving from a flat-rate day pass to per-minute pricing with off-peak discounts. The list below is what changes as a result.

**Notice what's deliberately imperfect.** CH-06 and CH-07 are marked *Implied* — they were inferred rather than stated outright. CH-08 is *Contested*: two documents disagree, and both readings are recorded rather than one being quietly picked. Real change models look like this. A list where everything is confidently *Stated* usually means somebody smoothed over the disagreements.

## Where your own version lives

A file like this one, kept wherever your organisation keeps internal documents. **Not in a public repository.** The `.gitignore` in this repo excludes `change-model.md` by default, but that only helps if you use that filename — check before you push.

---

## CH-01 · Per-minute pricing replaces day pass

- **Before:** One flat price buys 24 hours of unlimited rides.
- **After:** Riders are charged per minute of active hire, with a daily cap.
- **What changes:** price, data
- **Who is affected:** customers, systems
- **Source:** Pricing Review deck — slide 4
- **Confidence:** Stated

## CH-02 · Off-peak discount band

- **Before:** No time-based variation.
- **After:** Rides starting between 10:00 and 15:00 are charged at 60% of the standard rate.
- **What changes:** price, timing
- **Who is affected:** customers, systems
- **Source:** Pricing Review deck — slide 6
- **Confidence:** Stated

## CH-03 · Fare shown before unlock

- **Before:** Riders see the day pass price at checkout only.
- **After:** The applicable rate must be shown on the bike detail screen before the rider unlocks.
- **What changes:** customer communication, systems
- **Who is affected:** customers, systems
- **Source:** Pricing Review deck — slide 9
- **Confidence:** Stated

## CH-04 · Live fare during the ride

- **Before:** Nothing is shown during a ride.
- **After:** The app shows a running total, updated at least every 60 seconds.
- **What changes:** data, timing, systems
- **Who is affected:** customers, systems
- **Source:** Product requirements — section 3.2
- **Confidence:** Stated

## CH-05 · Receipt itemisation

- **Before:** A single line: "Day pass".
- **After:** Receipts must show duration, rate band applied, and any cap reached.
- **What changes:** customer communication, data
- **Who is affected:** customers, billing team
- **Source:** Product requirements — section 5
- **Confidence:** Stated

## CH-06 · Refund rules for interrupted rides

- **Before:** No refunds; the pass covered the whole day.
- **After:** Time is not charged when a ride is interrupted by a mechanical fault, once confirmed.
- **What changes:** roles, price
- **Who is affected:** customers, advisors, billing team
- **Source:** Ops policy draft v2 — page 3
- **Confidence:** Implied

## CH-07 · Advisor fare lookup tool

- **Before:** Advisors could confirm a day pass from the account screen.
- **After:** Advisors need a tool that reconstructs how a fare was calculated, to answer disputes.
- **What changes:** roles, systems
- **Who is affected:** advisors, systems
- **Source:** Ops policy draft v2 — page 5
- **Confidence:** Implied

## CH-08 · Corporate account billing cycle

- **Before:** Corporate accounts are invoiced per pass purchased.
- **After:** Corporate accounts move to a monthly consolidated invoice.
- **What changes:** timing, data
- **Who is affected:** billing team, systems
- **Source:** Finance note — 14 March
- **Confidence:** Contested — the Pricing Review deck still shows per-pass invoicing on slide 12
