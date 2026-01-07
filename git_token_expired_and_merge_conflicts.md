## Problem

- Made changes on GitHub WEB interface
- Worked locally → `git push` → ERROR: "Invalid username or token"  
- Token expired (GitHub PATs expire)
- Generated NEW token but local Git still cached OLD expired token
- Web changes existed but local unaware → potential merge conflict risk

## Fix Authentication (New Token)

```
git remote set-url origin https://USERNAME:NEW-TOKEN@github.com/USERNAME/REPO.git
```

## Sync Web Changes (Critical!)

```
git fetch origin                    # Safe: see remote changes
git pull --rebase origin main       # Merge web → local (Linear history)
```

```
BEFORE pull --rebase:
Web:  A---B---C (main)     ← Web commits
Local: A---D---E (your branch)

AFTER pull --rebase:
     A---B---C
            │
            D'---E'  ← commits "replayed" cleanly on top
```

##Push Local Changes

```
git push origin main
```
