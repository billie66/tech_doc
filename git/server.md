### how to build a git server

* get a copy of your dir

  cp -rf my_file.old/ my_file

* encrypt the file

  $ ls
  accounts
  $ gpg -c accounts

* make it a git repo

   git init
   git add .
   git ci

* make a bare clone, bareclone is a repo without checkout file(current * version) only has commit history

    git clone --bare my_file

* now we scp the my_file.git to the server

    scp -r my_file.git billie@server.com:repo-farm

* make a local clone out of the .git on the server

    $ rm -rf my_file.git/
    $ rm -rf my_file
    $ git clone billie@server.com:repo-farm/my_file.git
