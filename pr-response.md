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
**What I did:** Created tests/test_watchlist.py with test_add_to_watchlist_nonexistent_film_raises, modeled directly on test_add_to_collection_nonexistent_film_raises from test_collection.py — same fixture structure (app, sample_user, sample_film) and same assertion pattern (pytest.raises(FilmNotFoundError) with a fake UUID).
**How I verified:** Ran `pytest tests/test_watchlist.py -v` (passed), then the full suite `pytest tests/ -v` — all 5 tests pass, no regressions.

## Comment 4 — Default visibility
**My position:** Watchlists should default to private (public=False), not public.
**Reasoning:** Even though CineLog is a community film-tracking app, I don't think users should have to share their watchlist by default. A watchlist is more personal than a watched list since it reflects movies someone plans to watch, which they may not be ready to share publicly. Making it private by default lets users choose to share when they're comfortable instead of accidentally exposing their interests.
**Tradeoff acknowledged:** Fewer public watchlists means less content for discovery and recommendations. However, I think that's a better tradeoff than surprising users by making their watchlist visible without them realizing it. Users who want to participate in the social aspect of the app can still easily change the visibility to public, while users who value privacy don't have to opt out first. I could also see a more flexible system in the future (private, followers-only, public), but with the current boolean design, defaulting to private is the safer and more user-friendly choice.

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