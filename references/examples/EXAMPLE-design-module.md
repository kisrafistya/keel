# Worked example: design module

A filled design-module doc for one subsystem of the sample project **Snip** (see `EXAMPLE-decisions.md`): the **Redirect + Analytics** engine. This is an imitation target for `doc-design-module.md`: note the explicit scope, the contract surface in prose, and how the invariants from the DECISIONS doc are restated and enforced at the seam. Illustrative, not a real product.

---

## 1. Purpose & scope

Resolve a short code to its original URL and serve the redirect, then emit a single privacy-safe click event. **In scope:** code lookup, the redirect response, the async click event. **Out of scope:** the create/edit API (separate module), the dashboard that reads analytics (separate module), and authentication (admin-token middleware sits above this).

## 2. The model

Read-through cache in front of the store: a code is looked up in an in-memory map; on a miss it's fetched from the DB and cached. The redirect is served immediately. The click event is handed to a buffered channel and written by a background worker - the redirect path never waits for it (DECISIONS invariant).

## 3. Core mechanics

- **Lookup:** `code -> URL`. Cache hit serves directly; cache miss reads the DB, populates the cache, then serves. A code that doesn't exist returns 404.
- **Redirect:** respond `302` to the resolved URL (DECISIONS resolved-item: 302, not 301).
- **Click event:** construct a `ClickEvent`, derive country + device-class in-process, discard the raw IP and UA, push the event to the channel, and return. If the channel is full, drop the event and increment a dropped-events counter - never block.

## 4. Public interface / contract surface

- **Inbound:** `GET /{code}` -> `302 Location: <url>` on hit, `404` on miss. No body on the hot path.
- **Emitted shape:** `ClickEvent { code: string, ts: timestamp, country: string|null, device_class: "mobile"|"desktop"|"bot"|"unknown" }`. No field carries per-person data.
- **Consumes:** the store's `get(code) -> URL | NotFound`.

## 5. Invariants

- The redirect path **never** awaits the analytics write (fire-and-forget; drop under backpressure).
- `ClickEvent` **never** contains PII - the type makes it unrepresentable; raw IP/UA are local variables that never leave the function.
- A `404` (code not found) and an analytics failure are independent: an analytics outage **never** turns a valid redirect into a 5xx.

## 6. Dependencies

- **Provider (upstream):** the store module - `get(code)`. This module is a pure consumer of it; it never writes URLs.
- **Consumer (downstream):** the analytics sink reads `ClickEvent`s off the channel. The seam is the `ClickEvent` shape above, one direction, no back-edge into the redirect path.

## 7. Risks & edge cases

- **Cache stampede on a viral link:** many concurrent misses for the same cold code. Mitigation: single-flight the DB read per code.
- **Code not found:** return 404, do not emit a `ClickEvent`.
- **Clock skew on `ts`:** stamp at event creation in the redirect process, not at write time, so analytics reflect click time.
- **Channel full (backpressure):** drop + count, never block the redirect.

## 8. Phased implementation plan

- **P0:** redirect straight from the DB, no cache, no analytics. Correct first.
- **P1:** add the read-through cache; hit the p99 < 10ms target.
- **P2:** add the fire-and-forget click event + background writer.
- **P3:** add country + device-class enrichment (in-process, raw inputs discarded).

## 9. Sources

- Latency target (p99 redirect < 10ms) from DECISIONS #4.
- Privacy invariants from DECISIONS #3 and its Invariants section.
