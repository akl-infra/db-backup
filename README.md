# akldb backup

A nightly, git-committed snapshot of the akldb layout database, taken from
the public API (`https://api.akldb.org/v1/dump/latest.json`). Each night the
workflow downloads the dump the API names, verifies its sha256, and commits
the current state as one file per table under `snapshot/`: every table the
dump carries (records, layout formats, likes, authors, comments and comment
likes, WPM and link submissions, admins, bans, clients, import map, meta, and
any table added later). The event log (`events`) and the per-layout revision
history (`layout_revs`) are kept too, as JSON-lines chunks of 2000 rows under
`snapshot/events/` and `snapshot/layout_revs/`, ordered by event sequence; only
the cache (`auth_cache`) is left out. `manifest.json` records the date, sequence number and
layout count. Unchanged nights commit nothing, so `git log` is the change
history and any commit is a point-in-time copy.

Restore: the akldb repo's rehost procedure accepts a dump. Rebuild one from a
snapshot by putting each `snapshot/<table>.json` under its table name and each
chunked table back together, e.g. `cat snapshot/events/*.jsonl | jq -s .`.

Run by hand: Actions → backup → Run workflow.
