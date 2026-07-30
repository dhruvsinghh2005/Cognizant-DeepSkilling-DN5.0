# Lab 3 — Branching and Merging

**Cognizant Digital Nurture — Git-T03-HOL_001(c)**

## Objective
Construct a branch, make changes on it, and merge it back into `master` (trunk).

---

## Branching

**1. Create a new branch "GitNewBranch"**
```bash
$ git branch GitNewBranch
```

**2. List all local and remote branches** (`*` marks the current branch)
```bash
$ git branch -a
  GitNewBranch
* master
  remotes/origin/master
```

**3. Switch to the branch and add a file with content**
```bash
$ git checkout GitNewBranch
Switched to branch 'GitNewBranch'
$ echo "This file was added on GitNewBranch" > feature.txt
```

**4. Commit the change on the branch**
```bash
$ git add feature.txt
$ git commit -m "Add feature.txt on GitNewBranch"
[GitNewBranch 6c59f5b] Add feature.txt on GitNewBranch
 1 file changed, 1 insertion(+)
```

**5. Check status**
```bash
$ git status
On branch GitNewBranch
nothing to commit, working tree clean
```

## Merging

**1. Switch to master**
```bash
$ git checkout master
Switched to branch 'master'
```

**2. List CLI differences between master and the branch**
```bash
$ git diff master GitNewBranch
diff --git a/feature.txt b/feature.txt
new file mode 100644
--- /dev/null
+++ b/feature.txt
@@ -0,0 +1 @@
+This file was added on GitNewBranch
```

**3. List visual differences using a merge tool**
```bash
$ git difftool master GitNewBranch
```
> The lab specifies **P4Merge** (Windows GUI) for a side-by-side visual diff. `git diff` above serves the equivalent purpose; `git difftool` can be configured with any GUI diff tool (P4Merge, meld, vimdiff).

**4. Merge the branch into the trunk**
```bash
$ git merge GitNewBranch -m "Merge GitNewBranch into master"
Updating fc51d24..6c59f5b
Fast-forward (no commit created; -m option ignored)
 feature.txt | 1 +
 1 file changed, 1 insertion(+)
```

**5. Observe the log after merging**
```bash
$ git log --oneline --graph --decorate
* 6c59f5b (HEAD -> master, GitNewBranch) Add feature.txt on GitNewBranch
* fc51d24 Add .gitignore to exclude .log files and log folder
* fbe18ba (origin/master) Initial commit: added welcome.txt
```

**6. Delete the branch after merging and observe status**
```bash
$ git branch -d GitNewBranch
Deleted branch GitNewBranch (was 6c59f5b).
$ git branch -a
* master
  remotes/origin/master
```

## Outcome
`GitNewBranch` created, modified, fast-forward merged into `master`, and cleaned up after the merge.
