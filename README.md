# PP5

## Goal

In this exercise you will:

* Use Git **locally** on your own machine: create branches, make commits, and merge them back.
* Set up and interact with a **bare** Git repository on an SSH‐accessible server (e.g. **vorlesungsserver**, or any machine you have SSH access to).
* Push and pull to/from **GitHub** and the **THGA GitLab** server.
* Practice **forking** an existing repo, making changes, and submitting a **Pull Request** (on GitHub) or **Merge Request** (on GitLab).

**Important:** Start a stopwatch when you begin and work uninterruptedly for **90 minutes**. Once time is up, stop immediately and document exactly where you had to pause.

---

## Workflow

1. **Fork** this repository
2. **Modify & commit** your solution
3. **Submit your link for Review**

---

## Prerequisites

* Several starter repos are available here:
  [https://github.com/orgs/STEMgraph/repositories?q=Git%3A](https://github.com/orgs/STEMgraph/repositories?q=Git%3A)
* Ensure you have **SSH access** to a remote server (e.g., “vorlesungsserver”).
* Throughout, consult Git’s built-in man-pages (`git help <command>`) for explanations and options.

---

## Tasks

### Task 1: Local Git – Branching & Merging

1. Create a new directory in your home directory and initialize a repository in it. 
2. In one of your cloned repos, initialize a new branch called `feature-1`.
3. On `feature-1`, create a file `feature.txt` containing a short description of what you’re doing.
4. Commit your changes, then switch back to `master` (or `main`), and merge `feature-1` into your `master`.
5. Resolve any merge conflicts (if they arise) by hand, then commit the merge. 

**Your Commands & Output**

```bash
# Paste here the sequence of git commands you ran
# and the relevant terminal output (e.g., branch listing, merge messages)
```
eugen@User-PC:~$ mkdir pp5eugen
eugen@User-PC:~$ cd pp5eugen
eugen@User-PC:~/pp5eugen$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/eugen/pp5eugen/.git/
eugen@User-PC:~/pp5eugen$ git checkout -b feature-1
Switched to a new branch 'feature-1'
eugen@User-PC:~/pp5eugen$ echo "Das ist Paraktikum pp5.Aufgabe 1" > feature.txt
eugen@User-PC:~/pp5eugen$ ls
feature.txt
eugen@User-PC:~/pp5eugen$ git status
On branch feature-1

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        feature.txt

nothing added to commit but untracked files present (use "git add" to track)
eugen@User-PC:~/pp5eugen$ git add feature.txt
eugen@User-PC:~/pp5eugen$ git status
On branch feature-1

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   feature.txt

eugen@User-PC:~/pp5eugen$ git commit -m "Das Datei feature.txt wurde eingefügt"
[feature-1 (root-commit) 4a773f9] Das Datei feature.txt wurde eingefügt
 1 file changed, 1 insertion(+)
 create mode 100644 feature.txt
eugen@User-PC:~/pp5eugen$ git checkout master
error: pathspec 'master' did not match any file(s) known to git
eugen@User-PC:~/pp5eugen$ git branch --list
* feature-1
eugen@User-PC:~/pp5eugen$ git merge feature-1
Already up to date.
eugen@User-PC:~/pp5eugen$ git log --all
commit 4a773f993c27babb7f51befeae16f77774b82d5e (HEAD -> feature-1)
Author: eugen.risling@stud.thga.de <Your Email>
Date:   Wed May 21 20:36:04 2025 +0200

    Das Datei feature.txt wurde eingefügt
---

### Task 2: Bare Repository on an SSH Server

1. On your SSH server (e.g., “vorlesungsserver”), create a **bare** repo at `~/repos/myproject.git`:

   ```bash
   ssh youruser@vorlesungsserver \
     "mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare"
   ```
2. On your local machine, add it as a remote named `origin-ssh`:

   ```bash
   git remote add origin-ssh youruser@vorlesungsserver:~/repos/myproject.git
   ```
3. Push your `master` branch to `origin-ssh`, then clone it into a fresh directory to verify.

**Your Commands & Output**

```bash
# Paste here the push & clone commands and outputs
```
eugen@User-PC:~/pp5eugen$ ssh user11@128.140.85.215
user11@128.140.85.215's password:
Linux vorlesung 6.1.0-21-amd64 #1 SMP PREEMPT_DYNAMIC Debian 6.1.90-1 (2024-05-03) x86_64

The programs included with the Debian GNU/Linux system are free software;
the exact distribution terms for each program are described in the
individual files in /usr/share/doc/*/copyright.

Debian GNU/Linux comes with ABSOLUTELY NO WARRANTY, to the extent
permitted by applicable law.
Last login: Sat May 17 14:16:16 2025 from 91.51.164.3
user11@vorlesung:~$ mkdir -p ~/repos/myproject.git && cd ~/repos/myproject.git && git init --bare
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/user11/repos/myproject.git/
user11@vorlesung:~/repos/myproject.git$ ls
branches  config  description  HEAD  hooks  info  objects  refs
user11@vorlesung:~/repos/myproject.git$ exit
logout
Connection to 128.140.85.215 closed.
eugen@User-PC:~/pp5eugen$ git remote add origin-ssh user11@128.140.85.215:~/repos/myproject.git
eugen@User-PC:~/pp5eugen$ git push origin-ssh master
error: src refspec master does not match any
error: failed to push some refs to '128.140.85.215:~/repos/myproject.git'
eugen@User-PC:~/pp5eugen$ git push origin-ssh feature-1
user11@128.140.85.215's password:
Enumerating objects: 3, done.
Counting objects: 100% (3/3), done.
Writing objects: 100% (3/3), 276 bytes | 138.00 KiB/s, done.
Total 3 (delta 0), reused 0 (delta 0), pack-reused 0
To 128.140.85.215:~/repos/myproject.git
 * [new branch]      feature-1 -> feature-1
eugen@User-PC:~/pp5eugen$ git clone ~/pp5eugen/
Cloning into 'pp5eugen'...
done.
eugen@User-PC:~/pp5eugen$ ls -la
total 0
drwxr-xr-x 1 eugen eugen 512 May 21 21:15 .
drwxr-x--- 1 eugen eugen 512 May 21 20:43 ..
drwxr-xr-x 1 eugen eugen 512 May 21 21:02 .git
-rw-r--r-- 1 eugen eugen  33 May 21 20:28 feature.txt
drwxr-xr-x 1 eugen eugen 512 May 21 21:15 pp5eugen
---

### Task 3: GitHub & THGA GitLab

1. On [GitHub](github.com), create a new empty repo under your account named `myproject-gh`.
2. On [THGA GitLab](gitlab.thga.de), create a new project named `myproject-gl`.
3. In your local repository, add these as remotes:

   ```bash
   git remote add github  git@github.com:YOUR_USERNAME/myproject-gh.git
   git remote add gitlab  git@gitlab.thga.de:YOUR_USERNAME/myproject-gl.git
   ```
4. Push your `master` branch to both `github` and `gitlab` remotes.

> Hint: You are just adding two more bare-remotes to your already existing repository!

**Your Commands & Output**

```bash
# Paste here the remote‐adding & push outputs
```
eugen@User-PC:~$ mkdir myproject-gh
eugen@User-PC:~$ cd myproject-gh
eugen@User-PC:~/myproject-gh$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/eugen/myproject-gh/.git/
eugen@User-PC:~/myproject-gh$ git remote add github  git@github.com:Eugen888-oss/myproject-gh.git
eugen@User-PC:~/myproject-gh$ touch "pp5 task3" > githubtext.txt
eugen@User-PC:~/myproject-gh$ git add githubtext.txt
eugen@User-PC:~/myproject-gh$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   githubtext.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        pp5 task3

eugen@User-PC:~/myproject-gh$ cd ..
eugen@User-PC:~$ mkdir myproject-gl
eugen@User-PC:~$ cd myproject-gl
eugen@User-PC:~/myproject-gl$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/eugen/myproject-gl/.git/
eugen@User-PC:~/myproject-gl$ git remote add gitlab  git@gitlab.thga.de:Eugen888-oss/myproject-gl.git
eugen@User-PC:~/myproject-gl$ touch "pp5 task3" > githubtext.txt
eugen@User-PC:~/myproject-gl$ git status
On branch master

No commits yet

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        githubtext.txt
        pp5 task3

nothing added to commit but untracked files present (use "git add" to track)
eugen@User-PC:~/myproject-gl$ git add githubtext.txt
eugen@User-PC:~/myproject-gl$ git status
On branch master

No commits yet

Changes to be committed:
  (use "git rm --cached <file>..." to unstage)
        new file:   githubtext.txt

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        pp5 task3
---

### Task 4: Fork, Modify, and Pull/Merge Request

1. On GitHub, **fork** one of the repos from the STEMgraph org.
2. Clone your fork locally, create a branch `pp5-changes`, and make a small change (e.g., update the README).
3. Commit and push `pp5-changes` to **your** fork, then open a **Pull Request** against the original repo.
4. Repeat on THGA GitLab: fork another students repository, clone, branch, change, push, and open a **Merge Request**. If your peers opened a merge request to your repository, review and merge or decline it!

**Your PR/MR Links & Descriptions**

* GitHub PR: *paste URL and a one-sentence summary*
* GitLab MR: *paste URL and a one-sentence summary*

---

**Remember:** Stop working after **90 minutes** and record where you stopped!
