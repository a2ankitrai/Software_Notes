Git cheatsheet
---

- Force push the changes when local repo is not in sync with the remote.

```
git push -f origin
```

- Publish or push to a different remote branch from local branch

```
git push origin local_branch:remote:local_branch
```


---

- Reverting the commit head without reverting the code.

```
git reset --soft <<Commit_id>>
```

- Reverting the commit head as well as reverting the code.

```
git reset --hard <<commit_id>>
```

or

```
git reset --hard <<origin_name>>/<<branch_name>>
```

---

- Discarding local changes and resetting the code to origin

```
git checkout -- <file>
```

---

## Deleting branch

**Locally**
```
git branch -d the_local_branch
```

**Remote Branch**

```
git push origin --delete the_remote_branch
```

## Removing cherry-pick commit

A cherry-pick is basically a commit, so if you want to undo it, you just undo the commit.

> when I have other local changes

Stash your current changes so you can reapply them after resetting the commit.

```
$ git stash
$ git reset --hard HEAD^
$ git stash pop  # or `git stash apply`, if you want to keep the changeset in the stash
```

> when I have no other local changes

```
$ git reset --hard HEAD^
```

----

# Setting up ssh for GIT.

https://help.github.com/en/articles/connecting-to-github-with-ssh

https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#generating-a-new-ssh-key

https://help.github.com/en/articles/adding-a-new-ssh-key-to-your-github-account
















----
