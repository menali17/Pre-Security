# Introduction to Linux

## A bit of Background on Linux

Linux is an **open-source operating system kernel** created by **Linus Torvalds in 1991**. Over time, developers around the world built full operating systems around this kernel, these are known as **Linux distributions (distros)**.

Unlike proprietary systems such as Windows or macOS, Linux is:
- Open-source  
- Highly customizable  
- Known for stability and security  
- Widely used in servers and cybersecurity  

### Where is Linux used?

Linux powers things such as: 
- Websites that you visit (most web servers run Linux)
- Android smartphones (Android is Linux-based)
- Car entertainment/control panels  
- Point of Sale (PoS) systems such as checkout tills and registers in shops  
- Critical infrastructures such as traffic light controllers or industrial sensors  
- Cloud platforms and data centers  
- Cybersecurity and penetration testing systems  

Linux is especially popular in environments where **stability, performance, and security** are important.

### Flavours of Linux

The name "Linux" is actually an umbrella term for multiple OS's that are based on UNIX (another operating system). Thanks to Linux being open-source, variants of Linux come in all shapes and sizes — suited best for what the system is being used for.

For example, Ubuntu & Debian are some of the more commonplace distributions of Linux because they are so extensible. You can run Ubuntu as a server (such as websites & web applications) or as a fully-fledged desktop.

Other examples include:

- **Linux Mint** – Beginner-friendly, similar feel to Windows  
- **Kali Linux** – Used for cybersecurity and penetration testing  
- **Red Hat / Rocky Linux / AlmaLinux** – Common in enterprise and servers  
- **Arch Linux** – Lightweight and highly customizable (advanced users)  

Each distro is built for a different purpose, but they all share the **Linux kernel** at their core.

## Running First Commands

A large selling point of using OSs such as Ubuntu is how lightweight they can be. This, of course, doesn't come without its disadvantages, where for example, often there is no GUI (Graphical User Interface) or what is also known as a desktop environment that we can use to interact with the machine (unless it has been installed). A large part of interacting with these systems is using the "Terminal".

| Command | Description |
|---------|-------------|
| echo    | Output any text that we provide |
| whoami  | Find out what user we're currently logged in as |

The snippets below show an example of each command being used.

### Using echo

```bash
user12@linux1:~$ echo Hello
Hello

user12@linux1:~$ echo "Hello Friend!"
Hello Friend!
```

As shown in the terminal above, if we want to "echo" a single word, we don't need to use double quotes, for example, `echo Hello`. However, the string should be enclosed within double quotes if one or more spaces are present, for example, echo `"Hello Friend!"`.

`Whoami` can be used to find the username we are logged in as.

```bash
user12@linux1:~$ whoami
user12
```

## Interacting With the FileSystem

| Command | Description |
|---------|-------------|
| ls    | Listing |
| cd | Changing directory |
|  cat | concatenate
| pwd | print working directory

### Listing Files in our Current Directory (ls)

Before we can do anything such as finding out the contents of any files or folders, we need to know what exists in the first place. This can be done using the "ls" command. 

```bash
user12@linux1:~$ ls
'Important Files' 'My Documents' Notes Pictures
```

In the screenshot above, we can see there are the following directories/folders:

- Important Files
- My Documents
- Notes
- Pictures

You can list the contents of a directory without having to navigate to it by using ls and the name of the directory. I.e. ls `Pictures`

### Changing Our Current Directory (cd)
Now that we know what folders exist, we need to use the "cd" command (short for change directory) to change to that directory. Say if I wanted to open the "Pictures" directory, I'd do "cd Pictures". Where again, we want to find out the contents of this "Pictures" directory and to do so, we'd use "ls" again:

```bash
user12@linux1:~$/Pictures ls
dog_picture1.jpg dog_picture2.jpg dog_picture3.jpg dog_picture4.jpg
```

### OutPuting the Contents of a File (cat)

"Cat" is short for concatenating and is a good way for us to output the contents of files (not just text files)

In the terminal below, we can see how we have combined the use of "ls" to list the files within a directory called "Documents":

```bash
user12@linux1:~$/Documents ls
todo.txt
user12@linux1:~$/Documents cat todo.txt
Important tasks to do later
```

You can use cat to output the contents of a file within directories without having to navigate to it by using cat and the name of the directory. I.e. `cat /home/ubuntu/Documents/todo.txt`

Sometimes things like usernames, passwords, flags or configuration settings are stored within files where "cat" can be used to retrieve these.

Cat can read just files, not folders.

### Finding out the full Path to our Current Working Directory (pwd)

it's easy to lose track of where we are on the filesystem exactly, which is why we use "pwd". This stands for print working directory.

Using the example machine from before, we are currently in the "Documents" folder, but where is this exactly on the Linux machine's filesystem? We can find this out using this "pwd" command like within the screenshot below:

```bash
user12@linux1:~$/Documents pwd
/home/ubuntu/Documents
user12@linux1:~/Documents$
```

## Searching for files

One of the redeeming features of Linux is truly how efficient you can be with it. With that said, you can only be as efficient as you are familiar with it. As you interact with OSs such as Ubuntu over time, essential commands like those covered will start to become muscle-memory.

### Using Find

The find command is fantastic in the sense that it can be used both very simply or rather complex depending upon what it is you want to do exactly.

```bash
user12@linux1:~$ ls
Desktop Documents Pictures folder1
```

Directories can contain even more directories within themselves. It becomes a headache when we're having to look through every single one just to try and look for specific files. 

We can use find to do just this for us.

Let's assume that we already know the name of the file we're looking for, but can't remember where it is exactly. In this case, we're looking for `passwords.txt`

If we remember the filename, we can simply use find -name passwords.txt where the command will look through every folder in our current directory for that specific file like so:

```bash
user12@linux1:~$ find -name passwords.txt
./folder1/passwords.txt
```

Let's say that we don't know the name of the file, or want to search for every file that has an extension such as ".txt". 

We can simply use what's known as a wildcard (*) to search for anything that has .txt at the end. In our case, we want to find every .txt file that's in our current directory. We will construct a command such as `find -name *.txt` . Where "Find" has been able to find every .txt file and has then given us the location of each one:

```bash
user12@linux1:~$ find -name .txt
./folder1/passwords.txt
./Documents/todo.txt
```

## Using Grep

the `grep` command allows us to search the contents of files for specific values that we are looking for.

Taking for example, the access log of a web server. In this case, the access.log of a web server has 244 entries (using "wc" to count the number of entries in "access.log"):

```bash
user12@linux1:~$ wc -l acess.log
244 access.log
```

 Let's say for example if we wanted to search this log file to see the things that a certain user/IP address visited. Looking through 244 entries isn't all that efficient considering we want to find a specific value.

We can use grep to search the entire contents of this file for any entries of the value that we are searching for. Going with the example of a web server's access log, we want to see everything that the IP address "81.143.211.90" has visited

```bash
user12@linux1:~$ grep "81.143.211.90" access.log"
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"
```

## Searching Recursively with Grep

Sometimes, the information we are looking for is spread across multiple files inside a directory. Instead of checking each file individually, we can tell grep to search recursively through all files and subdirectories.

To do this, we use the `-R` (recursive) option.

For example, to search for a variable across all files in the current directory and its subfolders, we can run:

```
grep -R "PRETTY_NAME" /etc/
```

This will:

- Search every file in the current directory
- Search all subdirectories
- Show where the PRETTY_NAME appears

## Introduction to Shell Operators

There are a few important operators that are worth noting.

| Symbol / Operator | Description |
|-------------------|-------------|
| `&`  | This operator allows you to run commands in the background of your terminal. |
| `&&` | This operator allows you to combine multiple commands together in one line of your terminal. The second command runs only if the first succeeds. |
| `>`  | This operator is a redirector, meaning that we can take the output from a command (such as using `cat` to output a file) and direct it elsewhere. This **overwrites** the target file. |
| `>>` | This operator does the same function as the `>` operator but **appends** the output rather than replacing it (meaning nothing is overwritten). |

### Operator "&"

This operator allows us to execute commands in the background. For example, let's say we want to copy a large file. This will obviously take quite a long time and will leave us unable to do anything else until the file successfully copies.

The "&" shell operator allows us to execute a command and have it run in the background (such as this file copy) allowing us to do other things.

### Operator "&&"

This shell operator is a bit misleading in the sense of how familiar is to its partner "&". Unlike the "&" operator, we can use "&&" to make a list of commands to run for example ``command1 && command2``. However, it's worth noting that ``command2`` will only run if ``command1`` was successful.`

### Operator ">"

This operator is what's known as an output redirector. What this essentially means is that we take the output from a command we run and send that output to somewhere else.

Let's say we wanted to create a file named "welcome" with the message "hey". We can run `echo hey > welcome` where we want the file created with the contents "hey":

```
user12@linux1:~$ echo hey > welcome
user12@linux1:~$ cat welcome
hey
```
 If the file "welcome" already exists, the contents will be overwritten.

## Operator ">>"

What makes this operator different is that rather than overwriting any contents within a file, for example, it instead just puts the output at the end.

Following on with the previous example where we have the file "welcome" that has the contents of "hey". If were to use echo to add "hello" to the file using the > operator, the file will now only have "hello" and not "hey".

The `>>` operator allows to append the output to the bottom of the file, rather than replacing the contents:

```
user12@linux1:~$ echo hello >> welcome
user12@linux1:~$ cat welcome
hey
hello
```