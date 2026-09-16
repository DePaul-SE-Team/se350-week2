## Simple Git Exercise: Commits and Branch Merging

### Objective

Practice the basic Git workflow:

1. Check the repository status.
2. Modify a file.
3. Stage the change.
4. Commit the change.
5. Create and use a branch.
6. Merge the branch using a merge commit.
7. Inspect the Git history.

## Part 1: Make Your First Commit

### 1. Check the repository status

From the repository root, run:

```bash
git status
```

Read the output before continuing.

### 2. Create a file

Create a file named `student-info.txt` in the repository root. Add the following information:

```text
Name: Your Name
Favorite programming language: Your Answer
One thing I want to learn: Your Answer
```

Replace the placeholders with your own answers.

### 3. Inspect the change

Run:

```bash
git status
git diff
```

Answer this question:

> Why does `git diff` not display the contents of a completely new, untracked file?

### 4. Stage the file

Run:

```bash
git add student-info.txt
```

Then inspect the repository again:

```bash
git status
git diff --staged
```

Confirm that `student-info.txt` is ready to be committed.

### 5. Commit the change

Create a commit:

```bash
git commit -m "docs: add student information"
```

### 6. Verify the commit

Run:

```bash
git log -1 --oneline
git status
```

Confirm that:

* The commit appears in the Git history.
* The commit message is correct.
* Git reports that there is nothing left to commit.

## Part 2: Create a Merge Commit

### 7. Create a feature branch

Create and switch to a branch named `add-hobby`:

```bash
git switch -c add-hobby
```

Verify the current branch:

```bash
git branch
```

The `add-hobby` branch should have an asterisk beside it.

### 8. Make a change on the feature branch

Add the following line to `student-info.txt`:

```text
Favorite hobby: Your Answer
```

Replace the placeholder with your answer.

Inspect and commit the change:

```bash
git status
git diff
git add student-info.txt
gi
```
