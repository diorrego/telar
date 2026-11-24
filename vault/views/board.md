# Board

Dynamic views (Dataview plugin in Obsidian). The state lives in each note's frontmatter; this page only filters. Status values are defined in [`projects/CLAUDE.md`](../projects/CLAUDE.md), [`qa/CLAUDE.md`](../qa/CLAUDE.md) and [`CLAUDE.md`](../CLAUDE.md).

Without Obsidian, from the vault root:

```sh
grep -l "^status: proposed" projects/*/*/PLAN.md                    # plans waiting for a go (change the status as needed)
grep -lE "^status: (open|triaged|fixing|fixed)" qa/findings/*.md    # findings not closed
grep -l "^status: logged" qa/corrections/*.md                       # corrections not yet encoded
grep -l "^status: proposed" decisions/*.md                          # decisions waiting for Diego
```

## Plans waiting for a go

```dataview
TABLE origin, updated
FROM "projects"
WHERE file.name = "PLAN" AND status = "proposed"
SORT updated ASC
```

## Active plans

```dataview
TABLE origin, updated
FROM "projects"
WHERE file.name = "PLAN" AND status = "active" AND !superseded_by
SORT updated DESC
```

## Shipped

```dataview
TABLE updated
FROM "projects"
WHERE file.name = "PLAN" AND status = "shipped" AND !superseded_by
SORT updated DESC
```

## Dropped

```dataview
TABLE updated
FROM "projects"
WHERE file.name = "PLAN" AND status = "dropped"
SORT updated DESC
```

## Open findings

```dataview
TABLE severity, area, status, found
FROM "qa/findings"
WHERE status != "verified" AND status != "wont-fix"
SORT choice(severity = "critical", 0, choice(severity = "high", 1, choice(severity = "medium", 2, 3))) ASC
```

## Corrections not yet encoded

```dataview
TABLE occurrences, date, harness, model
FROM "qa/corrections"
WHERE status = "logged"
SORT occurrences DESC
```

## Decisions waiting for Diego

```dataview
TABLE date, decided_by
FROM "decisions"
WHERE status = "proposed"
SORT date ASC
```
