* take a screenshot  `shift+cmd+4 `

* maximize the google chrome window on Mac OS X

Quick version: press shift key, at the same time click the green button in the
title bar of chrome.

Add a new keyboard shortcut, under system preference > keyboard > keyboard
shortcuts > application shortcuts, make the menu title be 'Zoom', and make the
keyboard shortcut for Zoom be `shift+command+m`

* toggle device mode of chrome dveloper tools

点击 chrome 开发者工具中的手机图标，就能触发 device mode 功能

官方文档 <https://developer.chrome.com/devtools/docs/device-mode>

* start a http server

    python -m SimpleHTTPServer

* pretty print json

    cat unformated.json | python -m json.tool > formated.json

* uncompress 7z archive

    $ file font.7z
    font.7z: 7-zip archive data, version 0.3
    $ brew install p7zip
    $ 7z x -ofont font.7z

`-ofont` output directory name is `font`
`x` keep the original file path

* convert encoding format

    $ iconv -f big5 -t utf8 input_file_name > output_file_name

the traditional Chinese uses big5 encoding format

* uncompress rar archive data

    brew install unrar

http://unix.stackexchange.com/questions/94837/having-trouble-uncompressing-a-few-files

* xcode problem

>Agreeing to the Xcode/iOS license requires admin privileges, please re-run as root via sudo.

run command `sudo xcodebuild -license` or directly open xcode and agree the agreement

* get info of video files

    ffmpge -i video_file_name

* make gif file using licecap

http://www.cockos.com/licecap/

* cp hidden files

    cp -rf src/demo/. dest/demo

* clear mails from system

```
sudo echo -n > /var/mail/<username>
```



