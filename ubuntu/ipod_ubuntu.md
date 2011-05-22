### sync ipod with pc on ubuntu 10.10

On ubuntu 10.10, use Rhythmbox to sync music repository in pc with ipod shuffle. Run Rhythmbox first, 

    Application -> sound&video ->Rhythmbox music player

secondly, plug ipod into usb port, then it will be recognized by Rhythmbox.
The ipod device named PETER, so PETER will show under `Devices` label. Now you
can sync songs with ipod. 

1. import songs in pc to Rhythmbox  
    
    Music -> import files... 

2. select `PETER` label, then will display a curving arrow icon in the button
   bar. 

Now, just click the blue arrow button, all the songs will be transmited to ipod.

Rhythmbox is really cool, it will show you the current playing song name and
singer on the top right corner of the screen when you leave the music player
to do other work.

In addition, there is a tool called gtkpod that can do the same work and with
more function. 

    sudo apt-get install gtkpod

You can get much more information from a good site about ubuntu, [ubuntu
guide][1].

Now, I prefer gtkpod than Rhythmbox. Rhythmbox is a little strange, it will
create many folders in ipod. 

[1]: http://ubuntuguide.net/get-ipod-touchipad-recognized-sync-with-gtkpod-in-ubuntu-10-1010-04
