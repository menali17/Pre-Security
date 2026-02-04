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

- SIGTERM - Kill the process, but allow it to do some cleanup taks beforehand
- SIGKILL - Kill the process - doesn´tdo any cleanup after the fact
- SIGSTOP - Stop/suspend a process

### How do Processes Start?

The Operating System (OS) uses namespaces to ultimately split up the resources available on the computer to (such as CPU, RAM and priority) processes. Namespaces are great for security as it is a way of isolating processes from another, only those that are in the same namespace will be able to see each other.

The process with an ID of **1** is the process that starts when the system boots. On Ubuntu systems, this process is usually **systemd**, which is responsible for managing services and processes. It acts as a bridge between the operating system and user-level programs.

When the system finishes booting, `systemd` is one of the first processes to start. Any program or service that runs afterward typically starts as a **child process** of `systemd`.

This means that while these programs run as independent processes, they are ultimately managed by `systemd`. This structure helps the system organize, monitor, and control running services more effectively.
```
PID USER   PR NI  VIRT   RES   SHR S  %CPU %MEM    TIME+ COMMAND
1   root   20  0 101800 11340 8400 S   0.0  1.1   0:11.74 systemd
```

### Getting Processes/Services to Start on Boot

Some applications can be configured to start automatically when the system boots. Examples include web servers, database servers, or file transfer servers. This software is often critical, so administrators set it to start during the system’s boot process.

In this example, we’ll manually start the Apache web server and then configure the system to launch `apache2` automatically at boot.

To do this, we use the `systemctl` command. This command allows us to interact with the `systemd` process (the system and service manager).

The basic format of the command is: `systemctl [option] [service]`

For example, to tell apache to start up, we'll use `systemctl start apache2`. Same with if we wanted to stop apache, we'd just replace the [option] with stop (instead of start like we provided).

We can do five options with the `systemctl`:
- Start
- Stop
- Enable
- Disable
- Status

### An Introduction to Backgrounding and Foregrouding in Linux

Processes can run in two states: **foreground** and **background**.

Commands we normally run in the terminal, such as `echo`, run in the **foreground**. This means the terminal waits for the command to finish and shows the output directly to you.

For example:
```
root@linux3:~# echo "Hello World"
Hello World
```
Here, the command runs in the foreground, and we immediately see the output.

If we add the `&` operator, the process runs in the **background**:

```
root@linux3:~# echo "Hello World" &
[1] 16889
root@linux3:~# Hello World
```

Instead of showing the output right away, the terminal returns a **job number** (`[1]`) and a **PID** (`16889`). This indicates that the process is now running in the background.

Because it is running in the background, the terminal becomes available for new commands immediately, rather than waiting for the previous one to finish.

Running processes in the background is especially useful for long-running tasks, such as copying large files. This allows us to continue using the terminal for other commands without having to wait for the file transfer to finish.

We can achieve something similar when running scripts or commands interactively. Instead of starting them with the `&` operator, we can press **Ctrl + Z** on the keyboard to suspend (pause) the current process.

When we press **Ctrl + Z**:

- The process is stopped (paused)
- It is moved into the background
- The terminal becomes available for new commands

This is an effective way to temporarily pause a script or command without terminating it.

### Foregrounding a Processps

Now that we have a process running in the background, for example, our script `background.sh`, which we can confirm using the `ps aux` command, we can bring this process back to the foreground to interact with it again.
```
root      19802  0.9  0.3   8616  3108 pts/1    T    15:37   0:01 /bin/bash ./background.sh
root      20995  0.0  0.0      0     0 ?        I    15:40   0:00 [kworker/u30:1-events_unbound]
ubuntu    21007  0.0  0.0   7228   592 ?        S    15:40   0:00 sleep 1
root      21008  0.0  0.3  10616  3452 pts/1    R+   15:40   0:00 ps aux
```

After sending a process to the background using either **Ctrl + Z** or the `&` operator, we can use the `fg` command to bring it back to the foreground.

When `fg` is used, the selected background job returns to the terminal, and we can see the script’s output and interact with it again as if it had never been paused.
```
root@linux3:/var/opt# fg
```

The `fg` command resumes the most recent background or stopped job and attaches it back to the current terminal session. If multiple jobs exist, a specific job can be resumed using its job number, for example:`fg %1`

If no background or stopped jobs exist, the shell will return an error such as: `fg: no such job`

## Maintaining Your System: Automation

Users may want to schedule a certain action or task to take place after the system has booted. Take, for example, running commands, backing up files, or launching programs such as Spotify or Google Chrome.

We're going to be talking about the cron process, but more specifically, how we can interact with it through the use of crontabs. Crontab is one of the processes that is started during boot and is responsible for facilitating and managing cron jobs.

A crontab is simply a special file with formatting that is recognised by the cron process to execute each line step-by-step. Crontabs require 6 specific values:

| Value | Description |
|------|-------------|
| MIN  | What minute to execute at |
| HOUR | What hour to execute at |
| DOM  | What day of the month to execute at |
| MON  | What month of the year to execute at |
| DOW  | What day of the week to execute at |
| CMD  | The actual command that will be executed |

Let's use the example of backing up files. You may wish to backup "cmnatic"'s  "Documents" every 12 hours. We would use the following formatting: 
```
0 */12 * * * cp -R /home/cmnatic/Documents /var/backups/
```

An interesting feature of crontabs is that these also support the wildcard or asterisk (*). If we do not wish to provide a value for that specific field, i.e. we don't care what month, day, or year it is executed., only that it is executed every 12 hours, we simply just place an asterisk.

Crontabs can be edited by using `crontab -e`, where you can select an editor (such as Nano) to edit your crontab.


## Maintaining Your System: Package Management

### Introducing Packages & Software Repos

When developers wish to submit software to the community, they will submit it to an  "apt" repository. If approved, their programs and tools will be released into the wild. Two of the most redeeming features of Linux shine to light here: User accessibility and the merit of open source tools.

When using the `ls` command on a Ubuntu 20.04 Linux machine, these files serve as the gateway/registry. 

```bash
ubuntu@ip-10-10-29-121:/etc/apt$ ls
apt.conf.d  auth.conf.d  preferences.d  sources.list  sources.list.d  trusted.gpg.d
ubuntu@ip-10-10-29-121:/etc/apt$
``` 

Whilst Operating System vendors will maintain their own repositories, you can also add community repositories to your list. This allows you to extend the capabilities of your OS. Additional repositories can be added by using the `add-apt-repositorycommand` or by listing another provider. For example, some vendors will have a repository that is closer to their geographical location.

### Managing Your Repositories (Adding and Removing)

Normally we use the `apt` command to install software onto our Ubuntu system. The `apt` command is part of the package management software also named APT. APT contains a whole suite of tools that allows us to manage software packages and their sources, as well as install or remove software.

While you can install software using package installers such as `dpkg`, the benefit of APT is that whenever we update our system, the repositories that contain the software we added are also checked for updates automatically.

For example, we're can add the text editor **Sublime Text** to our Ubuntu machine as a repository, since it is not part of the default Ubuntu repositories. When adding software, the integrity of what we download is guaranteed through the use of **GPG (GNU Privacy Guard) keys**. These keys act as a safety check from the developers, essentially saying, *"this software is really from us."* If the keys do not match what your system trusts and what the developers used to sign the software, the download and installation will be blocked.


## Maintaining Your System: Logs

These files and folders contain logging information for applications and services running on your system. The Operating System  (OS) has become pretty good at automatically managing these logs in a process that is known as "rotating".

These services and logs are a great way in monitoring the health of your system and protecting it. Not only that, but the logs for services such as a web server contain information about every single request - allowing developers or administrators to diagnose performance issues or investigate an intruder's activity. For example, the two types of log files below that are of interest:
- Access log
- Error log

There are, of course, logs that store information about how the OS is running itself and actions that are performed by users, such as authentication attempts.

```
ubuntu@ip-172-31-23-158:/var/log/apache2$ ls
access.log        access.log.3.gz   access.log.10.gz  access.log.11.gz  access.log.12.gz  access.log.13.gz  access.log.14.gz  access.log.2.gz  access.log.4.gz  access.log.5.gz  access.log.6.gz  access.log.7.gz  access.log.8.gz  access.log.9.gz
error.log         error.log.1       error.log.10.gz   error.log.11.gz   error.log.12.gz   error.log.13.gz   error.log.14.gz   error.log.2.gz   error.log.3.gz   error.log.4.gz   error.log.5.gz   error.log.6.gz   error.log.7.gz   error.log.9.gz
other_vhosts_access.log
ubuntu@ip-172-31-23-158:/var/log/apache2$
```
