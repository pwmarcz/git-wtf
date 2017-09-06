# git wtf

This is a repository for which Git gives weird results.

It has been prepared from the in-the-wild example using `git filter-branch`. I pruned irrelevant commits, replaced the trees with empty tree, and replaced committer information. However, the date information remains the same, as it seems to influence the result.

My Git version:

```
$ git --version
git version 2.14.1
```

The commit `one` (`dcee72990fa57bf3f5f84888ba3420495accb03d`) is reachable from commit
`two` (`c6451cf8c02959091e3b0d1fb30db4d947da5ac5`):

```
$ git rev-list two | grep $(git rev-parse one)
dcee72990fa57bf3f5f84888ba3420495accb03d
```

However, git claims that the `two..one` range is not empty:

```
$ git rev-list two..one
dcee72990fa57bf3f5f84888ba3420495accb03d
bc0d1337c44efe25d65e5a9f856e637066a9beb1
7749d908cefeb209752738ba9e97c58f2f1febc7

$ git rev-list ^two one
dcee72990fa57bf3f5f84888ba3420495accb03d
bc0d1337c44efe25d65e5a9f856e637066a9beb1
7749d908cefeb209752738ba9e97c58f2f1febc7
```
