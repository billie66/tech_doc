### install nginx

    sudo apt-get install python-software-properties
    sudo add-apt-repository ppa:nginx/stable && apt-get update
    ---
    W: GPG error: http://ppa.launchpad.net natty Release: The following
    signatures couldn't be verified because the public key is not available:
    NO_PUBKEY 00A6F0A3C300EE8C
    ---
    sudo apt-key adv --recv-keys --keyserver keyserver.ubuntu.com 00A6F0A3C300EE8C
    sudo apt-get install nginx

### nginx error log files and nginx log file location

All Nginx configuration files are located in the /etc/nginx/ directory. The
primary configuration file is `/etc/nginx/nginx.conf`. [Reference](https://www.linode.com/docs/websites/nginx/basic-nginx-configuration)

The error log should be defined there with the "error_log" directive. For example:

    error_log /var/log/nginx/error.log

the "access_log" directive:

    access_log /var/log/nginx/access.log

cat

The "cat" command simply displays the contents of a file.
To see the whole error log all at once, you might run

    sudo cat /var/log/nginx/error.log

less

If the log you want to look at is particularly large,
you probably don't want to look at the whole thing at once.
To browse through a file you can use the "less" command:

    sudo less /var/log/nginx/error.log

While less is displaying a file you can hit the space bar to page down,
and the up and down arrow keys on your keyboard to scroll up or down one line at a time.

tail

The "tail" command returns lines from the end of a file.
By default tail displays the last ten lines of a file,
so this command would display the last ten lines of an access log:

    sudo tail /var/log/nginx/access.log

To specify the number of lines to grab, use the "-n [number]" option.
To display the last 100 lines of the access log, you could run:

    sudo tail -n 100 /var/log/nginx/access.log

You can also save yourself a little typing by just using "-[number]" instead of "-n [number]", as in:

    sudo tail -100 /var/log/nginx/access.log

The tail command is useful if you're just looking for recent activity in a log.
If you want to watch the end of a file for changes as they happen,
you can use the "-f" option:

    sudo tail -f /var/log/nginx/access.log

With this version of tail running, when a new line is added to the log file you'll see it on your screen too.
To get out of tail when it's in this mode use control-C.

grep

If you're looking for a particular item in a web log (like a certain IP address, or any "404" responses),
skimming through the log manually can be tiresome. It's easier to let the "grep" command do the work for you.
The grep command will look through its input, or a file, and return any lines that contain the search term sent to it.
To look for the term "404" in an access log, you might run:

    sudo grep 404 /var/log/nginx/access.log

