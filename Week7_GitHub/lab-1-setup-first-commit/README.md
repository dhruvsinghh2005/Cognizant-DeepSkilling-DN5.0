# Lab 1 — Git Setup, Configuration & First Commit

**Cognizant Digital Nurture — Git-T03-HOL_001(a)**

## Objective
Get familiar with `git init`, `git status`, `git add`, `git commit`, `git push`, and `git pull`. Configure Git, set a default editor, and add the first file to a repository.

## Environment note
Completed in a Linux shell. GitLab was simulated with a local bare repository acting as `origin`. On Windows Git Bash, notepad++ is integrated as the default editor via `git config --global core.editor "notepad++.exe -multiinst -notabbar -nosession -noPlugin"` — functionally identical to the `nano` setup shown below.

---

## Step 1: Configure Git

**1. Verify Git client is installed**
```bash
$ git --version
git version 2.43.0
```

**2. Configure user-level identity**
```bash
$ git config --global user.name "Dhruv"
$ git config --global user.email "2306198@kiit.ac.in"
```

**3. Verify the configuration**
```bash
$ git config --global --list
user.name=Dhruv
user.email=2306198@kiit.ac.in
```

## Step 2: Configure default editor

**4. Set a default editor**
```bash
$ git config --global core.editor "nano"
$ git config --global core.editor
nano
```

## Step 3: Add a file to the source code repository

**5. Create and initialize the "GitDemo" project**
```bash
$ mkdir GitDemo && cd GitDemo
$ git init
Initialized empty Git repository in /home/claude/GitDemo/.git/
```

**6. Verify initialization**
```bash
$ ls -la
drwxr-xr-x 3 root root 4096 .
drwxr-xr-x 8 root root 4096 ..
drwxr-xr-x 7 root root 4096 .git
```

**7. Create welcome.txt with content**
```bash
$ echo "Welcome to GitDemo repository" > welcome.txt
```

**8. Verify file creation**
```bash
$ ls -la
-rw-r--r-- 1 root root 30 welcome.txt
```

**9. Verify content**
```bash
$ cat welcome.txt
Welcome to GitDemo repository
```

**10. Check status of working directory**
```bash
$ git status
On branch master
No commits yet
Untracked files:
  (use "git add <file>..." to include in what will be committed)
        welcome.txt
```

**11. Stage the file**
```bash
$ git add welcome.txt
```

**12. Commit with a multi-line message**
```bash
$ git commit -m "Initial commit: added welcome.txt

Added welcome.txt file to GitDemo repository as part
of Git-T03-HOL_001 hands-on lab exercise."

[master (root-commit) fbe18ba] Initial commit: added welcome.txt
 1 file changed, 1 insertion(+)
 create mode 100644 welcome.txt
```

**13. Confirm working directory and local repo match**
```bash
$ git status
On branch master
nothing to commit, working tree clean
```

**14. Create remote repository and link as origin**
```bash
$ git init --bare remote-GitDemo.git
$ git remote add origin /home/claude/remote-GitDemo.git
$ git remote -v
origin  /home/claude/remote-GitDemo.git (fetch)
origin  /home/claude/remote-GitDemo.git (push)
```

**15. Pull the remote repository**
```bash
$ git pull origin master
fatal: couldn't find remote ref master
```
> Expected — the remote is brand new and empty, so there's nothing to pull yet.

**16. Push local to remote**
```bash
$ git push origin master
To /home/claude/remote-GitDemo.git
 * [new branch]      master -> master
```

## Outcome
`GitDemo` repository initialized, `welcome.txt` created and committed, and the local repository successfully pushed to the remote for the first time.
