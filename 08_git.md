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

