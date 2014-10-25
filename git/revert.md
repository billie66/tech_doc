### revert multiple commits

    git revert --no-commit HEAD~2^..HEAD

or

    git revert --no-commit HEAD~3..HEAD

HEAD is the most recent commit, HEAD~1 is the following one

### reference

http://sebgoo.blogspot.jp/2014/02/git-how-to-revert-multiple-recent.html
