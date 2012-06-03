### how to move files from one git repo to another

For example, there is a git repo called `hen`, which contains a subdirectory
called `search`, then I want to get all the files in the `search` directory,
and preserve all the history about them. To do this, perform following steps:

    git clone hen newrepo
    
    cd newrepo

    git filter-branch --prune-empty --subdirectory-filter search HEAD -- --all

Now the `newrepo` repo should only have `search` directory, and if you run
`tig`, you will just see commits about the files in `search`. 

While you finish your job, it isn't perfect. It means that the `newrepo` is
not clean, and has many stuff needed to clean up. Run the commands below:

    du -mh hen

    du -mh newrepo

then you will understand why you have to clean up the `newrepo`, since the
size of `newrepo` is bigger than `hen's`, though the former's content is few. 
So, here we do like this: 

* Remove any original refs
    
    git for-each-ref --format="%(refname)" refs/original/ | xargs -n 1 git update-ref -d

* Expire all entries from the reflog

    git reflog expire --expire=now --all

* Reset Working Directory

    git reset --hard

* Garbage Collection
    
    git gc --aggressive --prune=now

More details to check `git filter-brach` help document, and [information on github][1].

[1]:https://github.com/matthewmccullough/git-workshop/blob/master/workbook/markdown/27-Filter-Branch.md

