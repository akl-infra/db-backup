# akldb backup

A nightly, git-committed copy of the akldb layout database, taken from the
public API (`https://api.akldb.org/v1/dump/latest.json`). Each night the
workflow downloads the dump the API names, verifies its sha256, and commits
the decompressed, key-sorted JSON as `dump.json` together with a small
`manifest.json` (date, sequence number, layout count). Unchanged nights
commit nothing, so `git log` is the change history and any commit is a
restorable snapshot.

Restore: follow the rehost procedure in the akldb repo's README with the
`dump.json` of the commit you want (gzip it first if the tool expects the
`.json.gz` the API serves).

Run by hand: Actions → backup → Run workflow.
