# <Infrastructure component name>

Standard for describing 1 infrastructure component (data store, cache,
queue, external service...). Copy this file when adding a new
component, remove the instructional lines in parentheses.

## 1. Change history

_(Each new row goes at the TOP of the table, don't delete old rows.
Record changes that affect how the system operates — additions,
significant config changes, deprecation — not minor version bumps.)_

| Date       | Change                                      | Why        |
| ---------- | ------------------------------------------- | ---------- |
| YYYY-MM-DD | _(e.g. added a distributed lock for stock)_ | _(reason)_ |

## 2. What it's for

_(1-3 sentences: what role this component plays in the system — don't
describe how it works internally, just what it's used for.)_

...

## 3. Operational notes

_(Only things likely to cause trouble if not known in advance —
timeouts, connection limits, behavior on disconnect. Not
installation/deployment instructions.)_

- ...

## 4. Links and references

_(Related connection/config/helper files — list plainly, no
explanation. Include which domain depends on this component — point to
`docs/en/api/<domain>.md` instead of repeating the flow detail
there.)_

- `src/dbs/init.<name>.js`
- `src/configs/config.<name>.js`

**Used by:**

- `<domain>` — _(what for, when)_
