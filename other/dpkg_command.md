1. List packages matching given pattern

	dpkg -l package-name-pattern

Dpkg is the Ubuntu package manager dpkg is a medium-level tool to install, build, 
remove and manage Ubuntu packages. 

The primary and more user-friendly front-end for _dpkg_ is dselect.dpkg itself is 
controlled entirely via command line parameters, which consist of exactly one 
action and zero or more options. The action-parameter tells dpkg what to do and 
options control the behavior of the action in some way.

Now we will see all the available commands for dpkg with examples

2. Install a package

    Syntax

    dpkg -i (.deb file name)

    Example

    dpkg -i avg71flm_r28-1_i386.deb

3. Install all packages recursively from a directory

    Syntax

    dpkg -R

    Example

    dpkg -R /usr/local/src

4. Unpack the package, but don’t configure it.

    Syntax

    dpkg --unpack package_file

    If you use -R option is specified, package_file must refer to a directory instead.

    Example

    dpkg --unpack avg71flm_r28-1_i386.deb

5. Reconfigure an unpacked package

    Syntax

    dpkg --configure package

    If -a is given instead of package, all unpacked but uncon-figured packages are configured.

    Example

    dpkg --configure avg71flm_r28-1_i386.deb

6. Remove an installed package except configuration files

    Syntax

    dpkg -r

    Example

    dpkg -r avg71flm_r28-1_i386.deb

7. Remove an installed package including configuration files

    Syntax

    dpkg -P

    If you use -a is given instead of a package name, then all packages unpacked, 
    but marked to be removed or purged in file /var/lib/dpkg/status, are removed 
    or purged, respectively.

    Example

    dpkg -P avg71flm

8. Replace available packages info

    Syntax

    dpkg --update-avail <Packages-file>

    With this option old information is replaced with the information in the Packages-file.

9. Merge with info from file

    Syntax

    dpkg --merge-avail <Packages-file>

    With this option old informa-tion is combined with information from Packages-file.

    The Packages-file distributed with Debian is simply named Packages.dpkg 
    keeps its record of available packages in /var/lib/dpkg/available.

10. Update dpkg and dselect’s idea of which packages are available with information from the package pack-age_file.

    Syntax

    dpkg -A package_file

11. Forget about uninstalled unavailable packages.

    Syntax

    dpkg --forget-old-unavail

12. Erase the existing information about what packages are available.

    Syntax

    dpkg --clear-avail

13. Searches for packages that have been installed only partially on your system.

    Syntax

    dpkg -C

14. Compare Package versions version numbers

    Syntax

    dpkg --compare-versions ver1 op ver2

15. Display a brief help message.

    Syntax

    dpkg --help

16. Display dpkg licence.

    Syntax

    dpkg --licence (or) dpkg --license

17. Display dpkg version information.

    Syntax

    dpkg --version

18. Build a deb package.

    Syntax

    dpkg -b directory [filename]

19. List contents of a deb package.

    Syntax

    dpkg -c filename

20. Show information about a package.

    Syntax

    dpkg -I filename [control-file]

21. List packages matching given pattern.

    Syntax

    dpkg -l package-name-pattern

    Example

    dpkg -l vim

22. List all installed packages, along with package version and short description

    Syntax

    dpkg -l

23. Report status of specified package.

    Syntax

    dpkg -s package-name

    Example

    dpkg -s ssh

24. List files installed to your system from package.

    Syntax

    dpkg -L package-Name

    Example

    dpkg -L nagios2

25. Search for a filename from installed packages.

    Syntax

    dpkg -S filename-search-pattern

    Example

    dpkg -S /sbin/ifconfig

26. Display details about package

    dpkg -p package-name

    Example

    dpkg -p nagios2

