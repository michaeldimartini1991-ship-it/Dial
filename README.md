# Dial

**An investing tool built around the way college athletes actually get paid.**

NIL (name, image and likeness) income doesn't arrive as a paycheck. It comes in chunks, from a handful of deals, over an earning window that can close with one injury or the end of eligibility. Existing NIL money apps track deals and set aside taxes, then stop. Dial answers the next question: **what should an athlete do with the money that's left, and how much investment risk can they afford, given how uncertain their income is?**

## The core idea

An athlete's future earnings are part of their wealth. When those earnings are uncertain, a calmer portfolio keeps a bad market year from landing at the same time as a dry spell in deals. (In financial planning this is called *human capital*.) Dial turns that idea into a number:

1. **Income risk (0–100)** measures how uncertain the athlete's NIL income is.
2. Income risk translates into a **recommended range on the risk dial** (0 = calmest, 100 = wildest).
3. The dial builds a diversified, low-cost portfolio for that level of risk.

## How income risk is scored

Four factors, each scored from 0 (steady) to 1 (risky), weighted to total 100:

| Factor | What it measures | Weight |
|---|---|---|
| Eligibility left | `1 − years left / 4`, so a shorter window is riskier | 30 |
| Pro prospects | `1 − chance of a pro career` | 20 |
| Biggest chunk | Largest payment ÷ total received in the last 12 months | 25 |
| Signed ahead | `1 − (signed for next 12 months ÷ received in last 12)`, capped 0–1 | 25 |

**Recommended dial range:** top = `100 − 0.7 × income risk`, bottom = top − 35, suggested = midpoint. A dial set above the top is capped there.

**Cash cushion:** 3 to 12 months of costs, scaling with income risk.

**Tax set-aside:** federal rate (default 25%, for federal income and self-employment tax) × NIL income received since January 1, plus state income tax for the athlete's state using 2026 single-filer brackets (Tax Foundation, as of January 1, 2026), minus taxes already paid.

The weights and limits are judgment calls, not estimates from data. They're kept as named constants at the top of the engine so they're easy to test and change.

## What's in the app

| Tab | What it does |
|---|---|
| **Income** | Enter NIL payments (past = received, future = signed). See income risk, the recommended dial, and how cash splits between taxes, a cushion and investing. |
| **Dial** | Choose a risk level, with the recommended range shown on the gauge. |
| **Portfolio** | The resulting mix across eight asset classes, in dollars. |
| **Picks** | Example low-cost index funds for each slice. |
| **Outlook** | A Monte Carlo simulation (1,000 paths) of possible outcomes, plus stress tests for 2008-style and 2022-style years. |
| **Check-in** | A yearly update: what changed in the athlete's career, and whether the dial should move. |

## Under the hood

- Portfolio risk uses a full correlation matrix across asset classes rather than averaging each asset's volatility.
- The simulation is seeded, so results are repeatable.
- Everything runs in the browser. There's no server, and entries are saved only in the viewer's own browser.
- One self-contained file: plain HTML, CSS and JavaScript, no frameworks.

## Limitations

- Expected returns, volatilities and correlations are round-number assumptions, not estimates from historical data.
- The simulation assumes normally distributed yearly returns, which understates extreme crashes.
- The income risk weights haven't been validated against real athlete outcomes.
- Taxes are an estimate. Federal tax is a flat rate, and state tax applies brackets to gross NIL income with no deductions, so it leans high. Local income taxes (such as New York City's) are not included.

## Possible next steps

- Estimate return and risk inputs from historical index data.
- Test the income risk score on real or realistic athlete profiles.
- Sample past returns instead of assuming a bell curve.

## Run it

Open `index.html` in any browser. To host it, upload it to GitHub Pages, Netlify or any static host.

---

*Educational tool, not investment, tax or legal advice.*
