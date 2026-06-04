# Worked example: DECISIONS

A filled `DECISIONS` doc for a fictional sample project, **Snip** - a self-hosted URL shortener with privacy-respecting click analytics. This is an imitation target for `doc-decisions.md`: note the product boundary, the numbered locked entries with date + reason, and the invariants. The content is illustrative, not a real product.

---

## Product boundary (read first)

Snip turns long URLs into short codes and shows the owner basic, privacy-respecting click analytics. It is **self-hosted and single-tenant** (one admin, one instance). It is **not** a multi-tenant SaaS, **not** a marketing-attribution suite, and **not** an ad or tracking network. If a request would require storing who clicked, it is out of scope by design.

## Locked

1. **Single self-contained binary + SQLite for storage.** (locked 2026-02-10) - The target user is a developer who wants zero-ops self-hosting; a binary plus one file beats requiring Postgres.
2. **Short codes are base62 of an autoincrement row id, minimum length 5.** (locked 2026-02-10) - Collision-free without a read-before-write, and short. Padding to 5 keeps early codes from looking sequential.
3. **Analytics store NO PII.** (locked 2026-02-11) - No IP, no user-agent string, no cookies. Country and a coarse device-class are derived in-process and the raw inputs are discarded immediately. This is the product's wedge and an invariant, not a setting. See Invariants.
4. **Redirects are served from an in-memory cache; the DB is the source of truth.** (locked 2026-02-12) - Target is p99 redirect latency under 10ms; a cold cache falls back to the DB.
5. **No user accounts in v1; a single admin token guards the create/dashboard surface.** (locked 2026-02-12) - Matches the single-tenant boundary; accounts are scope creep until multi-tenant is on the table.
6. **A redirect never blocks on the analytics write.** (locked 2026-02-13) - The click event is fire-and-forget; an analytics failure must never delay or break a redirect. See Invariants. Supersedes the early synchronous-logging sketch.

## Resolved

- **Custom domains?** - Resolved: out of v1, tracked below. The base-domain case ships first; custom domains add DNS + cert handling that doesn't gate the core value.
- **301 vs 302 redirect?** - Resolved: 302 (temporary), so the owner can edit or disable a link later and clients don't cache it permanently.

## Still tracked

1. **Rate-limiting strategy for the create endpoint** - needed before any public exposure; unblocks on picking a limiter (in-process token bucket is the leading candidate).
2. **Bulk import / export** - wanted by power users; unblocks after the create API stabilizes.
3. **Custom domains** - unblocks after v1 ships and there's real demand.

## Invariants

- Analytics **never** store PII. A code path that would persist an IP, a UA string, or any per-person identifier is a bug, not a feature.
- A redirect **never** awaits an analytics write. The analytics sink can be down and redirects must still serve.
- Short codes are **never** reused, even after a link is deleted, so old codes can't silently point somewhere new.
