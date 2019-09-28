# Redhat distribution
yum search http
yum info httpd
yum install httpd

yum list installed httpd
yum deplist httpd

yum remove httpd
yum autoremove httpd

which httpd

yum repolist

// check where yum looks for repository info
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


# Debian

apt

source repo list location - /etc/apt/source.list

apt update
apt-cache search <package_name>
apt install <package_name>
which <package_name>
apt remove <package_name>
apt remove --purge <packge_name> // remove dependencies
apt autoremove // clean up the system
apt upgrade
apt full-upgrade

dpkg

dpkg --get-selection
dpkg-deb -i <package_name>.deb // view debian package details
dpkg-deb --contents <package_name>.deb
dpkg -i <package_name>.deb

apt update
apt -f upgrade

dpkg -r <package_name>.deb // remove
dpkg -l <package_name>.deb // list
dpkg -p <package_name>.deb // purge

# Basic linux commands

ls
ls -a
ls -l
ls -lS //sort by size desc
ls -lSr //sort by size desc reverse (asc)
ls -lt //sort by most recent
ls -l .cache //list files inside a folder
which ls //location of commands
env // environment variables
echo $PATH
echo $HOSTNAME
whoami
su <otheruser> //switch user
su - //switch to root account
sudo reboot //old command : init 6
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

pwd // print work directory. same as echo $PWD
cd // change directory

cd and hit enter // takes you back to home directory
cd ~ // takes back to home directory
cd - // get back to where you were last time based on $OLDPWD

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

cat .bash_history // records all command history ran recently
history
!62 //62 command in the history


# Shell Configuration Files

#For all users
/etc/bashrc	// system wide functions and aliases
/etc/profile	// system wide env. and startup programs used during a login shell
/etc/profile.d	// location of extra env. setup scripts

#For specific user
.bash_profile	// used to set user specific shell env. preferences
.bash_logout	// ran when user logs out of a login shell not a terminal
.bashrc		// non-login file that stores user specific functions and aliases


# Shell variables
env

# ariable scopes

TEST="testing"
echo $TEST
bash	//new bash terminal
echo $TEST	// empty. Because, it was local to previous terminal shell
exit
export TEST
bash
echo $TEST	// now prints the value.

#a dd new location (/opt) to path variable
PATH = $PATH:/opt

# Globbing
#Wild card pattern to print out matching files or folders you are looking for

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


# Quoting ",',\

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


# Formatting commands

# $ user
[rajkamal@localhost ~]$ 

# "#" for root account
root@localhost ~]# 

# flags and arguements

ls -l Documents/
# -l => flag
# Documents/ => Arguements

# Locate, find, whereis
## Additional note : whereis, whoami, which

# searches local database of files and folders looking for items that matchs the search criteria
locate passwd

# searchs the file system for files that match the search criteria
find /path/to/folder -name passwd

# when using find command to search for part of a file name
find /path/to/folder -name "*file"
find /path/to/folder -name "*.xml"

# whereis - locates binary, source and/or manual pages for a command
whereis cd

locate passwd	

