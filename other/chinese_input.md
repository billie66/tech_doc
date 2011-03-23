### Install chinese-input method in ubuntu(original language is english)

1. remove scim package

   `sudo apt-get --purge remove scim`

2. install fcitx package

	`sudo apt-get install im-switch fcitx`

    `im-switch -s fcitx -z default`

3. edit a file named 95input

	sudo vim /etc/X11/Xsession.d/95input
	sudo chmod +x /etc/X11/Xsession.d/95input

4. install chinese support 

	system-Administration manage-language support-chinese

5. reboot OS

you can input chinese with scim but not fcitx disappearing toolbox icon only

### Install chinese input in ubuntu (chinese)

1. install locale package

	sudo apt-get install language-pack-zh
	sudo apt-get install language-support-zh

2. install fcitx

	sudo apt-get install fcitx

3. reboot OS

You can use scim chinese input but not fcitx 
	
