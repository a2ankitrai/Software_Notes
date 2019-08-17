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

## Adding ssh key to ssh agent

Adding your SSH key to the ssh-agent
Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key. When adding your SSH key to the agent, use the default macOS ssh-add command, and not an application installed by macports, homebrew, or some other external source.

Start the ssh-agent in the background.

$ eval "$(ssh-agent -s)"
> Agent pid 59566
If you're using macOS Sierra 10.12.2 or later, you will need to modify your ~/.ssh/config file to automatically load keys into the ssh-agent and store passphrases in your keychain.

Host *
  AddKeysToAgent yes
  UseKeychain yes
  IdentityFile ~/.ssh/id_rsa
Add your SSH private key to the ssh-agent and store your passphrase in the keychain. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.

$ ssh-add -K ~/.ssh/id_rsa

https://help.github.com/en/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent#adding-your-ssh-key-to-the-ssh-agent














----
