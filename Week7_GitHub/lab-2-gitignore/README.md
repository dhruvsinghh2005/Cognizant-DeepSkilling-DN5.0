# Lab 2 — .gitignore

**Cognizant Digital Nurture — Git-T03-HOL_001(b)**

## Objective
Implement `.gitignore` to exclude unwanted files and folders — specifically `.log` files and a `log` folder — from being tracked by Git.

---

**1. Create a `.log` file and a `log` folder**
```bash
$ echo "This is an application log entry" > application.log
$ mkdir log
$ echo "debug trace output" > log/debug.txt
```

**2. Check status before ignoring**
```bash
$ git status
On branch master
Untracked files:
        application.log
        log/
```

**3. Create `.gitignore` to exclude `*.log` files and the `log/` folder**
```bash
$ cat > .gitignore << 'EOF'
*.log
log/
EOF
```

**4. Verify git status reflects the ignore rules**
```bash
$ git status
On branch master
Untracked files:
        .gitignore
```
> `application.log` and `log/` no longer appear — only the new `.gitignore` file itself shows as untracked.

**5. Stage and commit `.gitignore`**
```bash
$ git add .gitignore
$ git commit -m "Add .gitignore to exclude .log files and log folder"
[master fc51d24] Add .gitignore to exclude .log files and log folder
 1 file changed, 2 insertions(+)
```

**6. Confirm working directory, local repo, and Git status match (clean)**
```bash
$ git status
On branch master
nothing to commit, working tree clean
```

## Outcome
`.log` files and the `log/` folder are now permanently excluded from tracking, and `.gitignore` itself is version-controlled.
