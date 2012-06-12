### How to move files from one git repo to another

### Extract a directory from a git repo

For example, there is a git repo called `hen`, which contains a subdirectory
called `search`, then I want to extract all the files in the `search` directory,
and preserve all the history about them. To do this, perform following steps:

    git clone hen newrepo
    cd newrepo
    git remote rm origin
    git filter-branch --prune-empty --subdirectory-filter search HEAD -- --all
    mkdir search
    mv * search
    git add .
    git commit

Now the `newrepo` repo should only have `search` directory, and if you run
`tig`, you will just see commits about the files in `search`. 

While you finish your job, it isn't perfect. It means that the `newrepo` is
not clean, and has many stuff needed to clean up. Run the commands below:

    du -mh hen
    du -mh newrepo

then you will understand why you have to clean up the `newrepo`, since the
size of `newrepo` is bigger than `hen's`, though the former's content should
be fewer.  So, here we do like this: 

##### Remove any original refs
    
    git for-each-ref --format="%(refname)" refs/original/ | xargs -n 1 git update-ref -d

##### Expire all entries from the reflog

    git reflog expire --expire=now --all

##### Reset Working Directory

    git reset --hard

##### Garbage Collection
    
    git gc --aggressive --prune=now

More details to check `git filter-branch --help` manual page, and [information on github][1].

### Move one git repo to another

Now I have had a git repo `newrepo` in the home directory, I want to move all
its content to another git repo called `repob`, and keep all commit history of
`newrepo`, how can I do?

    cd repob
    git remote add new ~/newrepo 
    git pull new master
    git remote rm new

With these steps above, `repob` could get all the files of `newrepo` repository.

[1]:https://github.com/matthewmccullough/git-workshop/blob/master/workbook/markdown/27-Filter-Branch.md

