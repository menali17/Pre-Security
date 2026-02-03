# Linux Part 2

## Acessing Linux Machine Using SSH

Secure Shell (SSH) is the common means of connecting to and interacting with the command line of a remote Linux machine

### What is SSH & how Does it Work?

Secure Shell is a protocol between devices in a encrypted form. Using cryptography, any input we send in a human-readable format is encrypted for travelling over a network, where it is then unencrypted once it reaches the remote machine.


                **My computer --> The internet --> Linux Server**

                 "Hello world" --> f6b97e4faca8a5 --> "Hello world" 


SSH allows us to remotely execute commands on another device remotely. Any data sent between the devices is encrypted when it is sent over a network such as the Internet

## Introduction to Flags and Switches

A majority of commands allow for arguments to be provided. These arguments are identified by a hyphen and a certain keyword known as flags or switches.

When using a command, unless otherwise specified, it will perform its default behaviour. For example, ls lists the contents of the working directory. However, hidden files are not shown. We can use flags and switches to extend the behaviour of commands.

Using ls as an example, ls informs us that there is only one folder named "folder1" as highlighted.

```bash
user12@linux1:~$ ls
folder1
```

However, after using the `-a` argument (short for `--all`), we now suddenly have an output with a few more files and folders such as ".hiddenfolder". Files and folders with "." are hidden files.

```bash
user12@linux1:~$ ls -a
.hiddenfolder folder1
```

Commands that accept these will also have a `--help` option. This option will list the possible options that the command accepts, provide a brief description and example of how to use it.

### The Man(ual) Page

The manual pages are a great source of information for both system commands and applications available on both a Linux machine, which is accessible on the machine itself and online.

To access this documentation, we can use the `man` command and then provide the command we want to read the documentation for. Using `ls`, we would use `man ls` to view the manual pages for `ls`:

```bash
user12@linux2:~$ man ls
LS(1)                                               User Commands                                               LS(1)

NAME
       ls - list directory contents

SYNOPSIS
       ls [OPTION]... [FILE]...

DESCRIPTION
       List  information  about the FILEs (the current directory by default).  Sort entries alphabetically if none of
       -cftuvSUX nor --sort is specified.

       Mandatory arguments to long options are mandatory for short options too.

       -a, --all
              do not ignore entries starting with .

       -A, --almost-all
              do not list implied . and ..

       --author
              with -l, print the author of each file

       -b, --escape
              print C-style escapes for nongraphic characters

       --block-size=SIZE
              with -l, scale sizes by SIZE when printing them; e.g., '--block-size=M'; see SIZE format below

 Manual page ls(1) line 1 (press h for help or q to quit)
```


## Filesystem Interaction

| Command | Full Name       | Purpose                         |
|---------|-----------------|---------------------------------|
| touch   | touch           | Create file                     |
| mkdir   | make directory  | Create a folder                 |
| cp      | copy            | Copy a file or folder           |
| mv      | move            | Move a file or folder           |
| rm      | remove          | Remove a file or folder         |
| file    | file            | Determine the type of a file    |

Similarly to using cat, we can provide full file paths, `directory1/directory2/note` for all of these commands.

### Creating Files and Folders (touch, mkdir)
Creating files and folders on Linux is a simple process.

The touch command takes exactly one argument: the name we want to give the file we create. For example, we can create the file "note" by using `touch note.`

It's worth noting that touch simply creates a blank file. We would need to use commands like `echo` or text editors such as nano to add content to the blank file.

```bash
user12@linux1:~$ touch note
user12@linux1:~$ ls
folder1 note
```

This is a similar process for making a folder, which just involves using the `mkdir` command and again providing the name that we want to assign to the directory. For example, creating the directory "mydirectory" using `mkdir mydirectory.`

```bash
user12@linux1:~$ mkdir mydirectory
user12@linux1:~$ ls
folder1 mydirectory note
```

### Removing Files and Folders (rm)

We can simply remove files by using `rm`. However, you need to provide the `-R` switch alongside the name of the directory you wish to remove.

```bash
user12@linux1:~$ rm -R note
user12@linux1:~$ ls
folder1 mydirectory 
```

```bash
user12@linux1:~$ rm -R mydirectory
user12@linux1:~$ ls
folder1 
```

### Copying and Moving Files and Folders (cp,mv)

Copying and moving files is an important functionality on a Linux machine. Starting with `cp`, this command takes two arguments:

1. The name of existing file.
2. The name we wish to assign to the new file when copying.

`cp` copies the entire contents of the existing file into the new file.

```bash
user12@linux1:~$ cp note note2
user12@linux1:~$ ls
folder1 note note2
```

Moving a file takes two arguments, just like the cp command. However, rather than copying and/or creating a new file, mv will merge or modify the second file that we provide as an argument. 

Not only can you use mv to move a file to a new folder, but you can also use mv to rename a file or folder. For example, we are renaming the file "note2" to be named "note3". "note3" will now have the contents of "note2":

```bash
user12@linux1:~$ mv note2 note3
user12@linux1:~$ ls
folder1 note note3
```

### Determining File Type

What is often misleading and often catches people out is making presumptions from files as to what their purpose or contents may be. Files usually have what's known as an extension to make this easier. For example, text files usually have an extension of ".txt".

Without knowing the context of why the file is there, we don't really know its purpose, so we enter the file command. This command takes one argument. For example, we use file to confirm whether or not the "note" file in the examples is indeed a text file, like so file note.

```bash
user12@linux1:~$ file note
note: ASCII text
```


## Permissions 101

Certain users cannot access certain files or folders.

Let’s take the first column shown when using the `-l` switch.

```bash
user12@linux1:~$ ls -lh
-rw-r--r-- 1 cmnatic cmnatic 0 Feb 19 10:37 file1
-rw-r--r-- 8 cmnatic cmnatic 0 Feb 19 10:37 file2
```

This column is very important for determining certain characteristics of a file or folder and whether or not we have access to it.

A file or folder can have a couple of characteristics that determine both what actions are allowed and what user or group has the ability to perform those actions, such as the following:

- Read (r) – Allows viewing the contents of a file or listing a directory

- Write (w) – Allows modifying or deleting a file

- Execute (x) – Allows running a file as a program or entering a directory

Let´s understand the permission string:
```` 
-rw-r--r--
````

| Section | Meaning |
|--------|---------|
| `-` | File type (`-` = file, `d` = directory) |
| `rw-` | Permissions for the **owner** |
| `r--` | Permissions for the **group** |
| `r--` | Permissions for **others** |

So in this case:

- The owner can **read and write**
- The group can **only read**
- Everyone else can **only read**


### Switching between users

Switching between users on a Linux install is easy work thanks to the `su` command. Unless you are the root user (or using root permissions through sudo), then you are required to know two things to facilitate this transition of user accounts:

- The user we wish to switch to
- The user's password


The `su` command takes a couple of switches that may be of relevance. For example, executing a command once you log in or specifying a specific shell to use.

Simply, by providing the `-l` switch to `su`, we start a shell that is much more similar to the actual user logging into the system, we inherit a lot more properties of the new user, environment variables and the likes.

```bash
user12@linux1:~$ su user13
Password:
```

When using `su` to switch to `"user2"`, our new session drops us into our previous user's home directory.  

```bash
user12@linux1:~$ su -l user13
Password:
user13@linux1:~$ pwd
user13@:/home/user13$
```

Where now, after using `-l`, our new session has dropped us into the home directory of "user" automatically. 

### Understanding File Permissions in Numeric Format

In Linux, every file and directory has a set of permissions that control who can read, write, or execute it. These permissions are often displayed in symbolic format, such as:
```
rwxrwxwrx
```

This format is split into three groups:

| Section | Applies To | Example |
|--------|-------------|---------|
| First 3 | Owner | `rwx` |
| Next 3  | Group | `rwx` |
| Last 3  | Others | `rwx` |

Each letter represents a specific permission:

- `r` = read  
- `w` = write  
- `x` = execute  



### Converting Symbolic Permissions to Numbers

Each permission has a numeric value:

| Permission | Value |
|------------|-------|
| Read (`r`)    | 4 |
| Write (`w`)   | 2 |
| Execute (`x`) | 1 |


To calculate the numeric value, we add the values together for each group.

**Example:** `rwxrwxrwx`

| Group  | Permissions | Calculation | Value |
|--------|-------------|-------------|-------|
| Owner  | `rwx` | 4 + 2 + 1 | 7 |
| Group  | `rwx` | 4 + 2 + 1 | 7 |
| Others | `rwx` | 4 + 2 + 1 | 7 |

So:

```
rwxrwxrwx = 777
```

Understanding numeric permissions is important because:

- Many Linux Commands use numeric values 
- You can quickly identify security risks
- You can control who can access sensitive files

For example

```
chmod 750 system_overview.txt
```

This means:
- Owner: full access
- Group: read + execute
- Other: no access


## Common Directories


### **/etc**

This root directory is one of the most important root directories on your system. The etc folder (short for etcetera) is a commonplace location to store system files that are used by your operating system. 

For example, the sudoers file highlighted in the terminal below contains a list of the users & groups that have permission to run sudo or a set of commands as the root user.

Also highlighted below are the "passwd" and "shadow" files. These two files are special for Linux as they show how your system stores the passwords for each user in encrypted formatting called sha512.

```bash
user12@linux2:/etc ls
shadow passwd sudoers sudoers.d
```

### **/var**

The "/var" directory, with "var" being short for variable data,  is one of the main root folders found on a Linux install. 

This folder stores data that is frequently accessed or written by services or applications running on the system. For example, log files from running services and applications are written here (/var/log), or other data that is not necessarily associated with a specific user (databases and the like).

```bash
user12@linux2:/var ls
backups log opt tmp
```

### **/root**

Unlike the /home directory, the /root folder is actually the home for the "root" system user. 

There isn't anything more to this folder other than just understanding that this is the home directory for the "root" user. But, it is worth a mention as the logical presumption is that this user would have their data in a directory such as "/home/root" by default.  
```
user12@linux2:~# ls
myfile myfolder passwords.xlsx
````

### **/tmp**

This is a unique root directory found on a Linux install. Short for "temporary"

The /tmp directory is volatile and is used to store data that is only needed to be accessed once or twice. Similar to the memory in computer, once the computer is restarted, the contents of this folder are cleared out.

Any user can write to this folder by default. Meaning once we have access to a machine, it serves as a good place to store things like our enumeration scripts.
```
root@linux2:/tmp# ls
todelete trash.txt rubbish.bin
```