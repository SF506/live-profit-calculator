---
name: live-profit-calculator
description: "Builds a live, interactive profit calculator page for any product or service: per-unit costs, monthly costs, break-even, batch view, scenarios, goal-seek and sensitivity."
---

# Live Profit Calculator

Build one self-contained HTML page, published as an artifact, where every cost has its own control and the results update live. This skill makes the calculator only. It does not research the market, compare competitor prices or judge whether the idea is good; that work belongs to a business-plan skill.

It works for any field: physical products, food, clothing, digital products, subscriptions, services, courses, events. Everything is driven by the user's own numbers.

## Scope: profit only

The calculator is about profit: what each sale keeps, what each month keeps, and what a whole batch keeps. Leave operations to the user. Do not model stock levels, reorder timing, stock-outs, lead times or a month-by-month cash balance unless the user asks for them.

## Rules

1. Use only the user's numbers. Never inflate, pad or add a reserve on your own. If a number is missing, ask. If the user can't give it, use a clearly labelled guess (show "guess" next to it) and say so.
2. Build costs from their real parts. If the user gives the parts (for example item price, shipping per kg, minimum shipment weight, weight per unit), use those parts as separate controls. Never replace them with a rounded total. Weight-based shipping: shipping = rate × max(units × unit weight, minimum weight), so a small order still pays for the minimum weight; show the shipping per unit that results.
3. Extra costs the user didn't mention, or costs they say they'll add later (for example commission), go in an "Optional costs" group set to 0 by default.
4. Deduct costs in the order the user describes. Ask for the order if it isn't obvious (for example: discount first, then payment fee, then everything else). Percent fees are charged on whatever base the user says, including any shipping fee the customer pays, and the page explains that in one line.
5. Before building, restate every cost, its unit (per order, per unit, percent, monthly, one-time) and the deduction order. Wait for a yes.
6. Nothing in the page is tied to one brand or field until the user's intake fills it in. Labels come from the user's own words ("pair", "seat", "session", "box", "license").
7. Never leave a key number blank or as a dash. If a value can't be reached, say so in words (for example "Not reachable at these numbers").
8. Write page copy in short, plain words. No jargon; if a term is needed (ROAS, break-even), explain it in one line.
9. After every change the user asks for, update the file, republish to the same URL and confirm in one line what changed.

## Step 1: Setup interview

The results are only as accurate as the inputs, so interview the user before building anything.

- If a `grill-me` or `interview-me` skill is available, load it with the Skill tool and run the interview through it, using the topics below as its agenda.
- If neither is available, ask the questions yourself: one message, grouped by topic, numbered so the user can answer by number.
- Either way:
  - Let the user skip what doesn't apply.
  - Ask follow-ups wherever an answer is vague ("around", "maybe", a range, a missing unit).
  - Ask about any cost that is mentioned but unclear: what it's charged on, and whether it applies to every order.
  - Stop when every cost has a number, a unit and a place in the deduction order.

Topics to cover:

1. **Product and field.** What are you selling, and what is one unit called?
2. **Price.** Price per unit, and the currency.
3. **Unit cost.** Cost to make or buy one unit, broken into its parts where possible: item price, shipping (flat, per unit, or per kg with any minimum weight, plus weight per unit), customs and taxes. Or the cost to deliver one unit of service. Is this a final quote or an estimate?
4. **Batch.** Is there a first batch or one-time setup cost? How many units, and how much?
5. **Per-order costs.** For example: discount codes and the share of orders that use them, affiliate or influencer commission, payment gateway fee (fixed + percent, and what it's charged on), shipping you cover, shipping the customer pays, packaging, platform commission. For each one: per order or per unit? Every order or only some?
6. **Deduction order.** In what order should these come off the price?
7. **Monthly costs.** For example: store platform, software, rent, salaries, tools.
8. **Paid ads.** Monthly ad budget, kept separate from other costs.
9. **Sales.** Expected units per month. Where does the estimate come from?
10. **Batch period.** How many months do you expect to take to sell one batch?
11. **Goal.** Any target (monthly revenue, monthly profit, units)?
12. **Packs, plans or tiers.** Bundles, packs, plans, tiers or subscriptions (for example 2-for-X, monthly and yearly plans, basic/pro/premium)? If yes, list each one: name, price, what it includes, and whether per-order costs apply once per order or per unit. If no, leave the section out.
13. **Taxes and returns.** Is sales tax or VAT included in your price, and at what rate? Do you expect returns, refunds, failed deliveries or chargebacks?
14. **Look and language.** Use the default style (Step 2) or your own brand colours, fonts and logo? Which language or languages?

## Step 2: Look and style

Use this unless the user gives their own brand guide; if they do, keep the same layout and quality bar in their colours and fonts.

A dark, calm, premium dashboard. Near-black background with slightly lighter panels and thin borders. Off-white text, grey for labels. One warm accent colour (amber or gold) for the profit figure and key highlights. Green for profit and red for loss, always with a + or − sign so colour is never the only signal. Big, bold key numbers; everything else small and quiet. Small uppercase section labels with a short accent line before them. Rounded panels, no heavy shadows, no gradients, no emoji or illustrations. Arabic font: IBM Plex Sans Arabic. English font: Inter. Numbers line up in columns (tabular figures), right-aligned, with thousands separators and units. Tables have quiet row dividers and a highlighted total row.

Desktop: controls on the left, results on the right, with a sticky top bar holding the product name and the theme and language buttons. Phone: one column, large tap-friendly boxes, 16px side gutter, no sideways page scroll; wide tables scroll inside their own box. Offer a light theme through a button, but open in dark.

## The model

Keep the math in one pure function so every section uses the same numbers:

```
order(v, P, q):                 // P = order price, q = units in the order
  cs        = codeShare/100
  discount  = cs * P * disc/100
  afterDisc = P - discount
  gateway   = payFix + payPct/100 * (afterDisc + customerShipping)   // base as the user says
  tax       = taxOn ? afterDisc * rate/(100+rate) : 0                  // only if tax is included in the price
  unitCost  = itemPrice + shippingPerUnit + otherLandedPerUnit         // from real parts (Rule 2)
  steps     = [discount, gateway, tax, unitCost*q, cs*commission, shippingYouCover, packaging, ...userCosts, returnRate*returnCost]
  keep      = P - sum(steps)
```

Reorder `steps` to match the user's deduction order. Drop any cost the user doesn't have.

- Monthly profit = units per month × keep − monthly costs − ads.
- Break-even = units per month needed to cover monthly costs + ads (round up (monthly costs + ads) ÷ keep), and the revenue at that point.
- Batch over period = batch units × keep − period months × (each monthly cost + ads).

Check the model in node with the user's defaults before building the page, and state the headline numbers.

## Page sections

- **Top:**
  - Product name and a short line saying these are the user's numbers.
  - KPI strip of 4: kept per sale, monthly profit, break-even units per month, maximum ad spend per sale.
- **Controls (left menu):** grouped: product and price, per-order costs, optional costs, unit cost (with its real parts), monthly costs, sales and targets, batch period. Each control has a label with its unit and a one-line note when needed. Every input the results use must be in this menu, including the batch period.
- **Break-even and goal-seek:**
  - Break-even units per month, revenue at break-even, and a profit/loss pill at the user's sales.
  - Solve for: units needed to reach the user's revenue or profit target, the lowest price that breaks even at the user's sales, and the highest discount-code share that still breaks even. A button applies an answer to the controls.
  - Say plainly if a goal can't be reached by changing that one input.
- **One order, step by step:**
  - Stacked bar of one order: each cost plus what's kept, with a legend.
  - Step table with columns: per sale, per month, per batch, running balance. Rows: price, each cost, kept.
  - Under that, in the per-month column, list each monthly cost as its own row (platform, software, other, ads), then the monthly profit total, so the column adds up.
  - Revenue target status (below / within / above).
- **Whole batch over the period:**
  - Period length (months, from the menu), units in the batch, monthly sales needed to sell it in that period, batch revenue, batch margin before monthly costs.
  - Each monthly cost listed separately as months × amount (for example "6 × 299"), then the total running costs.
  - Batch profit and profit per unit.
- **Sensitivity:** move each input ±10% and rank inputs by their effect on monthly profit (bars, biggest first). Add one plain line: "Shows which number moves your profit most. Long bar = small change, big effect; work on those first."
- **Ad planner:**
  - Monthly ad budget.
  - Ad ceiling per sale = kept per sale − monthly costs ÷ monthly units.
  - Break-even ROAS = price after discount ÷ kept per sale, with a one-line explanation.
  - Sales the ad budget must bring in to not lose money.
  - Pause rule: pause if cost per sale goes above half the ceiling.
- **Scenarios:**
  - Three slots: Worst, Base, Best.
  - Base always follows the current inputs live.
  - Worst and Best start as clearly labelled live examples built from the user's own numbers, and change more than one input so per-sale figures differ too (for example Worst: half sales and every order uses the discount code; Best: 1.5× sales and no codes). Show what each example changes.
  - "Save current" fixes a slot; a saved slot gets "Load" and "Clear" (Clear turns it back into the live example).
  - Comparison table: sales, the other changed inputs, revenue, kept per sale, monthly profit, break-even units, ad ceiling.
- **Packs, plans or tiers** (only if the user offers them): price, what the customer pays after discount, kept per order, kept per unit or per month, using the same `order()` function.
- **Copy summary** button (clipboard API, falling back to a selectable text box) and a reset button.

Only add stock, reorder or cash-over-time sections if the user asks for them.

## Build details

- One self-contained HTML file: inline CSS and JS, no chart libraries (draw charts as inline SVG or CSS bars).
- Theme tokens on `:root`, dark by default, light behind the button.
- If the user wants two languages, one button switches all text, direction (RTL/LTR) and number formatting from a single string dictionary.
- Remember inputs, theme, language and saved scenarios in localStorage, wrapped in try/catch so the page still works without it.

## Verify before publishing

1. Run `order()` and the batch math in node with the defaults, and confirm the numbers you restated.
2. Open the page with Playwright in every language and theme, at desktop (1280px) and phone (390px) width. Check for console errors, horizontal overflow, blank key numbers, and numbers that don't match the node run. Change an input and confirm every section (scenarios included) updates.
3. Go through every section and rule in this skill and confirm each one is on the page.
4. Publish as an artifact. Reply with one line on what the page is and the headline numbers: kept per sale, monthly profit, break-even units, ad ceiling and any warning.

## Sharing

When the user wants to share with someone who doesn't use Claude, or use it on a phone:
- Tell them to open the page's Share menu and choose "Anyone with the link", then test the link in a private browser window while signed out.
- If a public link is blocked, offer the page as a standalone HTML file (send it with SendUserFile) that they can pass on by WhatsApp or email and open in any phone browser. Each person's changes save only on their own device.
