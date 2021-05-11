# Git

## wording

- [Good references](https://stackoverflow.com/a/3690796)
- [Usage of index explained](http://web.archive.org/web/20090210020404id_/http://whygitisbetterthanx.com/#the-staging-area)
- index = staging area
- working tree = working directory
- (branch) head: pointer to the newest commit on a branch
- tag: fixed pointer to commit
- HEAD: movable pointer which usually points to the head/tip of a branch. The next commit will take action on the commit which HEAD points to.
- reset (HEAD vs index vs working tree)
  - Reset Soft (HEAD only)
  - Mixed (Head and index)
  - Hard (Head, index, Working Tree)

## clear working directory (with untracked files)

With reset:

- To last commit including ignored files: `git reset --hard && git clean -dfx`
- To last commit: `git reset --hard && git clean -df`

With stash. Allows to revert changes, but not recommended with many files: 

- To last commit including ignored files: `git stash --all`
- To last commit: `git stash --include-untracked `
- Permanently deleting files: `git stash drop`
- Revert changes: `git stash pop`

## clean files in history

If you want to delete passwords or other sensible stuff from git history use [bfg](https://rtyley.github.io/bfg-repo-cleaner/). It does not touch your current commit (HEAD) just older commits.

Afterwards use force push to change history: `git push --force`

## ignore certs

- via system env variable: env GIT_SSL_NO_VERIFY=true
- or via cli: git config http.sslVerify "false"

## tag

```shell 
git tag -a 1.2.3 -m "message
git push --follow-tags

```

## password manager

```
# check existing methods
git help -a | grep credential

# there options might be available 
## credential           Retrieve and store user 
## credential-cache     Helper to temporarily store passwords in memory
## credential-store     Helper to store credentials on disk in plaintext (~/.git-credentials)

# credential-cache
git config --global credential.helper "cache --timeout 30000"

# credential-store 
git config --global credential.helper "store"

# you might need to install manager-core to use it
# and then set it via
# git config --global credential.helper "manager-core"
```
