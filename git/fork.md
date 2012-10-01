### First clone, after fork?

    git clone git://github.com/happypeter/happycasts.git

Now, change file .git/config of the local repo happycasts 

    [remote "origin"]
        fetch = +refs/heads/*:refs/remotes/origin/*
        url = git://github.com/happypeter/happycasts.git

to:
    url = git@github.com:billie66/happycasts.git 

then add a new branch:

   [branch "compass"]
       remote = origin
       merge = refs/heads/compass

Save .git/config file.

Create a new branch named compass and make it working branch.

    git branch compass
    git checkout compass

Push all changes on the compass branch to the remote compass branch on github.

    git push origin compass

Check the repo on github if it has a new branch named compass.
 
