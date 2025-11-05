# testing-rebase
That other repo is not meant to test rebasing

Adding more information after rewriting

Check this Reddit post: https://www.reddit.com/r/git/comments/1oognou/comment/nn4ez2j/

Potential Causes
==================

1. The first is that Gutenberg repo is failing on merge commits, because it's running a Husky task that lints staged files and fails, so it`s impossible `--continue` the merge. Maybe I can try to disable Huskey with `HUSKY=0 git merge ...` next time.

2. The solution for now is using `git rebase` and ideally `--force-with-lease` push to update the PR branch. Remember to `--continue` after resolving conflicts.