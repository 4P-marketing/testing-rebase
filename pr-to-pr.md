https://www.reddit.com/r/git/comments/1op8bpe/

I know that this is not strictly Git, but there are a couple of Git commands involved to achieve this
Let's say that I see a PR in a repository, and the PR is the number 1234.
Say the repository is https://github.com/test/test-repository
The PR has been done from the fork https://github.com/forker/test-repository
With the branch: pr-branch (forker:pr-branch)
I intend to send PR into https://github.com/forker/test-repository/ inside pr-branch so after it is accepted, my commits are added into PR number 1234
What is the course of action to make this happen?
This has been my course of action, which has not finished as expected:
I started by cloning my fork of https://github.com/test/test-repository
My fork (say https://github.com/sirlouen/test-repository) is origin and upstream is https://github.com/test/test-repository
After cloning, I continued by using the gh command gh pr checkout 1234
This adds a remote to https://github.com/forker/test-repository called forker
This also creates a branch called pr-branch.
Now I create a branch from here: git checkout branch-of-pr-branch
I add the changes and commit them
Then I do git push origin branch-of-pr-branch
Now in GitHub I can go to https://github.com/forker/test-repository/ and a message is waiting there for a new PR with the button Compare & pull Request
But if I check the files changed here, there are several thousand files from https://github.com/test/test-repository not only my file with changes.
At this point I can conclude I'm doing something wrong at some point. The main reason there are so many files, is because the pr-branch has been sitting for 3 years in the upstream repository, and it has had a couple of merges over this period of time. But still I was expecting just 1 commit and only the files I was changing, so basically I'm doing something wrong at some point.
This has been one of those things I never got right, and I always tried to avoid just creating a brand new PR instead of a PR to the PR. But this time I would like to have it right.
Final note: I'm not a maintainer of the test/test-repository but even if I were, I think I would f**k it up with this protocol, because I'm doing some wrong command, but I'm not sure which one it is.
SOLUTION
- I sent this Reddit post to a colleague, and he told me that I was doing it correctly. The only missing part was after Compare & pull request the branch by default in the forker/test-repository repository was main. and I did not notice. I had to explicitly target the pr-branch and voila, PR to PR achieved.
I would use this post for future reference because I'm 100% sure I will forget this protocol in one month :)
EXTRA QUESTION
What would be the difference if I were the maintainer of the test/test-repository with edit permissions to the pr-branch? Obviously I would not have to do a PR because I could push directly to the branch.
So I assume that the difference is in step number 8 I would simply do:
8. git push forker branch-of-pr-branch
And it will get merged and directly appear in the PR 1234.
Am I right?