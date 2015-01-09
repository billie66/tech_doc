### how to make subtitles for videos

use gnome-subtitles

### convert traditional han to simplified han

    sudo apt-get install gcin
    trad2sim

### check ubuntu version

    lsb_release -a

### ffmpeg

#### Create a thumbnail image every X seconds of the video

* extract just a single frame from the video into an image file with size 800x600

    ffmpeg -i input.mov -ss 0:00:01.000 -f image2 -vframes 1 -s 800x600 output.jpg

### convert jpg to png

    mogrify -format png /path/*.jpg

### java (amd64 or i386)

    sudo apt-get install openjdk-7-jre-headless

### json_reformat

    sudo apt-get install yajl-tools

### references

* http://askubuntu.com/questions/504276/how-do-i-use-apt-to-install-32-bit-openjdk-7-jre-on-azure-amd64-ubuntu-server-14
