---
name: vehicle-data
description: Look up vehicle data with the Auto.dev connector. Use when the user gives a VIN or a license plate, asks about a specific car's specs, trim, photos, recalls, payments, interest rate, taxes and fees, or cost of ownership, or wants to find cars for sale by make, model, year, price, mileage, state, or ZIP code.
---

# Vehicle data with Auto.dev

The Auto.dev connector (`auto-dev`) answers vehicle questions with live data. Use its tools
instead of guessing specs, prices, or recall status from memory.

## Pick the tool

| The user wants | Tool | Plan |
| --- | --- | --- |
| What a VIN is: year, make, model, trim, engine, drivetrain | `auto_decode` | Free |
| Cars for sale matching filters | `auto_listings` | Free |
| Photos of a vehicle | `auto_photos` | Free |
| Full specifications | `auto_specs` | Growth |
| OEM build sheet, factory options | `auto_build` | Growth |
| Safety recalls | `auto_recalls` | Growth |
| Monthly payment estimate | `auto_payments` | Growth |
| Interest rate estimate | `auto_apr` | Growth |
| Total cost of ownership | `auto_tco` | Growth |
| Everything about one VIN in one call | `fetch` | Free for listing, decode, and photos; Growth adds specs, recalls, and cost of ownership |
| Recalls not yet repaired | `auto_open_recalls` | Scale |
| License plate to VIN | `auto_plate` | Scale |
| Taxes and fees estimate | `auto_taxes` | Scale |
| Parameter names or response fields | `auto_docs` | All plans |

If the user tells you their plan, skip tools it doesn't include. When you're unsure of a
parameter, call `auto_docs` with the tool's topic (for example `listings` or `payments`) before
calling the tool.

## Inputs

- **VIN**: 17 characters, letters and digits, never I, O, or Q. Remove spaces and dashes and
  uppercase it without asking. If it's the wrong length or contains I, O, or Q, ask the user to
  check it rather than calling the tool.
- **Listings ranges**: `year`, `price`, and `miles` take one value or a `min-max` range, such as
  `2019-2022` or `15000-30000`. `state` is a two-letter code. For "near me" searches, pass a
  5-digit `zip`, and `distance` in miles if the user gives one (50 by default). `limit` is 10
  by default and 40 at most. Use `page` for more.
- **Model names**: use the manufacturer's spelling, such as `CX-5`, `F-150`, `RAV4`, `Model 3`.
  If a listings search comes back empty, try the corrected spelling once and tell the user.
- **Interest rates**: `auto_apr` needs the VIN, a ZIP code, and a credit score. It reads the
  year, make, and model from the VIN, so no decode call is needed first.
- **Payments, taxes and fees**: `auto_payments` and `auto_taxes` need the VIN, a price, and a
  ZIP code. The tools refuse to run without them.
- **Money inputs**: ask the user for credit score, ZIP code, price, down payment, and trade-in
  rather than inventing them. Send only what the tool needs.
- **License plates**: look up only plates the user gives you, one at a time, for a reason the
  user states. Never run plate lookups in bulk.

## Answer well

- For one vehicle, lead with year, make, model, and trim, then the facts the user asked for.
- For listings, show a short table: year, make, model, trim, price, mileage, location, dealer.
  Summarize instead of pasting raw JSON.
- Payments, interest rates, taxes, and cost of ownership are estimates. Say so, and don't
  present them as a loan offer or a final price.
- For "tell me about this car", call `auto_decode` first, then only the other VIN tools the
  user's question needs, in parallel. `fetch` makes six calls at once, so use it when the user
  wants the full picture, not for one fact.

## When a tool returns an error

- **Plan errors**: the tool needs a higher plan. Tell the user which plan includes it (see the
  table above) and that plans are at https://www.auto.dev/pricing, then answer with the tools
  their plan covers. Don't retry the same call.
- **Sign-in errors**: ask the user to reconnect the Auto.dev connector, then try again.
- **Invalid input**: fix the input the error names, or ask the user for it, then try once more.
- **No results**: say so plainly and suggest a wider filter, such as a larger price range or no
  state filter.
