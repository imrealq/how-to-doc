# MongoDB

## 1. Change history

| Date       | Change                                                                                               | Why                                                            |
| ---------- | ---------------------------------------------------------------------------------------------------- | -------------------------------------------------------------- |
| 2026-08-19 | Replaced `{ new: true }` (deprecated) with `{ returnDocument: 'after' }` in every `findOneAndUpdate` | Mongoose warns the old option will be removed                  |
| 2026-08-12 | Added `checkOverload` — logs connection count + memory every 5s, warns if above `numCores * 5`       | Needed manual connection-load monitoring, no external tool yet |
| 2026-08-11 | Created `init.mongodb.js` (singleton), `maxPoolSize: 50`                                             | The primary connection, shared across the whole system         |

## 2. What it's for

The primary data store — holds every business entity (Shop, Product,
Cart, Order...). See the full relationship diagram at
[database/SCHEMA.md](../database/SCHEMA.md).

## 3. Operational notes

- The connection is a **singleton** (`Database.getInstance()`) — one
  connection pool for the whole app, `maxPoolSize: 50`.
- No retry/backoff on connection failure at startup — errors are just
  logged to console (`catch(err) => console.log(...)`), the app keeps
  running even if Mongo isn't ready (any request touching the DB will
  time out individually).
- `checkOverload` only logs a warning, it doesn't disconnect or reject
  requests when over the threshold — it's observational, not an active
  protection mechanism.

## 4. Links and references

- `src/dbs/init.mongodb.js`
- `src/configs/config.mongodb.js`
- `src/helpers/check.connection.js`

**Used by:** every business domain (Access, Product, Inventory,
Discount, Cart, Order) — through each entity's Mongoose model.
