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
