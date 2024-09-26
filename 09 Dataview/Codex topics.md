---
tags:
  - moc
  - codex
---
# Codex Topics
## General

```dataview
LIST
FROM #codex and ("01 Fleeting" or "02 Literature" or "03 Permanent" or "05 Projects/Codex")
```

## Tasks

```dataview
TASK
WHERE !completed and contains(tags, "#task/codex")
GROUP BY file.link
SORT rows.file.ctime ASC
```

```dataview
LIST
FROM #task/codex and ("01 Fleeting" or "02 Literature" or "03 Permanent")
```

## Issues

```dataview
LIST
FROM #issue/codex
GROUP BY file.link
SORT rows.file.ctime ASC
```

