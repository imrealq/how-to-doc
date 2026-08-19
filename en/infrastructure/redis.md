# Redis

## 1. Change history

| Date       | Change                                                                    | Why                                                                        |
| ---------- | ------------------------------------------------------------------------- | -------------------------------------------------------------------------- |
| 2026-08-19 | Added `redisLock.js` (distributed lock, `SET NX PX` + Lua script release) | Needed a shared lock across multiple server instances when deducting stock |
| 2026-08-19 | Created `init.redis.js` (singleton, `ioredis`)                            | The first Redis connection in the system                                   |

## 2. What it's for

Distributed lock for stock-deduction operations — blocks 2 concurrent
requests from deducting stock for the same product when multiple server
instances run in parallel. See [inventory.md](../api/inventory.md).

## 3. Operational notes

- The connection is a **singleton** (`RedisDatabase.getInstance()`), no
  manual retry — relies on `ioredis`'s default reconnect behavior.
- Connection errors are only logged to console
  (`client.on('error', ...)`), there's no circuit breaker or fallback
  when Redis is unavailable — if Redis goes down, `acquireLock` will
  always fail (returns `null` after exhausting retries), blocking every
  stock-deduction operation.
- The lock has a 10s TTL — if the process holding the lock crashes
  before releasing it, the lock auto-expires after 10s, it doesn't hang
  forever.

## 4. Links and references

- `src/dbs/init.redis.js`
- `src/configs/config.redis.js`
- `src/helpers/redisLock.js`

**Used by:**

- `Inventory` — `acquireLock`/`releaseLock` inside `reservationInventory`
