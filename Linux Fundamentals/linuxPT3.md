# Linux Part 3

## Terminal Text Editors

There are few options that we can use, all with a variety of friendliness and utility.

### **Nano**

To create or edit a file using nano, we simply use `nano filename`, replacing "filename" with the name of the file you wish to edit.

```
user2@linux3:/tmp# nano myfile
  GNU nano 4.8                                             myfile                                                       

^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo       M-A Mark Text
^X Exit        ^R Read File   ^\ Replace     ^U Paste Text  ^T To Spell    ^_ Go To Line  M-E Redo       M-6 Copy Text
```

Once we press enter to execute the command, `nano` will launch. Where we can just begin to start entering or modifying our text. We can navigate each line using the "up" and "down" arrow keys or start a new line using the "Enter" key on our keyboard.

```
tryhackme@linux3:/tmp# nano myfile
  GNU nano 4.8                                             myfile                                             Modified  

Hello User
I can write things into "myfile"


^G Get Help    ^O Write Out   ^W Where Is    ^K Cut Text    ^J Justify     ^C Cur Pos     M-U Undo       M-A Mark Text
^X Exit        ^R Read File   ^\ Replace     ^U Paste Text  ^T To Spell    ^_ Go To Line  M-E Redo       M-6 Copy Text
````

Nano has a few features that are easy to remember & covers the most general things you would want out of a text editor, including:

- Searching for text
- Copying and Pasting
- Jumping to the line number
- Finding out what line number we are on


We can use these features of nano by pressing the "Ctrl" key (which is represented as an ^ on Linux)  and a corresponding letter. For example, to exit, we would want to press "Ctrl" and "X" to exit Nano.

### **VIM**

VIM is a much more advanced text editor.

Some of VIM´S benefits, includes:

- Customisable - we can modify the keyboard shortcuts to be of your choosing
- Syntax Highlighting - this is useful if you are writing or maintaining code, making it a ppopular choice for software developers
- VIM works on all terminals where nano may not be installed


## General/Useful Utilities

### **Downloading Files (Wget)**

This command allows us to download files from the web via HTTP, similar to accessing a file through a web browser. We simply need to provide the address (URL) of the resource we want to download.

For example, if I wanted to download a file named "myfile.txt" onto my machine, and I knew its web address, it would look something like this:

```
wget https://assets.genericwebsite.com/additional/linux-fundamentals/part3/myfile.txt
```

### **Transferring Files From Your Host – SCP (SSH)**

Secure Copy, or **SCP**, is a method of securely copying files. Unlike the regular `cp` command, SCP allows you to transfer files between two computers using the SSH protocol, which provides both authentication and encryption.

SCP works using a **SOURCE → DESTINATION** model. It allows you to:

- Copy files and directories from your current system to a remote system  
- Copy files and directories from a remote system to your current system  

This requires that you know the username and password (or have SSH key access) for a user on both your local system and the remote system.

For example, let’s copy a file from our machine to a remote machine, as shown in the table below:

| Variable | Value |
|----------|-------|
| The IP address of the remote system | 192.168.1.30 |
| User on the remote system | ubuntu |
| Name of the file on the local system | important.txt |
| Name that we wish to store the file as on the remote system | transferred.txt |

Let's craft our scp command (remembering that the format of SCP is just SOURCE and DESTINATION):

```
scp important.txt ubuntu@192.168.1.30:/home/ubuntu/transferred.txt
```

And now let's reverse this and layout the syntax for using scp to copy a file from a remote computer that we're not logged into 

| Variable | Value |
|----------|-------|
| IP address of the remote system | 192.168.1.30 |
| User on the remote system | ubuntu |
| Name of the file on the remote system | documents.txt |
| Name that we wish to store the file as on our system | notes.txt |

The command will now look like the following: `scp ubuntu@192.168.1.30:/home/ubuntu/documents.txt notes.txt` 

### **Serving Files From Your Host – Web Server (Python)**

Ubuntu machines come pre-packaged with Python3. Python conveniently provides a lightweight and easy-to-use module called `http.server`. This module allows you to quickly turn your computer into a simple web server that can be used to host files, which can then be downloaded by another computer using tools such as `curl` or `wget`.

Python3’s `http.server` will serve the files in the directory where you run the command. This behavior can be changed using options found in the manual pages.

To start the server, simply run: `python3 -m http.server`

For an example:
```
user2@linux3:/webserver# python3 -m http.server
Serving HTTP on 0.0.0.0 port 8000 (http://0.0.0.0:8000/) ...
``` 

Now, let's use `wget` to download the file using the `10.66.175.187` address and the name of the file. Bbecause the python3 server is running port 8000, you will need to specify this within your wget command. 

For example:
 
 ```
 user2@mymachine:~# wget http://10.66.175.187:8000/myfile
```

We will need to open a new terminal to use wget and leave the one that you have started the Python3 web server in. This is because, once you start the Python3 web server, it will run in that terminal until you cancel it.

```
user2@linux3:/tmp# wget http://10.66.175.187:8000/file

2021-05-04 14:26:16  http://127.0.0.1:8000/file
Connecting to http://127.0.0.1:8000... connected.
HTTP request sent, awaiting response... 200 OK
Length: 51095 (50K) [text]
Saving to: ‘file’

file                    100%[=================================================>]  49.90K  --.-KB/s    in 0.04s

2021-05-04 14:26:16 (1.31 MB/s) - ‘file’ saved [51095/51095]
```


## Processes 101

Processes are the programs that are running on your machine. They are managed by the kernel, and each process has an ID associated with it, known as its PID (Process ID). The PID increases in the order that processes start.

### Viewing Processes

We can use the `ps` command to display a list of the running processes for our user’s session, along with additional information such as the status code, the session that started the process, how much CPU time it has used, and the name of the program or command that is being executed.

```
cmnatic@CMNatic-LPT0:~$ ps
  PID TTY          TIME CMD
  102 pts/1    00:00:00 bash
  204 pts/1    00:00:00 ps

cmnatic@CMNatic-LPT0:~$ ps
  PID TTY          TIME CMD
  102 pts/1    00:00:00 bash
  205 pts/1    00:00:00 ps
```

Notice that the `ps` process first appears with a PID of **204**, and when the command is run again, it appears with a new PID of **205**. This happens because each time you run a command, a new process is created, and the system assigns it the next available Process ID.


To see the processes run by other users and those that don't run from a session, we need to provide aux to the ps command: `ps aux`
```
cmnatic@CMNatic-THM-LPT0:~$ ps aux
USER       PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root         1  0.0  0.0    892   580 ?        Sl   Apr24   0:00 /init
root       100  0.0  0.0    892    84 ?        Ss   13:28   0:00 /init
root       101  0.0  0.0    892     8 ?        R    13:28   0:00 /init
cmnatic    102  0.0  0.0  10032  4984 pts/1    Ss   13:28   0:00 -bash
cmnatic    206  0.0  0.0  10616  3288 pts/1    R+   22:32   0:00 ps aux
```


Notice that we can now see a total of five processes. Also, we can see processes owned by different users, such as **root** and **cmnatic**.

Another very useful command is `top`. The `top` command provides real-time statistics about the processes running on your system, rather than a one-time snapshot.

These statistics refresh automatically every few seconds and will also update as you interact with the interface, such as when using the arrow keys to browse through the process list.

The `top` command is a powerful tool for gaining insight into system performance and resource usage.

``` 
top - 22:36:17 up 1 day,  6:32,  0 users,  load average: 0.00, 0.00, 0.00
Tasks: 5 total,   1 running,   4 sleeping,   0 stopped,   0 zombie
%Cpu(s): 0.0 us,  0.8 sy,  0.0 ni, 99.2 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
MiB Mem :  12630.9 total,  12206.5 free,     83.6 used,    340.9 buff/cache
MiB Swap:   4096.0 total,   4096.0 free,      0.0 used.   12360.1 avail Mem

  PID USER      PR  NI    VIRT    RES    SHR S  %CPU %MEM     TIME+ COMMAND
    1 root      20   0     892    580    516 S   0.0  0.0   0:00.93 init
  100 root      20   0     892     84     20 S   0.0  0.0   0:00.00 init
  101 root      20   0     892     84     20 S   0.0  0.0   0:00.07 init
  102 cmnatic   20   0   10032   4988   3272 S   0.0  0.0   0:00.08 bash
  209 cmnatic   20   0   10872   3704   3188 R   0.0  0.0   0:00.00 top
```

### Managing Processes

You can send signals to terminate processes. There are several types of signals, each determining how "cleanly" the kernel handles the process termination.

To stop a process, we use the appropriately named `kill` command along with the PID of the process we want to terminate. For example, to stop a process with PID 1337: kill `1337`

There are some of the signals that we can send to a process when it is killed:

- SIGNTERM - Kill the process, but allow it to do some cleanup taks beforehand
- SIGKILL - Kill the process - doesn´tdo any cleanup after the fact
- SIGSTOP - Stop/suspend a process

### How do Processes Start?
