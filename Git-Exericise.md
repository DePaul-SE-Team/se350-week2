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
```
Answer this question:

> Explain the result of `git diff`? Show screen shot or copy and paste the result to explain.

Continue with the script below

```bash
git add student-info.txt
git commit -m "docs: add favorite hobby"
```

### 9. Return to the main branch

Switch back to `main`:

```bash
git switch main
```

> If your repository uses `master` instead of `main`, replace `main` with `master`.

Open `student-info.txt`. Notice that the hobby is not present because that change currently exists only on the `add-hobby` branch.

### 10. Merge the feature branch

Merge `add-hobby` into the current branch:

```bash
git merge --no-ff add-hobby -m "merge: add hobby information"
```
The --no-ff option forces Git to create a merge commit, even when a fast-forward merge would be possible.

Answer below:
> What does the above command do?

### 11. Inspect the Git history

Run:

```bash
git log --oneline --graph --decorate --all
git status
```

Confirm that:

* The history contains the original commit.
* The history contains the feature-branch commit.
* The history contains the merge commit.
* `student-info.txt` now includes the hobby.
* The working tree is clean.

### Reflection

Answer each question in two or three sentences:

1. What is the difference between an untracked, staged, and committed file?
2. What changed after you ran `git add student-info.txt`?
3. Why was the hobby change not visible after switching back to `main`?
4. What did the merge operation do?
5. Why did this exercise use `--no-ff`?
6. How does the graph show that a branch was merged?

### Submission

Submit:

* The completed `student-info.txt` file.
* The output of `git log --oneline --graph --decorate --all`.
* The final output of `git status`.
* Your answer to the question from Part 1, Step 3.
* Your answers to the reflection questions.
