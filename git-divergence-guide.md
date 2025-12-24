# Git Divergence Quick Reference

Current state (before):
```
origin/main:  A - R1 - R2 - ... - R12         (12 commits that only remote has)
                              \
local main:                    L1            (1 commit that only you have)
```

**Interpretation**: origin/main and main have diverged — remote has 12 commits, local has 1 commit.

## Option 1: Merge (keep both histories; create a merge commit)

**Command**:
```
git fetch origin
git checkout main
git pull --no-rebase origin main   # or: git merge origin/main
```

**Before**:
```
A - R1 - R2 - ... - R12    (origin/main)
           \
            (shared history)
             \
              L1           (local main)
```

**After**:
```
A - R1 - R2 - ... - R12  \
                         M   <- merge commit (contains both histories)
                        /
                   L1 --
```

**Notes**:
- Safe for shared branches.
- Preserves both sets of commits; creates a new merge commit M.
- If conflicts occur: resolve each file, `git add <file>`, then `git commit`.

## Option 2: Rebase (linear history; rewrite local commit)

**Command**:
```
git fetch origin
git checkout main
git pull --rebase origin main    # or: git rebase origin/main
```

**Before**:
```
A - R1 - R2 - ... - R12    (origin/main)
           \
            L1             (local main)
```

**After**:
```
A - R1 - R2 - ... - R12 - L1'   (L1' is L1 replayed on top of R12)
```

**Notes**:
- Produces a linear history — your local commit is rewritten (new commit id L1').
- Good for tidy history on feature branches; be cautious if L1 was already pushed/shared.
- Conflicts: resolve files, `git add <file>`, then `git rebase --continue`. Abort with `git rebase --abort`.

## Option 3: Force-overwrite remote (discard remote commits; dangerous)

**Command**:
```
git checkout main
git push --force origin main           # !! destructive !!
# Prefer: git push --force-with-lease origin main  (safer alternative)
```

**Before**:
```
A - R1 - R2 - ... - R12    (origin/main)
           \
            L1             (local main)
```

**After** (remote becomes exactly like local):
```
A - L1   (both local main and origin/main now point to L1)
```

**Notes**:
- Destroys the 12 remote commits on origin/main (lost for collaborators unless they have copies).
- Only use if absolutely sure remote commits should be removed.
- Prefer `--force-with-lease` to avoid overwriting newer remote changes.
