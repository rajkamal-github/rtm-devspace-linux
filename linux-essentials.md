# Redhat distribution

```
yum search http
yum info httpd
yum install httpd

yum list installed httpd
yum deplist httpd

yum remove httpd
yum autoremove httpd

which httpd

yum repolist

## check where yum looks for repository info
cd /etc/yum.repos.d
less CentOS-Base.repo

yum clean all
yum update

rpm -i <package_name>.rpm
rpm -ivh <package_name>.rpm
rpm -q <package_name>
rpm -qi <package_name>
rpm -ql <package_name>
rpm -qd <package_name>
rpm -qR <package_name>
rpm -qpR <package_name>
rpm -Uvh <package_name>
rpm --test -e <package_name> [erase test]
rpm -e <package_name> [erase]

```

# Debian

```
apt

source repo list location - /etc/apt/source.list

apt update
apt-cache search <package_name>
apt install <package_name>
which <package_name>
apt remove <package_name>
apt remove --purge <packge_name> # remove dependencies
apt autoremove # clean up the system
apt upgrade
apt full-upgrade

dpkg

dpkg --get-selection
dpkg-deb -i <package_name>.deb # view debian package details
dpkg-deb --contents <package_name>.deb
dpkg -i <package_name>.deb

apt update
apt -f upgrade

dpkg -r <package_name>.deb # remove
dpkg -l <package_name>.deb # list
dpkg -p <package_name>.deb # purge

```

# Basic linux commands

```
ls
ls -a
ls -l
ls -lS # sort by size desc
ls -lSr # sort by size desc reverse (asc)
ls -lt # sort by most recent
ls -l .cache # list files inside a folder
which ls # location of commands
env #  environment variables
echo $PATH
echo $HOSTNAME
whoami
su <otheruser> # switch user
su - # switch to root account
sudo reboot # old command : init 6
poweroff
shutdown
halt
shutdown --help
top

uname
uname -s
uname -r
uname -m
uname -o
uname -a

pwd #  print work directory. same as echo $PWD
cd #  change directory

cd and hit enter #  takes you back to home directory
cd ~ #  takes back to home directory
cd - #  get back to where you were last time based on $OLDPWD
```

# Eg:

```
[rajkamal@localhost ~]$ ls
bin      Documents  help.txt  Pictures  Templates
Desktop  Downloads  Music     Public    Videos
[rajkamal@localhost ~]$ cd Documents/
[rajkamal@localhost Documents]$ pwd
/home/rajkamal/Documents
[rajkamal@localhost Documents]$ cd
[rajkamal@localhost ~]$ pwd
/home/rajkamal
[rajkamal@localhost ~]$ cd -
/home/rajkamal/Documents
[rajkamal@localhost Documents]$ 

```

cat .bash_history #  records all command history ran recently
history
!62 # 62 command in the history


# Shell Configuration Files

```
# For all users
/etc/bashrc	#  system wide functions and aliases
/etc/profile	#  system wide env. and startup programs used during a login shell
/etc/profile.d	#  location of extra env. setup scripts


# For specific user
.bash_profile	#  used to set user specific shell env. preferences
.bash_logout	#  ran when user logs out of a login shell not a terminal
.bashrc		#  non-login file that stores user specific functions and aliases
```

# Shell variables
env

## variable scopes
```
TEST="testing"
echo $TEST
bash	# new bash terminal
echo $TEST	#  empty. Because, it was local to previous terminal shell
exit
export TEST
bash
echo $TEST	#  now prints the value.
```
## add new location (/opt) to path variable
PATH = $PATH:/opt

# Globbing
Wild card pattern to print out matching files or folders you are looking for

```
ls *.txt
ls test*

#? matches any single character
ls ?.txt #matches 1.txt, 2.text
ls ????.txt	#matches 1234.txt 4567.txt
ls test?.txt	#matchtes test1.txt test2.txt
ls [Pp]*.txt	#matches any file starting with P or p
ls [p]*.txt	#matches any files starting with p
ls [Ww]eather.txt	#matches any file Weather.txt or weather.txt
ls [Ww]eather[Rr]eport199[0-9] #matching file weatherreport1992, weatherreport1993, WeatherReport1994
ls [Ww]eather[Rr]eport199[0-9]?2017 #matching file weatherreport1992 2017

#not match
ls [^WtTJP]*	#any file except starting with W,t,T,J,P

#wild card folder name
ls /etc/*/important/
```

# Quoting ",',\

```
# resolves the variable
echo "The currently logged on user is $LOGNAME"

# prevents bash from evaluating variable
echo 'The currently logged on user is $LOGNAME'

# backslash \ (escape the dollar sign)
echo "Hey, can I borrow \$3.50"

# to list files under folder "Secret Stuff"
ls Secret\ Stuff
ls "Secret Stuff"
ls 'Secret Stuff'

# extend the commands to multiple lines
ls \
-l
```

# Formatting commands
```
# $ user
[rajkamal@localhost ~]$ 

# "#" for root account
root@localhost ~]# 
```

# flags and arguements

```
ls -l Documents/
-l => flag
Documents/ => Arguements
```

# Locate, find, whereis
Additional note : whereis, whoami, which

Searches local database of files and folders looking for items that matchs the search criteria
```
locate passwd
```

## find - Searches the file system for files that match the search criteria

```
find /path/to/folder -name passwd


When using find command to search for part of a file name
find /path/to/folder -name "*file"
find /path/to/folder -name "*.xml"
```

## whereis - locates binary, source and/or manual pages for a command
```
whereis cd

locate passwd	
```

# Linux File System

Ref: http://www.pathname.com/fhs/

```
Take you to the root directory of the file system
cd /
```

```
[rajkamal@localhost /]$ ls -l
total 24
lrwxrwxrwx.   1 root root    7 Sep 25 17:22 bin -> usr/bin  # executable programs where the regular user can run
dr-xr-xr-x.   5 root root 4096 Sep 25 22:56 boot            # boot directory contains necessary files to get boot up. Linux kernel also resides here.
drwxr-xr-x.  20 root root 3200 Sep 27 10:29 dev             # location where all the devices are referenced from. Hardrives, keyboards, usb devices
drwxr-xr-x. 153 root root 8192 Sep 28 15:10 etc             # configuration files contains all system services
drwxr-xr-x.   3 root root   22 Sep 25 17:30 home            # user accounts directory.
lrwxrwxrwx.   1 root root    7 Sep 25 17:22 lib -> usr/lib  # lib files that contain code that gets shared out to many application in your system
lrwxrwxrwx.   1 root root    9 Sep 25 17:22 lib64 -> usr/lib64 # same as lib for 64 bit
drwxr-xr-x.   2 root root    6 Apr 10  2018 media           # cd , usb are mounted to
drwxr-xr-x.   2 root root    6 Apr 10  2018 mnt             # harddrives connected to system
drwxr-xr-x.   4 root root   49 Sep 25 22:55 opt             # optional location for application to be stored if they are not located in bin
dr-xr-xr-x. 242 root root    0 Sep 27 10:29 proc            # Linux outputs information about running linux system. Console.log
dr-xr-x---.   8 root root  279 Sep 27 10:47 root            # home directory for root user. Not to be confused with main root of the file system
drwxr-xr-x.  41 root root 1260 Sep 28 15:42 run             #
lrwxrwxrwx.   1 root root    8 Sep 25 17:22 sbin -> usr/sbin# location where sys admin tools and programs are located which is used by root user
drwxr-xr-x.   2 root root    6 Apr 10  2018 srv             # typical use for server applications such as web server
dr-xr-xr-x.  13 root root    0 Sep 27 10:29 sys             # contains information about the hardware that is on the system
drwxrwxrwt.  35 root root 4096 Sep 28 15:45 tmp             # location to store temporary data
drwxr-xr-x.  13 root root  155 Sep 25 17:22 usr             # contains own set of directory tree that closely mirrors of the root directory.
drwxr-xr-x.  22 root root 4096 Sep 26 09:43 var             # contains files that tend to vary in size like log files, printer files and local system email files.
```

# Absolute and relative paths

## Absolute Path
Absolute path to the file. Always begin with the root directory (/)

```
[rajkamal@localhost ~]$ pwd
/home/rajkamal
[rajkamal@localhost ~]$ 
```

## Relative Path 
Relative path (doesn't start with /. Always relative to current location)

```
[rajkamal@localhost ~]$ cd ~
[rajkamal@localhost ~]$ pwd
/home/rajkamal
[rajkamal@localhost ~]$ ls
bin  Desktop  development  Documents  Downloads  help.txt  Music  node_modules  Pictures  Public  Templates  Videos
[rajkamal@localhost ~]$ cd development/
[rajkamal@localhost development]$ 
```

# Files and Directories

```
mkdir <directory_name>
mkdir <dir1> <dir2> <dir3>  # creates a list of directories
mkdir -p dir/subdir1/subdir2

touch <filename.extension>
cp <file_path> <destination_path>
mv <file_path> <destination_path>
cp -R <folder_path> <destination_path>  # -R flag to recursively copy all its contents

rmdir <directory_name>  # for empty directory
rm -r <directory_name> # to recursively delete all its contents
```

# Archive and compression

## tar
Bundle files into a single file.