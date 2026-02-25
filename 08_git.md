
# Remedy commits

Revert the full commit by creating a new commit:
`git revert hash_tag`

Remove the last commit in history:
`git reset HEAD^ --hard`

Edit or Remove the non-last commits in history:
```bash
git rebase -i hash_tag_to_remove^

# Then edit/delete the commit lines in an editor
# There will be command prompt after edit and exit the editor
```

## Rebase changes

`git fetch origin`: Update local repo

`git rebase origin/master`: Rebase the `featureX` branch onto remote tracking branch `origin/msater`

Rebase changes with conflict resolution

`git push origin HEAD:refs/for/master`: Commit for review



`git rebase -i origin/master`: interactive rebase

`pick` -> `edit`: rework certain commits

`pick` -> `delete`: delete certain commits

`git rebase --continue`: Continue after amending commits

### Precise rebase

`git rebase --onto <newbase> <since> <until>`
- `<newbase>`: The branch or commit onto which you will replay your commits (the new base).
- `<since>`: The commit before the first commit you want to move (exclusive).
- `<until>`: The commit where your sequence of changes ends, typically your current branch name (inclusive).

A practical example:
```
# 1. Rebase a branch onto the new base from the old base
git checkout feature-branch
git rebase --onto main <since> feature-branch

# 2. Move a serial of commits from a branch to another branch
git checkout source-branch
git rebase --onto target-branch <before> <until>
```

---

The example 1 tells git: "Find the commits from B (exclusive) to feature-branch (inclusive), and replay them onto main."
```
A---B---C---D  main
     \
      E---F  feature-branch
```
The result is a cleaner history:
```
A---B---C---D  main
             \
              E'---F'  feature-branch
```

---

The example 2 tells git: "Find the commits after commit B until commit D, replay them onto target-branch."
```
A---B---C---D  source-branch
     \
      E---F  target-branch
```
Then, the git history becomes:
```
A---B  source-branch
     \
      E---F---C'---D'  target-branch
```

In this case, the command sequence is the same as:
```
git checkout target-branch
git cherry-pick C D
```

---

## Discard local changes diverged from remote

`git reset --hard origin/main`

`git pull origin/main`

# Recover deleted files from Git history

## Identify the commits deleting files:

`git log --oneline --diff-filter=D --summary`

or

`git log --follow -- filename.txt`

## Restore the files

`git checkout <commit-hash>^ -- filename.txt`

or

`git restore --source <commit-hash>^ filename.txt`

# Recover deleted commits

View history of changes to current branch
> `git reflog`

Identify the commit to recover from the from reflog output

Reset the branch to desired commit
> `git reset --hard <commit-hash>`

Verify the recovery
> `git log`


# Discard local commits and pull from remote
```bash
# Fetch the latest changes from remote
git fetch origin

# Reset your local branch to match the remote branch exactly
git reset --hard origin/main
```
`--hard` flag: This discards all local changes, including uncommitted changes and all local commits. Use with caution!

# Reset git submodules to default commits

Reset all submodule by `git submodule foreach`

`git submodule foreach --recursive git reset --hard`



Remove submodules and re-clone them

```bash
# Unbind all submodules
git submodule deinit -f .

# Reinitialize and checkout again
git submodule update --init --recursive
```



List what commits submodule should point to (then you can checkout each commit in submodule):

`git ls-tree HEAD`



# Patch

Generate patch for a specific commit:

`git format-patch -1 <commit-hash>`



Generate patches for multiple commits:

`git format-patch <start-commit>..<end-commit>`



Generate patches for Last N commits:

`git format-patch -3`



Generate patches for uncommitted changes:

`git diff > my-changes.patch`



Apply a patch:

`git apply <patch-file>`



Apply and create a commit from the patch:

`git am <patch-file>`

