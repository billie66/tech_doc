### how to run android emulator on ubuntu 12.04

1. install java environment, and it's better to install `openjdk-7-jdk`

     sudo apt-get install openjdk-7-jdk

2. Android SDK offical download address http://developer.android.com/sdk/index.html

     adt-bundle-linux-x86-20131030.zip (Linux 32-bit)

3. uncompress Android SDK package to my home directory

     billie@goodcat:~$ unzip adt-bundle-linux-x86-20131030.zip

4. go to the adt-bundle-linux-x86-20131030 directory

     billie@goodcat:~/adt-bundle-linux-x86-20131030$ ls
     eclipse  sdk
     billie@goodcat:~/adt-bundle-linux-x86-20131030$ cd sdk
     billie@goodcat:~/adt-bundle-linux-x86-20131030/sdk$ ls
     add-ons  build-tools  extras  platforms  platform-tools  samples  system-images  temp  tools

5. edit /home/billie/.bashrc file, add the two lines below to it.

     export PATH="${HOME}/adt-bundle-linux-x86-20131030/sdk/tools:${PATH}"

     export PATH="${HOME}/adt-bundle-linux-x86-20131030/sdk/platform-tools:${PATH}"

6. reload /home/billie/.bashrc

     source /home/billie/.bashrc

7. launch Android SDK Manager, run `android` command in the terminal

     billie@goodcat:~$ android

8. After type Enter, a dialog window will pop up, which is Android SDK Manager, then click checkboxes aside of
the `Tools` and an Android version (for example Android 4.4.2 API 19, the most top one in the list)
to install them. Make sure all the packages installed successfully before exiting the Manager.

9. launch Android Virtual Device Manager

     billie@goodcat:~$ android avd

10. after the AVD popup window shows, then click `new` button to create an new emulator,
then open a form (Edit AVD) with several fields needed to fill up. remember not to modify the `RAM` value.

11. when finished the form, click `OK` button, the new AVD is listed in the AVD Manager.

12. select the AVD just created, click `Start` button, then a `Launch Options` window will pop up, check
the `Scale display to real size` option. you can also detect your monitor dpi by clicking `?` button.
Finally click `Launch` button to load your AVD. maybe it will take a while.

### Reference

* http://imacify.com/2013/06/how-to-run-android-apps-on-ubuntu/
