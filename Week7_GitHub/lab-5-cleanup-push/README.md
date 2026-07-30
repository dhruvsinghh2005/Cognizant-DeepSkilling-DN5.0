# Lab 5 — Clean Up and Push Back to Remote

**Cognizant Digital Nurture — Git-T03-HOL_003** (Prerequisite: Git-T03-HOL_002)

## Objective
Clean up and push all pending local changes back to the remote repository.

---

**1. Verify master is in a clean state**
```bash
$ git status
On branch master
nothing to commit, working tree clean
```

**2. List all available branches**
```bash
$ git branch -a
* master
  remotes/origin/master
```

**3. Pull the remote repository into master**
```bash
$ git pull origin master
Already up to date.
```
> Local `master` is ahead of the remote (which only had the Lab 1 commit) — nothing new upstream to pull.

**4. Push all pending changes to the remote**
```bash
$ git push origin master
To /home/claude/remote-GitDemo.git
   fbe18ba..726aef8  master -> master
```

**5. Verify the changes are reflected on the remote**
```bash
$ git clone remote-GitDemo.git verify-clone
$ cd verify-clone && ls -la
welcome.txt  .gitignore  feature.txt  hello.xml

$ git log --oneline --graph --decorate --all
* 726aef8 (HEAD -> master, origin/master, origin/HEAD) Update .gitignore to exclude .orig backup files
*   12faf67 Resolve merge conflict in hello.xml between master and GitWork
| * 6a6b465 Update hello.xml content on GitWork branch
| * 1a1aef9 Add hello.xml on GitWork branch
* | af223bf Add hello.xml on master with different content
* 6c59f5b Add feature.txt on GitNewBranch
* fc51d24 Add .gitignore to exclude .log files and log folder
* fbe18ba Initial commit: added welcome.txt
```
> A clean clone from the remote confirms all four tracked files and the full commit/merge history from Labs 1–4 are present — the push succeeded.

## Outcome
All pending commits from Labs 1 through 4 are synced to the remote repository and verified via an independent clone.
