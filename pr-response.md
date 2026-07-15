# PR Response Doc — CineLog Watchlist Feature

## AI Usage
<!-- Fill in at the end — how you used AI tools during this project -->

## Comment 1 — Rename
**What I did:** Used Ctrl + F to find all occurences of save_to_watchlist() and changed them to add_to_watchlist. 
**How I verified:** Tracked down the add to watchlist route and manually verified that each point on trying to add a film to watchlist uses add_to_watchlist(). So verified from add_film function on routes/watchlist to watchlist_service. Also when importing watchlist service method, the import showed now add_to_watchlist().

## Comment 2 — Deduplication
**What I did:**
**How I verified:**

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