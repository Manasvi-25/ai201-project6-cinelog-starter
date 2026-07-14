# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
*What I did:** Renamed `save_to_watchlist()` to `add_to_watchlist()` in services/watchlist_service.py to match the project's verb_to_noun convention (consistent with add_to_collection()). Updated the import and call site in routes/watchlist/watchlist.py.
**How I verified:** Searched the project with `Select-String -Recurse -Filter *.py -Pattern "save_to_watchlist"` and confirmed no remaining references. Ran full test suite (pytest tests/ -v) — all 4 existing tests pass.

## Comment 2 — Deduplication
**What I did:** Added an `AlreadyInWatchlistError` exception class and a duplicate check in `add_to_watchlist()`, following the same pattern as `add_to_collection()` in collection_service.py — query for an existing entry with matching user_id/film_id before creating a new one, and raise if found.
**How I verified:** Ran the full test suite (pytest tests/ -v) — all 4 existing tests still pass. (No test yet directly exercises the duplicate case; that's addressed as part of Comment 3's test coverage / can add one as a stretch test.)

## Comment 3 — Missing test
**What I did:**
**How I verified:**

## Comment 4 — Default visibility
**My position:**
**Reasoning:**
**Tradeoff acknowledged:**

## Comment 5 — Sort order
**My position:**
**Reasoning:**
**Engagement with reviewer's point:**

## Comment 6 — Rebase
**What conflicted:**
**How I resolved it:**
**How I verified no conflict remains:**

## PR Description
<!-- Written at the end — feature overview, design decisions, manual testing steps -->