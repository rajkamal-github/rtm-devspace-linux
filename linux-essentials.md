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

# Power of Commandline

## Archive and compression

### Archiving using tar
Bundle files into a single file.

EXAMPLES

```
# Create archive.tar from files foo and bar.
tar -cf archive.tar foo bar 

# List all files in archive.tar verbosely.
tar -tvf archive.tar 

# Extract all files from archive.tar.
tar -xf archive.tar 
```

```
[rajkamal@localhost ~]$ ls
bin  Desktop  development  development.tar  Documents  Downloads  help.txt  Music  node_modules  Pictures  Public  Templates  Videos
[rajkamal@localhost ~]$ touch Documents/file1.txt
[rajkamal@localhost ~]$ touch Documents/file2.txt
[rajkamal@localhost ~]$ touch Documents/file3.pdf
[rajkamal@localhost ~]$ touch Documents/file4.doc
[rajkamal@localhost ~]$ touch Documents/file5.xls
[rajkamal@localhost ~]$ touch Documents/file6.xml
[rajkamal@localhost ~]$ touch Documents/file7.json
[rajkamal@localhost ~]$ ls Documents/
file1.txt  file2.txt  file3.pdf  file4.doc  file5.xls  file6.xml  file7.json
[rajkamal@localhost ~]$ tar -cf archive-documents.tar Documents
[rajkamal@localhost ~]$ ls
archive-documents.tar  bin  Desktop  development  development.tar  Documents  Downloads  help.txt  Music  node_modules  Pictures  Public  Templates  Videos
[rajkamal@localhost ~]$ mkdir tar-demo
[rajkamal@localhost ~]$ mv archive-documents.tar tar-demo/
[rajkamal@localhost ~]$ cd tar-demo/
[rajkamal@localhost tar-demo]$ tar -xf archive-documents.tar 
[rajkamal@localhost tar-demo]$ ls
archive-documents.tar  Documents
[rajkamal@localhost tar-demo]$ ls Documents/
file1.txt  file2.txt  file3.pdf  file4.doc  file5.xls  file6.xml  file7.json

```

### Compression using tar

#### Gzip compression 
Gzip is used for compression

```
tar -czf gzip-compression-demo.gz gzip-compresion-demo
```

#### Bz2 compression

```
tar -cjf bz2-compression-demo.bz2 bz2-compresion-demo
```

#### Lab

```
[rajkamal@localhost ~]$ mkdir compression
[rajkamal@localhost ~]$ cd compression/
[rajkamal@localhost compression]$ ls
[rajkamal@localhost compression]$ mkdir gzip-compression-demo
[rajkamal@localhost compression]$ touch gzip-compression-demo/file1.pdf
[rajkamal@localhost compression]$ touch gzip-compression-demo/file2.doc
[rajkamal@localhost compression]$ touch gzip-compression-demo/file3.doc
[rajkamal@localhost compression]$ touch gzip-compression-demo/file4.doc
[rajkamal@localhost compression]$ touch gzip-compression-demo/file5.doc
[rajkamal@localhost compression]$ mkdir bz2-compression-demo
[rajkamal@localhost compression]$ cp gzip-compression-demo/* bz2-compression-demo/
[rajkamal@localhost compression]$ ls bz2-compression-demo/
file1.pdf  file2.doc  file3.doc  file4.doc  file5.doc
[rajkamal@localhost compression]$ ls gzip-compression-demo/
file1.pdf  file2.doc  file3.doc  file4.doc  file5.doc
[rajkamal@localhost compression]$ tar -czf gzip-compression-demo.gz gzip-compression-demo
[rajkamal@localhost compression]$ tar -cjf bz2-compression-demo.bz2 bz2-compression-demo
[rajkamal@localhost compression]$ ls
bz2-compression-demo  bz2-compression-demo.bz2  gzip-compression-demo  gzip-compression-demo.gz
[rajkamal@localhost compression]$ tar -tvf gzip-compression-demo.gz 
drwxrwxr-x rajkamal/rajkamal 0 2019-09-28 17:01 gzip-compression-demo/
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 gzip-compression-demo/file1.pdf
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 gzip-compression-demo/file2.doc
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 gzip-compression-demo/file3.doc
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 gzip-compression-demo/file4.doc
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 gzip-compression-demo/file5.doc
[rajkamal@localhost compression]$ tar -tvf bz2-compression-demo.bz2 
drwxrwxr-x rajkamal/rajkamal 0 2019-09-28 17:01 bz2-compression-demo/
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 bz2-compression-demo/file1.pdf
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 bz2-compression-demo/file2.doc
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 bz2-compression-demo/file3.doc
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 bz2-compression-demo/file4.doc
-rw-rw-r-- rajkamal/rajkamal 0 2019-09-28 17:01 bz2-compression-demo/file5.doc
[rajkamal@localhost compression]$ ls
bz2-compression-demo  bz2-compression-demo.bz2  gzip-compression-demo  gzip-compression-demo.gz
[rajkamal@localhost compression]$ rm -r bz2-compression-demo
[rajkamal@localhost compression]$ rm -r gzip-compression-demo
[rajkamal@localhost compression]$ ls
bz2-compression-demo.bz2  gzip-compression-demo.gz
[rajkamal@localhost compression]$ tar -xzf gzip-compression-demo.gz 
[rajkamal@localhost compression]$ tar -xjf bz2-compression-demo.bz2 
[rajkamal@localhost compression]$ ls
bz2-compression-demo  bz2-compression-demo.bz2  gzip-compression-demo  gzip-compression-demo.gz
[rajkamal@localhost compression]$ ls gzip-compression-demo/
file1.pdf  file2.doc  file3.doc  file4.doc  file5.doc
[rajkamal@localhost compression]$ ls bz2-compression-demo/
file1.pdf  file2.doc  file3.doc  file4.doc  file5.doc
[rajkamal@localhost compression]$ 
```

### Other archiving and compression commands

```
zip
gzip
gunzip
bzip2
bunzip2

Refer man pages for these commands.

```

#### Lab for zip

```
[rajkamal@localhost compression]$ mkdir zip-demo
[rajkamal@localhost compression]$ cp gzip-compression-demo/* zip-demo/
[rajkamal@localhost compression]$ ls zip-demo/
file1.pdf  file2.doc  file3.doc  file4.doc  file5.doc
[rajkamal@localhost compression]$ zip -r zip-demo.zip zip-demo
  adding: zip-demo/ (stored 0%)
  adding: zip-demo/file1.pdf (stored 0%)
  adding: zip-demo/file2.doc (stored 0%)
  adding: zip-demo/file3.doc (stored 0%)
  adding: zip-demo/file4.doc (stored 0%)
  adding: zip-demo/file5.doc (stored 0%)
[rajkamal@localhost compression]$ ls
bz2-compression-demo  gzip-compression-demo  zip-demo  zip-demo.zip
[rajkamal@localhost compression]$ rm -r zip-demo
[rajkamal@localhost compression]$ unzip zip-demo.zip 
Archive:  zip-demo.zip
   creating: zip-demo/
 extracting: zip-demo/file1.pdf      
 extracting: zip-demo/file2.doc      
 extracting: zip-demo/file3.doc      
 extracting: zip-demo/file4.doc      
 extracting: zip-demo/file5.doc      
[rajkamal@localhost compression]$ ls
bz2-compression-demo  gzip-compression-demo  zip-demo  zip-demo.zip

```


## Viewing text

### Less, head and tail commands

```
less readme.md          # similar to man commands. Use up and down to navigate to the file contents.
head readme.md          # shows top 10 lines of file by default
tail readme.md          # shows bottom 10 lines of file by default
head readme.md -n 20    # Shows first 10 lines of file
tail -f cloudserverlogs.txt       # shows bottom 10 lines of file by default. But the file remains open for your view to file updates in realtime.

```

### Analyzing text document from command line
Head get first 1 line from file

```
head  # prints top 10 lines of the file by default
# -n  switch to print number of lines

# stdout command
# stdout print whatever is tossed into that bucket to the console. Every linux command, tosses output to the bucket which is printout to the screen from there.
# here we are piping (redirecting the output to a file instead of a bucket) the output to a file using  > and  >>
> Add to a file
>> Append to a file


#Eg.
[rajkamal@localhost linux-essentials]$ head -n 1 cicero_disputations.txt > ancient.txt^C
[rajkamal@localhost linux-essentials]$ head -n 1 cicero_disputations.txt > ancient.txt
[rajkamal@localhost linux-essentials]$ head -n 1 plato_republic.txt > ancient.txt
[rajkamal@localhost linux-essentials]$ head -n 1 aristotle_politics.txt >> ancient.txt
[rajkamal@localhost linux-essentials]$ head -n 1 cicero_disputations.txt >> ancient.txt
[rajkamal@localhost linux-essentials]$ cat ancient.txt 
The Project Gutenberg EBook of The Republic of Plato, by Plato
The Project Gutenberg EBook of Politics, by Aristotle
The Project Gutenberg EBook of Treaties on Friendship and Old Age, by Marcus Tullius Cicero
```

Cut command

```
# cut - cuts the input file based on a delimitter and selects the fields to print
# -d switch takes the delimitter
# -f switch takes the fields range to print. Here we print fields starting from 6th to end.

[rajkamal@localhost linux-essentials]$ cut -d" " -f 6- ancient.txt 
The Republic of Plato, by Plato
Politics, by Aristotle
Treaties on Friendship and Old Age, by Marcus Tullius Cicero

# Piping the output to a file
[rajkamal@localhost linux-essentials]$ cut -d" " -f 6- ancient.txt > ancient_works.txt
```

Sort command

```
# sorts the contents of a file alphabetically

[rajkamal@localhost linux-essentials]$ sort ancient_works.txt 
Politics, by Aristotle
The Republic of Plato, by Plato
Treaties on Friendship and Old Age, by Marcus Tullius Cicero
[rajkamal@localhost linux-essentials]$ sort ancient_works.txt > ancient_books.txt
```

Word count command

```
# word count command to add some statistics about the file
# -l switch prints the no. of lines in each file
# -w switch prints the no. of words in each file


[rajkamal@localhost linux-essentials]$ echo >> ancient_books.txt 
[rajkamal@localhost linux-essentials]$ echo "  Lines  Words  Document" >> ancient_books.txt 
[rajkamal@localhost linux-essentials]$ cat ancient_works.txt 
The Republic of Plato, by Plato
Politics, by Aristotle
Treaties on Friendship and Old Age, by Marcus Tullius Cicero
[rajkamal@localhost linux-essentials]$ cat ancient_books.txt 
Politics, by Aristotle
The Republic of Plato, by Plato
Treaties on Friendship and Old Age, by Marcus Tullius Cicero

  Lines  Words  Document
[rajkamal@localhost linux-essentials]$ wc -lw plato_republic.txt aristotle_politics.txt cicero_disputations.txt >> ancient_books.txt 
[rajkamal@localhost linux-essentials]$ cat ancient_books.txt 
Politics, by Aristotle
The Republic of Plato, by Plato
Treaties on Friendship and Old Age, by Marcus Tullius Cicero

  Lines  Words  Document
  29809  255816 plato_republic.txt
  29809  255813 aristotle_politics.txt
  29809  255820 cicero_disputations.txt
  89427  767449 total
[rajkamal@localhost linux-essentials]$ 

```

## Pipes, grep and regular expressions

```
# grep  - show the lines in a file that matches a specific pattern
# -l = performs a case in-sensitive search
# -v = returns the lines that doesn't contain the pattern
# -r = performs a recursive search
# | = pipes the output of a command to another command
# Regular expressions
# ^ = searches the beginning of a line
# $ = searches the end of a line
# . = stands in for a single character. (wild card for a single character. eg: ".[h]" pattern search for any word that has second word as h)
# [abc] = search for a specified characters
# [^abc] = search for any other characters than specified
# * = Matches zero of more of the proceeding characters or expression. Eg. "Log*" search for anything starts with "Log".

# Eg.

# case sensitive search
[rajkamal@localhost linux-essentials]$ grep republic cicero_disputations.txt 
had a myth respecting its own origin; the Platonic republic may also have

# case in-sensitive search
[rajkamal@localhost linux-essentials]$ grep -i republic cicero_disputations.txt
[rajkamal@localhost linux-essentials]$ 

# Piping output of grep to commands

[rajkamal@localhost linux-essentials]$ grep -i republic cicero_disputations.txt | less
[rajkamal@localhost linux-essentials]$ grep -i republic cicero_disputations.txt | wc -w
397
[rajkamal@localhost linux-essentials]$ grep -i republic cicero_disputations.txt | wc -l
36
[rajkamal@localhost linux-essentials]$ grep -i republic cicero_disputations.txt | wc -lw
     36     397
[rajkamal@localhost linux-essentials]$ 

# Regular expressions

# Lines starting with a word republic
[rajkamal@localhost linux-essentials]$ grep -i '^republic' cicero_disputations.txt

# Lines end with a word republic
[rajkamal@localhost linux-essentials]$ grep -i 'republic$' cicero_disputations.txt
[rajkamal@localhost linux-essentials]$ 

# Lines starting with specific characters
[rajkamal@localhost linux-essentials]$ grep '^[AaBb]' cicero_disputations.txt

# Lines doesn't start with specific characters
[rajkamal@localhost linux-essentials]$ grep '^[^AaBb]' cicero_disputations.txt

# Any word that has first unknown character (.) and second character as h
[rajkamal@localhost linux-essentials]$ grep '.[h]' cicero_disputations.txt 

# Any word starting with www
[rajkamal@localhost linux-essentials]$ grep 'www*' cicero_disputations.txt

# no star (*) would fetch the same results
[rajkamal@localhost linux-essentials]$ grep 'www' cicero_disputations.txt 

# if you are specific and enclose in a block. This would get only www and ignore wwww.
[rajkamal@localhost linux-essentials]$ grep '\bwww\b' cicero_disputations.txt 

```


### Excercise
- Log in to your Linux Essentials lab server.
- Become the root account user.
- List out the contents of the /var/log/messages log file and use pipes and the grep search utility to find anything that references DHCPREQUEST.
- Using the last command, how would you also use pipes and the more utility to page through the multiple pages of returns?
- How can we also use the grep and pipe utility to redirect the output data into a file called /root/file.log to then view those results?
- Now verify that the log that you redirected to the file.log file contains your output.

```
[rajkamal@localhost linux-essentials]$ sudo grep "DHCPREQUEST" /var/log/messages 
[sudo] password for rajkamal: 
Sep 25 17:32:47 localhost dhclient[8555]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x1311cbb6)
Sep 25 17:32:54 localhost dhclient[9947]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x48d266cf)
Sep 25 17:39:17 localhost dhclient[1159]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x4cbac94d)
Sep 25 17:42:09 localhost dhclient[1159]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x6d313c9)
Sep 25 17:51:07 localhost dhclient[1153]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x2fb89b48)
Sep 25 17:52:45 localhost dhclient[1159]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x311e0d41)
Sep 25 18:00:04 localhost dhclient[1168]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x463497f1)
Sep 25 18:04:38 localhost dhclient[3355]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x5d9e45d0)
Sep 25 18:07:28 localhost dhclient[3453]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x56032cbc)
Sep 25 18:12:31 localhost dhclient[3607]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x4cedf8b8)
Sep 25 18:13:16 localhost dhclient[3655]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x4764fc1b)
Sep 25 18:14:51 localhost dhclient[3713]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x12d858bd)
Sep 25 18:15:19 localhost dhclient[3759]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x549f55c0)
Sep 25 18:15:25 localhost dhclient[3790]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x48984e31)
Sep 25 22:32:59 localhost dhclient[1162]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x3501d865)
Sep 25 22:38:50 localhost dhclient[3282]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x44e0d5ac)
Sep 25 22:49:04 localhost dhclient[1259]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x5e2a3432)
Sep 26 11:34:24 localhost dhclient[1189]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x3703d934)
Sep 26 18:14:08 localhost dhclient[11810]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x6890e2db)
Sep 27 09:08:54 localhost dhclient[13200]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x71ee5cfc)
Sep 27 10:29:53 localhost dhclient[1187]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x251eae37)
Sep 27 17:58:57 localhost dhclient[19178]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0xdd6cca2)
Sep 28 15:10:26 localhost dhclient[19246]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x22659532)
Sep 29 22:15:05 localhost dhclient[1194]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x58057379)
Sep 30 09:30:53 localhost dhclient[3557]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x72e9199)
[rajkamal@localhost linux-essentials]$ sudo grep "DHCPREQUEST" /var/log/messages | less
[rajkamal@localhost linux-essentials]$ sudo grep "DHCPREQUEST" /var/log/messages > testfile.logd
[rajkamal@localhost linux-essentials]$ cat testfile.log 
Sep 25 17:32:47 localhost dhclient[8555]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x1311cbb6)
Sep 25 17:32:54 localhost dhclient[9947]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x48d266cf)
Sep 25 17:39:17 localhost dhclient[1159]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x4cbac94d)
Sep 25 17:42:09 localhost dhclient[1159]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x6d313c9)
Sep 25 17:51:07 localhost dhclient[1153]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x2fb89b48)
Sep 25 17:52:45 localhost dhclient[1159]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x311e0d41)
Sep 25 18:00:04 localhost dhclient[1168]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x463497f1)
Sep 25 18:04:38 localhost dhclient[3355]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x5d9e45d0)
Sep 25 18:07:28 localhost dhclient[3453]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x56032cbc)
Sep 25 18:12:31 localhost dhclient[3607]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x4cedf8b8)
Sep 25 18:13:16 localhost dhclient[3655]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x4764fc1b)
Sep 25 18:14:51 localhost dhclient[3713]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x12d858bd)
Sep 25 18:15:19 localhost dhclient[3759]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x549f55c0)
Sep 25 18:15:25 localhost dhclient[3790]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x48984e31)
Sep 25 22:32:59 localhost dhclient[1162]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x3501d865)
Sep 25 22:38:50 localhost dhclient[3282]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x44e0d5ac)
Sep 25 22:49:04 localhost dhclient[1259]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x5e2a3432)
Sep 26 11:34:24 localhost dhclient[1189]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x3703d934)
Sep 26 18:14:08 localhost dhclient[11810]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x6890e2db)
Sep 27 09:08:54 localhost dhclient[13200]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x71ee5cfc)
Sep 27 10:29:53 localhost dhclient[1187]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x251eae37)
Sep 27 17:58:57 localhost dhclient[19178]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0xdd6cca2)
Sep 28 15:10:26 localhost dhclient[19246]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x22659532)
Sep 29 22:15:05 localhost dhclient[1194]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x58057379)
Sep 30 09:30:53 localhost dhclient[3557]: DHCPREQUEST on eth0 to 255.255.255.255 port 67 (xid=0x72e9199)
[rajkamal@localhost linux-essentials]$ 
```

## Turning commands into a Script

### Text editor Nano
nano command

```
[rajkamal@localhost linux-essentials]$ nano toaster.txt
[rajkamal@localhost linux-essentials]$ cat toaster.txt 
Hello Linux Pioneers
[rajkamal@localhost linux-essentials]$ 

```

### Text editor vi/vim
vim

```
# default command mode
# i = insert mode
# Esc = leave the mode
# o = puts back to insert mode and puts the cursor at the end of the file
# h = left arrow
# j = bottom arrow
# k = up arrow
# l = right arrow
# v = visual mode
# vllll = Equivalent of highlight text
# y = yank the highlighted text to memory buffer. Effectively does the copy.
# p = paste the yanked text
# u = undo
# shift + g = go to the bottom of the file
# esc + :w <file_name> = write file with a name to disk
# dw = delete word
# shift + a = append text at the end of the line
# esc + :wq = write and exit

```

## Shell scripting

> .sh = shell script files but it's not necessary
> First line of any bash script need to have
> #!/bin/bash