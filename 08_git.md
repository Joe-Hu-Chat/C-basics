
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

### precise rebase

`git rebase --onto <newbase> <since> <until>`
- `<newbase>`: The branch or commit onto which you will replay your commits (the new base).
- `<since>`: The commit before the first commit you want to move (exclusive).
- `<until>`: The commit where your sequence of changes ends, typically your current branch name (inclusive).

A practical example:
```
# 1. Check out the branch containing the commits you want to move
git checkout feature-branch

# 2. Rebase a specific range of commits onto the new base
git rebase --onto main <since> feature-branch
```
This command tells Git: "Find the commits from B (exclusive) to feature-branch (inclusive), and replay them onto main."

To move commits E and F from feature-branch to be based on `main` instead of old-base:
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


# reset git submodules to default commits

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

