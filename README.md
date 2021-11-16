# demo-large-repo

## Demo

using partial clone
```
git clone --sparse --filter=blob:none --no-checkout https://github.com/tvolodimir/demo-large-repo.git test1
```
using shalow clone
```
git clone --depth 1 --no-checkout https://github.com/tvolodimir/demo-large-repo.git test2
```

## Shallow Approach

With git shallow clone you get fewer files. Provide an argument of -- depth 1 to the git clone command to copy only the latest revision of a repo:

```git clone -–depth [depth] [remote-url]```
 
You can also use git shallow clone to access a single branch:

```git clone [remote-url] --branch [name] --single-branch [folder]```
 
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
