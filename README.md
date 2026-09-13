# akldb backup

A nightly, git-committed snapshot of the akldb layout database, taken from
the public API (`https://api.akldb.org/v1/dump/latest.json`). Each night the
workflow downloads the dump the API names, verifies its sha256, and commits
the current state as one file per table under `snapshot/`: `records.json`,
`layout_formats.json`, `likes.json`, `authors.json`, `admins.json`, `bans.json`,
`clients.json`, `import_map.json`, `meta.json`. The
event log, the per-layout revision history and the caches are deliberately
left out -- this is a snapshot of what exists, not material for replaying
how it got there. `manifest.json` records the date, sequence number and
layout count. Unchanged nights commit nothing, so `git log` is the change
history and any commit is a point-in-time copy.

Restore: the akldb repo's rehost procedure accepts a dump; a snapshot is a
dump minus the history sections, so it restores current state only.

Run by hand: Actions → backup → Run workflow.
