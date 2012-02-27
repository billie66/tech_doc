### change host name in ubuntu 

You know, we can set the hostname of a machine when we install the ubuntu
on it, once you have the name, but it is ugly and you feel sick at the
sight of it, you want to change the name immediately, what can we do now?
Calm down, it's easy to change it in ubuntu，since the hostname is stored
in the /etc/hostname.

    sudo echo "hostname" > /etc/hostname 

Certainly, you can directly edit the file as well.At this point, it's not
done. You also need to modify the file /etc/hosts, and replace the old
hostname with the new one, otherwise when you run sudo, the command will
report a message, for example,

    sudo: unable to resolve host puppy. （puppy is a hostname）

Finally, you need to restart your machine, then make all change take
effect.

