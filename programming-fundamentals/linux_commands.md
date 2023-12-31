# Linux Commands 
source: 
1. https://man7.org/linux/man-pages/dir_all_alphabetic.html
2. https://books.goalkicker.com/LinuxBook/
3. https://sourabhbajaj.com/mac-setup/iTerm/tree.html
4. https://www.freecodecamp.org/news/file-permissions-in-linux-chmod-command-explained/
5. https://www.geeksforgeeks.org/soft-hard-links-unixlinux/
6. https://clubmate.fi/symbolic-links-and-hard-links-creating-updating-deleting-and-all-that
7. https://devconnected.com/understanding-hard-and-soft-links-on-linux/
8. https://www.baeldung.com/linux/find-all-links-for-file
9. https://www.networkworld.com/article/3256288/linux-to-recurse-or-not.html
10. https://devconnected.com/user-administration-complete-guide-on-linux/

## Basic Linux Commands
Note: after the command e.g. ls, the options are called command flags (such as -a -R)

### Directory navigation
1. Full path of current working directory
``` bash
pwd
```
2. Navigate to the last directory that you are working in
``` bash
cd -
```
3. Navigate to current user's home directory
``` bash
cd ~ or cd
```
4. Navigate to the parent directory of current directory
``` bash
cd ..
```

## Listing files inside a directory
1. Listing files & directories in long format inside current directory (better readability)\
   Finding existing permissions of a file
``` bash
ls -l
```
2. Listing information about directories (not contents)
``` bash
ls -ld
```
3. Listing all files (including hidden ones -- files starting with a .)
``` bash
ls -a
```
4. List files and Appends symbol at the end of a filename to indicate its type\
(* -- executable; / -- directory; @ -- symbolic link; = -- socket; | -- pipe; > -- door)
``` bash
ls -F
```
5. Print the index number of each file (inode number is on the column located at the extreme left)
``` bash
ls -li
```
6. Listing files sorted by last modified time in long format (top -- most recently modified files)
``` bash
ls -lt
```
7. Listing files in human readable format (sizes like 1K 234M 2G etc)
``` bash
ls -lh
```
8. Display all subdirectories recursively (long format)
``` bash
ls -lR
```
9. Generate tree representation of file system starting from current directory\
Tree is a recursive directory listing command that produces a depth indented listing of files
``` bash
tree
```
### Installation of Tree on Mac
``` bash
brew install tree
```
#### To limit the recursion you can pass an -L flag and specify the maximum depth tree will use when searching
``` bash
tree -L 1
```
will output:
``` bash
.
├── Apps
├── CONTRIBUTING.md
├── Cpp
├── Docker
├── Git
└── Go

5 directories, 1 files
```
### Create, copy and remove file/directory
1. Copy file from source to destination, preserve original attributes of file (-p) while copying ie. file owner, timestamp, group, permissions
``` bash
cp -p source destination
```
2. Copy source directory to specified destination recursively
``` bash
cp -R source_dir
```
3. Move or Rename file (from file1 to file2)
``` bash
mv file1 file2
```
4. For new users to linux command line, prompts you for confirmation before removal of file
``` bash
rm -i filename
```
5. Remove directory recursively, without prompt forcefully, ignoring non-existent files
``` bash
rm -rf dir-name
```
6. Remove directory recursively
``` bash
rm -R dir-name
```
7. Remove empty directories
``` bash
rmdir dir-name
```
8. Create a new directory
``` bash
mkdir dir-name
```
9. Create a directory hierarchy, create parent directories as needed if they don't exist (can specify multiple directories)
``` bash
mkdir -p dir-name/sub-dir-name
```
10. Create a new file, if file does not exist, otherwise modify the timestamp of file to the current time
``` bash
touch filename
```

### Permissions and Groups for Files/Directory
#### 3 main commands when managing file permissions
i. chmod (Change mode)\
ii. chown (Change ownership)\
iii. chgrp (Change group)

1. Change file permissions (Specifications: u -- user; g -- group; o -- other; + -- add permissions; - remove; r -- read; w -- write; x -- execute)
``` bash
chmod <specifications> filename
```
2. Change file permissions of directory (and ALL contents within directory) recursively (Specifications: u -- user; g -- group; o -- other; a -- all of the above(equivalent to "ugo"); + -- add permissions; - remove; r -- read; w -- write; x -- execute)
``` bash
chmod -R <specifications> dir-name
```
<table>
 <thead>
  <tr>
   <th>Access</th><th>Symbolic Mode</th><th>Octal Value</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Read</td><td>r</td><td>4</td>
  </tr>
  <tr>
   <td>Write</td><td>w</td><td>2</td>
  </tr>
  <tr>
   <td>Execute</td><td>x</td><td>1</td>
  </tr>
 </tbody>
</table>

<table>
 <thead>
  <tr>
   <th>Identity</th><th>Symbolic Mode<br>(u+rwx,g+rw,o+r)</th><th>Position<br> (764 -- user, group, others)</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>User</td><td>u</td><td>First or left-most</td>
  </tr>
  <tr>
   <td>Group</td><td>g</td><td>Middle</td>
  </tr>
  <tr>
   <td>Others</td><td>o</td><td>Last or right-most</td>
  </tr>
 </tbody>
</table>

<table>
 <thead>
  <tr>
   <th>Task</th><th>Operator</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Grant a level of access</td><td>+</td>
  </tr>
  <tr>
   <td>Remove a level of access</td><td>-</td>
  </tr>
  <tr>
   <td>Set a level of access</td><td>=</td>
  </tr>
 </tbody>
</table>

### How to manage permissions in symbolic mode (more powerful than octal because we can mask out permission bits)
3. Add read, write or execute permissions for owner/user for file, install.sh
``` bash
chmod u+rwx install.sh
```
4. Add read permissions for owner and group for myfile
``` bash
chmod go+r myfile
```
5. Allow all users to read, write or execute permissions myfile
``` bash
chmod a +rwx myfile
```
6. Remove/revoke read permissions from group and others for myfile
``` bash
chmod go -r myfile
```
7. Change ownership of a file to user owner1
``` bash
chown owner1 filename
```
8. Change primary group ownership of directory dir-name to group grp_owner recursively
``` bash
chown -R grp_owner dir-name
```

### How to manage permissions in octal mode (permission modes are absolute, cannot be used to change individual bits)
``` bash
chmod 744 install.sh
```
First number (7) represents permission for user: 7 = 4(read) + 2(write) + 1(execute)\
Second number (4) represents permission for group: 4 = 4(read)\
Third number (4) represents permission for others: 4 = 4(read)

<div style="width:253px; height:222px; background-color: #FFFFFF">
<img src="https://www.freecodecamp.org/news/content/images/2022/12/permissions-1.png" alt="output of ls -l" title="Existing permissions output description">
</div>

First character refers to type of input
   - "-" refers to file
   - "d" refers to directory
   - "l" refers to symlink, which is a shortcut for a file or directory
 
Group next set of letters (rwx maximum 3 per group) refers to permissions for user, group and others

### Linux Links

#### Inode
Every file in the system has an inode (index node)\
It is an object that stores information (metadata) about any file within your filesystem in Linux operating system except its name and data (file contents)\
They are independent of filenames
- You can copy a single file, rename it, and still have it point to the same inode as the original

Inodes are specific to the file system, storage device, the partition\
Inodes are one-to-one match to a file
 - Every file has an inode
 - Every directory has an inode

Information contained in an inode:
- Inode number
- File size
- Owner information (User and group IDs associated with the file)
- Permissions needed to access the file
- File Type
- Number of links
- Device on which the file is stored 
- Creation, read, and write timestamps
- Location of the data (though not the filepath)

#### Soft link (Symbolic link) vs Hard link
Soft link is a pointer(file) to the original file (similar to windows shortcut)\
Smaller file size compared to the original file\
Link across file systems: If you want to link files across the file systems, you can only use symlinks/soft links\
Inode number of soft link is different from that of the original file
<div style="width:1399px; height:661px; background-color: #FFFFFF">
<img src="https://devconnected.com/wp-content/uploads/2019/08/sooft-links.png" title="Understanding Soft links">
</div>

``` bash
   inode #100 <------ originalfile
   inode #200 <------ softlink1
   inode #300 <------ softlink2  
```
The file and shortcut share the same content\
If you modify the content of the shortcut, changes will be applied to the content of the file\
If you delete the shortcut, only the reference to the first inode is deleted, contents of the file on disk won't be lost\
If you delete or move the original file, softlinks will not work properly (AKA Hanging links)!\
If we change the name of the original file, all the soft links for that file become dangling\
i.e. they are worthless since the symbolic link loses reference to the first inode, unable to read file (consequence)

Hard link is different name of the original file (But you are directly manipulating the file)\
Having same file size as original file\
We cannot create a hard link for a directory to avoid recursive loops\
Inode number of hardlink is the EXACTLY SAME as the original file
<div style="width:1399px; height:661px; background-color: #FFFFFF">
<img src="https://devconnected.com/wp-content/uploads/2019/08/hard-soft-links-768x499.png" title="Understanding Hard links">
</div>

``` bash
  inode #100 <------ originalfile
  inode #100 <------ hardlink1
  inode #100 <------ hardlink2
 ```
 If you modify the content in the original file, it will be modified in the hard link file\
 Likewise, if you modify content in hard link file, the contents in original file will be modified\
 If you delete the hard link file, you can still access original file content\
 However, if you delete the original file, the hard links will still contain data that were in original file\
 Removing hard link, just reduces the link count, but doesn’t affect other links
 
#### Difference between copying & creating hard link
<div style="width:1399px; height:661px; background-color: #FFFFFF">
<img src="https://devconnected.com/wp-content/uploads/2019/08/copying-a-file-768x419.png" title="Understanding Hard links">
</div>

When a file is duplicated(copied), you assign new blocks on disk with same content as original file and the inode is different\
Hard-linking does not duplicate content of the file it links to, you are using disk space to store the name of original file, not actual file content and you directly manipulate the original file
 
### Create Soft link (Symlink) to a file/directory
1. Create symlink for the files 
``` bash
# ln - link files; -s flag (specify symbolic link)
$ ln  -s <original filename> <link name>
```
2. Create links for the directory (-s flag specify symbolic link)
``` bash
$ ln -s <target_directory> <link_name>
```
### Remove Soft link (Symlink) to a file/directory
#### 2 main commands when removing Symbolic links
i. rm (removes given files and directories, accepts multiple arguments)\
ii. unlink (deletes a given file, only accepts single argument)

1. Remove symlinks for the file (on success, command exits with zero and displays no output)
``` bash
# Approach 1: rm
$ rm symlink_name
# Approach 2: unlink (safer approach)
$ unlink symlink_name
```
2. Receive prompting prior to removing symlinks for the file (to confirm type y and press Enter)
``` bash
$ rm -i symlink_name
```
``` bash
# Output
rm: remove symbolic link 'symlink_name'?
```

3. Remove symlinks for multiple files (pass names of symlinks as arguments separated by space)
``` bash
$ rm symlink1 symlink2
```
4. Remove symbolic link that points to a directory
``` bash
$ rm -r symlink_to_dir/
```
``` bash
$ rm -d symlink_to_dir/
```
``` bash
# -f flag (forcefully removes the symlink from directory)
$ rm -f symlink_to_dir/
```
### Create Hard link to a file/directory
``` bash
┌──The link command
│
│                          ┌──Path to the intended link, can use . or ~
│                          │
│                    ┌─────┴──────┐
ln /path/to/original /path/to/link
    └───────┬───────┘
            └──Path to the original file/folder can
               use . or ~ or other relative paths
```
   a. Display all the attributes stored into the inode
``` bash
# stat : get file status
# -x : Display information in a more verbose way as known from some Linux distributions
$ stat -x File_A
```
``` bash
# Output
    File: "File_A"
    Size: 7            FileType: Regular File
    Mode: (0644/-rw-r--r--)         Uid: (  501/   bob)  Gid: (   20/   staff)
Device: 1,4   Inode: 51882811    Links: 1
Access: Tue Jan 20 09:14:04 2015
Modify: Tue Jan 20 09:14:04 2015
Change: Tue Jan 20 09:14:04 2015
 Birth: Tue Jan 20 09:14:04 2015
```
### How to find links on a filesystem
i. find by exact filename\
ii. find by inode number\
iii. find by recursive method (use type flag to find links, limit search using maxdepth parameter)

#### i. Find by exact filename
``` bash
# With option -samefile we add our filename or directory
# -L flag to locate broken links
# The search executed everywhere using root directory ” / ”  as the working directory.
[mogamal@server1:~/test]find -L / -samefile file1.txt
/home/mogamal/test/file1.txt
/tmp/filelink
/opt/filelink2
/srv/filelink3
find: ‘/etc/polkit-1/localauthority’: Permission denied
``` 
``` bash
# for better readability, use redirections to redirect errors like “permission denied ” to /dev/null space
[mogamal@server1:~/test]find -L / -samefile file1.txt 2> /dev/null
/home/mogamal/test/file1.txt
/tmp/filelink
/opt/filelink2
/srv/filelink3
```
#### ii. Find by inode number
``` bash
# use stat on a file to see which inode number it refers to
[mogamal@server1:~/test]stat file1.txt
  File: file1.txt
  Size: 11              Blocks: 8          IO Block: 4096   regular file
Device: 810h/2064d      Inode: 94804       Links: 1
```
``` bash
# file1.txt refers to inode 94804
# use -inum action which refers to the inode of the file
# redirect errors like “permission denied ” to /dev/null space
[mogamal@server1:~/test]find -L / -inum 94804 2> /dev/null 
/home/mogamal/test/file1.txt 
/tmp/filelink
/opt/filelink2
/srv/filelink3
```
#### iii. Find by recursive method (use type flag to find links, limit search using maxdepth parameter)
``` bash
# -type allows multiple types to be specified
# when we specify the type as small L (l for the link), it displays all soft links in the specified path
# -ls option to list the full attributes of the links
[mogamal@server1:~/test]find / -type l -ls 2> /dev/null | more
    94809      0 lrwxrwxrwx   1 mogamal  mogamal        23 Jun 11 17:11 /tmp/dirlink -> /home/mogamal/test/dir1
    94805      0 lrwxrwxrwx   1 mogamal  mogamal        28 Jun 11 16:52 /srv/filelink -> /home/mogamal/test/file1.txt
    94808      0 lrwxrwxrwx   1 mogamal  mogamal        28 Jun 11 17:00 /tmp/filelink2 -> /home/mogamal/test/file1.txt
    94810      0 lrwxrwxrwx   1 mogamal  mogamal        24 Jun 11 17:11 /srv/dirlink2 -> /home/mogamal/test/dir1/
...
```
``` bash
# grep command to match the filename pattern which is file1.txt or dir1
[mogamal@server1:~/test]find / -type l -ls 2> /dev/null | grep dir1
    94809      0 lrwxrwxrwx   1 mogamal  mogamal        23 Jun 11 17:11 /tmp/dirlink -> /home/mogamal/test/dir1
    94810      0 lrwxrwxrwx   1 mogamal  mogamal        24 Jun 11 17:11 /srv/dirlink2 -> /home/mogamal/test/dir1/
...
```
``` bash
# to limit searches to the current directory, you have to use the maxdepth parameter
$ find . -maxdepth 1 -type l -ls 
   262558      0 lrwxrwxrwx   1 schkn   schkn           7 Aug 14 20:14 ./shortcut-folder -> folder/
   258539      0 lrwxrwxrwx   1 schkn   schkn           3 Jan 26 2019 ./soft-job -> job
```
### To recurse or not?
<table>
 <thead>
  <tr>
   <th>Command</th><th>Option</th><th>Comment</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>chown</td><td>-R</td><td></td>
  </tr>
  <tr>
   <td>cp</td><td>-R or -r</td><td></td>
  </tr>
  <tr>
   <td>grep</td><td>-R or -r</td><td>-R follows symlinks</td>
  </tr>
  <tr>
   <td>find</td><td>NA</td><td>recurses by default</td>
  </tr>
  <tr>
   <td>ls</td><td>-R/td><td></td>
  </tr>
  <tr>
   <td>mkdir</td><td>-p</td><td>p = parent dirs</td>
  </tr>
  <tr>
   <td>rm</td><td>-R or -r</td><td></td>
  </tr>
  <tr>
   <td>zip</td><td>-r</td><td></td>
  </tr>
 </tbody>
</table>

### User Administration Basics on Linux
#### 3 types of user accounts 
i. Root account (most powerful, highest authority, can perform any operation e.g. change pw, kill processes, navigate to any directories on filesystem) \
ii. System account (used by processes or programs on host e.g mail administration, run simple Apache server)\
iii. User accounts (real users like you and I, team members, to have private workspace, some accounts are 


created to retrieve some files on the host, can modify to give them correct configuration)

### User Account Identifiers
<div style="width:1399px; height:661px; background-color: #FFFFFF">
<img src="https://devconnected.com/wp-content/uploads/2019/10/user-identify.png" title="User Identifier">
</div>

#### Accounts have:
- Username (or Login ID)
- Second field used to be password, now it's marked with 'x' as a placeholder
- User ID (UID)
- Group ID (GID)
- Comments
- Home directory location
- Shell

Information are stored in the /etc/passwd file\
GID listed in /etc/passwd file is default group for an account\
New files belong to a user's default group
<br>
1. View information related to your ID (tells you who you currently are) 
``` bash
# UID used to uniquely identify users & categorize user accounts on a system
$ id
```
<div style="width:1399px; height:661px; background-color: #FFFFFF">
<img src="https://devconnected.com/wp-content/uploads/2019/10/id-command.png" title="id output">
</div>
<br>

<table>
 <thead>
  <tr>
   <th>Account Type</th><th>UID</th><th>GID</th>
  </tr>
 </thead>
 <tbody>
  <tr>
   <td>Root</td><td>0</td><td>0</td>
  </tr>
  <tr>
   <td>System, services<br> & other special accounts</td><td>1 to 500 or<br> 1 to 999 (Debian-based systems)</td><td>1 to 999</td>
  </tr>
  <tr>
   <td>User</td><td>1000 and above</td><td>1000 and above</td>
  </tr>
 </tbody>
</table>

#### Remote root login over ssh session
1. Login as a normal user account 
``` bash
ssh user1@server1.cyberciti.biz
```
2. Switch to root account
``` bash
su -
```
3. Update any package as sysadmin
``` bash
# For RHEL/CentOS server
yum upgrade
```
<br>

``` bash
# For Debian/Ubuntu server
apt update && apt upgrade
```

#### Superuser (Root)
1. Switch to root user (in Root's environment, using root's environment variables)
``` bash
$ su -
# need to supply root user account password when prompted
Password: *******
#
```

``` bash
# Once logged in, prompt changes from $ to #
#
```
<br>

Note: If you su -root, you become root, but you're using normal user's environment and variables.
``` bash
# Give you normal user's default shell
echo $SHELL
```

2. Create new user account
``` bash
useradd <username>
```
2. Create new user account with home directory if it does not exist (files and directories contained in skeleton directory will be copied to home directory)
``` bash
# useradd will create home directory unless CREATE_HOME in /etc/login.defs is set to no
# -d flag: new user will be created using HOME_DIR as the value for the user's login directory. The default is to append the LOGIN name to BASE_DIR and use that as the login directory name. The directory HOME_DIR does not have to exist but will not be created if it is missing.
# -s : specifies name of the user's login shell. The default is to leave this field blank, which causes the system to select the default login shell specified by the SHELL variable in /etc/default/useradd, or an empty string by default. This option also sets the SHELL variable in /etc/default/useradd
useradd -m -d /home/robert -s /bin/bash robert
# Note: /etc/passwd, /etc/group and /etc/shadow files are updated
```
3. Setting another user's password / Changing password of current user
``` bash
passwd <username>
```
4. Removing a user
``` bash
userdel <username>
```
5. Removing a user and its home folder
``` bash
userdel -r <username>
```
6. Listing groups the current user is in
``` bash
groups
```
7. Listing groups a user is in
``` bash
groups <username>
```
8. Display hostname of system in full (Fully Qualified Domain Name - FQDN)
``` bash
hostname -f
```
10. Display username of users logged in at the terminal
``` bash
whoami
```
11. Who recently used the system
``` bash
last
```
12. When was the last time root logged in as a user
``` bash
last root
```
13. Display all bad login attempts into the system for audit trail
``` bash
lastb
```
14. Modify the user -- comment/description
``` bash
# -c comment (new value of user's password file comment field, typically contains user's full name)
# GECOS field might be blank, contain a user's full name, or contains the name of some daemon or service account description
# AKA General Comprehensive Operating System (GCOS) field
usermod -c "Human Resources Admin" robert
```
``` bash
robert:x:1007:1007:Human Resources Admin:/home/robert:/bin/bash
```
