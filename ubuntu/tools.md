### how to make subtitles for videos

use gnome-subtitles

### convert traditional han to simplified han

  sudo apt-get install gcin
  trad2sim

### ffmpeg

#### Create a thumbnail image every X seconds of the video

* extract just a single frame from the video into an image file with size 800x600

  ffmpeg -i input.mov -ss 0:00:01.000 -f image2 -vframes 1 -s 800x600 output.jpg
