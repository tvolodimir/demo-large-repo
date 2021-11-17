# demo-large-repo

## Demo

using partial clone
```
git clone --sparse --filter=blob:none --no-checkout https://github.com/tvolodimir/demo-large-repo.git test1
```
using shallow clone
```
git clone --depth 1 --no-checkout https://github.com/tvolodimir/demo-large-repo.git test2
```

## Shallow Clone

With git shallow clone you get fewer files. Provide an argument of -- depth 1 to the git clone command to copy only the latest revision of a repo:

```git clone -–depth [depth] [remote-url]```
 
You can also use git shallow clone to access a single branch:

```git clone [remote-url] --branch [name] --single-branch [folder]```

Or you can use `--depth=1` to get all files but with no history.

## Single Branch clone
 
`git clone <url> --single-branch` clones only the remote primary HEAD (default: origin/master)
`git clone <url> --branch <branch> --single-branch [<folder>]` clones only the remote <branch>
 
```
# unshallow the current branch
git fetch --unshallow

# for getting back all the branches
git config remote.origin.fetch refs/heads/*:refs/remotes/origin/*
git fetch --unshallow
```

## Filter clone
Specifying –filter= allows you to tell the server you’re cloning from the objects you choose.
The format for filter-spec is defined in the options section of git rev-list --help. or here - https://github.com/git/git/blob/v2.34.0/Documentation/rev-list-options.txt#L883-L931

`--no-checkout` tells Git to avoid checking out the repository entirely

The form `--filter=blob:none` omits all blobs.
 
The form `--filter=sparse:oid=<blob-ish>` uses a sparse-checkout specification contained in the blob (or blob-expression) <blob-ish> to omit blobs that would not be required for a sparse checkout on the requested refs.
 
A partial clone with missing trees can be obtained using `git clone --filter=tree:0 <repo>`
 
`--filter=blob:none` will exclude all files from the clone and only fetch the commits

##  (cone) sparse-checkout

You can use `--sparse` to get only the root directory, then edit the sparse checkout file to add the directory you want.


 
```
cd <directory>
git sparse-checkout init --cone # to fetch only root files
git sparse-checkout set apps/my_app libs/my_lib # etc, to list sub-folders to checkout
# they are checked out immediately after this command, no need to run git pull
```

```
git clone --filter=blob:none --no-checkout --depth 1 --sparse <project-url>
cd <project>
git sparse-checkout init --cone

# Specify the files and folders you want to clone

git sparse-checkout add <folder>/<innerfolder> <folder2>/<innerfolder2>
git checkout
```
 
`git archive --remote` to download partial sets of files.

```
#fastest clone possible:
git clone --filter=blob:none --no-checkout https://github.com/git/git
cd git
git sparse-checkout init --cone
git read-tree -mu HEAD
```
 
## Remove all history at server

Use the --orphan option, which returns it to the init state with only one commit.
Add all the files in the path and commit. 
Delete the remote master branch, rename the current branch to master.
Force push your new master to the code hosting environment. 
Remove all the old files with the prune command, and push the new state to the remote.
```
git checkout --orphan freshBranch
git add -A
git commit
git branch -D master 
git branch -m master 
git push -f origin master 
git gc --aggressive --prune=all
git push -f origin master
```
 
## Other techniques
 
 
Use GVFS (Git Virtual File System) - https://devblogs.microsoft.com/devops/announcing-gvfs-git-virtual-file-system/
 
The Virtual Filesystem for Git (formerly GVFS) - https://vfsforgit.org/
 
microsoft/scalar - https://github.com/microsoft/scalar

The command `filter-branch` can rewrite huge swaths of your history - https://git-scm.com/book/en/v2/Git-Tools-Rewriting-History
 
working on two branches simultaneously - https://stackoverflow.com/a/30186843

## resources:
- https://github.blog/2020-01-13-highlights-from-git-2-25/
- https://github.blog/2020-01-17-bring-your-monorepo-down-to-size-with-sparse-checkout/
- https://github.blog/2020-12-21-get-up-to-speed-with-partial-clone-and-shallow-clone/
- https://github.blog/2021-11-10-make-your-monorepo-feel-small-with-gits-sparse-index/
- https://github.blog/2021-11-15-highlights-from-git-2-34/
- https://docs.gitlab.com/ee/topics/git/partial_clone.html
- https://git-scm.com/docs/partial-clone/en
- https://docs.github.com/en/repositories/working-with-files/managing-large-files
- https://git-lfs.github.com/
- https://www.atlassian.com/git/tutorials/big-repositories
- https://jira.atlassian.com/browse/BSERV-11639
- https://stackoverflow.com/a/67351911

