[user]
	name = Billie Zhang
	email = billiecoder@gmail.com
[core]
	editor = vim
[merge]
	tool = vimdiff

[branch "gh-pages"]
    remote = origin
    merge = refs/heads/gh-pages
[alias]
    st = status
    co = checkout
    br = branch
    ci = commit -a -v 
    throw = reset --hard # remove staged and working tree changes
    cn = clean -f -d     # remove untracked files
[color]
    ui = auto
