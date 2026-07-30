# Lab 4 — Conflict Resolution

**Cognizant Digital Nurture — Git-T03-HOL_002** (Prerequisite: Git-T03-HOL_001)

## Objective
Resolve a conflict that arises when `master` and a branch both modify the same file.

---

**1. Verify master is in a clean state**
```bash
$ git status
On branch master
nothing to commit, working tree clean
```

**2. Create branch "GitWork" and add `hello.xml`**
```bash
$ git checkout -b GitWork
Switched to a new branch 'GitWork'
$ cat > hello.xml << 'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<greeting>
    <message>Hello from GitWork branch</message>
</greeting>
EOF
$ git add hello.xml
$ git commit -m "Add hello.xml on GitWork branch"
[GitWork 1a1aef9] Add hello.xml on GitWork branch
```

**3. Update `hello.xml` content and observe status**
```bash
# edit hello.xml — change <message>, add <author> tag
$ git status
On branch GitWork
Changes not staged for commit:
        modified:   hello.xml
```

**4. Commit the change on the branch**
```bash
$ git add hello.xml
$ git commit -m "Update hello.xml content on GitWork branch"
[GitWork 6a6b465] Update hello.xml content on GitWork branch
 1 file changed, 2 insertions(+), 1 deletion(-)
```

**5. Switch to master**
```bash
$ git checkout master
Switched to branch 'master'
```

**6. Add `hello.xml` to master with different content**
```bash
$ cat > hello.xml << 'EOF'
<?xml version="1.0" encoding="UTF-8"?>
<greeting>
    <message>Hello from master branch</message>
    <version>1.0</version>
</greeting>
EOF
```

**7. Commit the change to master**
```bash
$ git add hello.xml
$ git commit -m "Add hello.xml on master with different content"
[master af223bf] Add hello.xml on master with different content
```

**8. Observe the log across all branches**
```bash
$ git log --oneline --graph --decorate --all
* af223bf (HEAD -> master) Add hello.xml on master with different content
| * 6a6b465 (GitWork) Update hello.xml content on GitWork branch
| * 1a1aef9 Add hello.xml on GitWork branch
|/
* 6c59f5b Add feature.txt on GitNewBranch
* fc51d24 Add .gitignore to exclude .log files and log folder
* fbe18ba (origin/master) Initial commit: added welcome.txt
```

**9. Check differences with `git diff`**
```bash
$ git diff master GitWork -- hello.xml
-    <message>Hello from master branch</message>
-    <version>1.0</version>
+    <message>Hello from GitWork branch - updated content</message>
+    <author>Dhruv</author>
```

**10. Use a visual merge tool to compare**
> P4Merge (Windows GUI) specified in the lab for a 3-pane visual comparison. `git diff` (step 9) and the conflict markers (step 12) serve the same purpose on Linux.

**11. Merge the branch into master**
```bash
$ git merge GitWork -m "Merge GitWork into master"
Auto-merging hello.xml
CONFLICT (add/add): Merge conflict in hello.xml
Automatic merge failed; fix conflicts and then commit the result.
```

**12. Observe the Git conflict markup**
```bash
$ cat hello.xml
<?xml version="1.0" encoding="UTF-8"?>
<greeting>
<<<<<<< HEAD
    <message>Hello from master branch</message>
    <version>1.0</version>
=======
    <message>Hello from GitWork branch - updated content</message>
    <author>Priyanshu</author>
>>>>>>> GitWork
</greeting>
```

**13. Use a 3-way merge to resolve the conflict**

Combine both sides and remove the conflict markers:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<greeting>
    <message>Hello from GitWork branch - updated content</message>
    <version>1.0</version>
    <author>Dhruv</author>
</greeting>
```

**14. Commit the resolved changes**
```bash
$ git add hello.xml
$ git commit -m "Resolve merge conflict in hello.xml between master and GitWork"
[master 12faf67] Resolve merge conflict in hello.xml between master and GitWork
```

**15. Observe status and add a backup file to `.gitignore`**
```bash
$ echo "backup of hello.xml before conflict resolution" > hello.xml.orig
$ git status
On branch master
Untracked files:
        hello.xml.orig
$ echo "*.orig" >> .gitignore
```

**16. Commit the `.gitignore` change**
```bash
$ git add .gitignore
$ git commit -m "Update .gitignore to exclude .orig backup files"
[master 726aef8] Update .gitignore to exclude .orig backup files
```

**17. List all available branches**
```bash
$ git branch -a
  GitWork
* master
  remotes/origin/master
```

**18. Delete the merged branch**
```bash
$ git branch -d GitWork
Deleted branch GitWork (was 6a6b465).
```

**19. Observe the final log**
```bash
$ git log --oneline --graph --decorate
* 726aef8 (HEAD -> master) Update .gitignore to exclude .orig backup files
*   12faf67 Resolve merge conflict in hello.xml between master and GitWork
|\
| * 6a6b465 Update hello.xml content on GitWork branch
| * 1a1aef9 Add hello.xml on GitWork branch
* | af223bf Add hello.xml on master with different content
|/
* 6c59f5b Add feature.txt on GitNewBranch
* fc51d24 Add .gitignore to exclude .log files and log folder
* fbe18ba (origin/master) Initial commit: added welcome.txt
```

## Outcome
A genuine `add/add` conflict in `hello.xml` was created, resolved via a manual 3-way merge preserving both branches' intent, and committed — with the merge commit `12faf67` clearly visible tying the diverged history back together.
