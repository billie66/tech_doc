### install sshpass on OS X

```
brew install https://raw.githubusercontent.com/kadwanev/bigboybrew/master/Library/Formula/sshpass.rb
```

Notice: connect vpn, then execute the command above

[guide](https://gist.github.com/arunoda/7790979)

```
SSHPASS='password' sshpass -e ssh -p2022 root@server << EOF
#commands to run on remote host
cd server_directory
ls
EOF
```
