# Windows Fundamentals Part 2

## System Configuration and Advanced System Settings

### System Configuration

The **System Configuration** utility (`msconfig`) is a tool used for advanced troubleshooting. Its primary purpose is to help diagnose and resolve startup issues.

There are several ways to launch System Configuration. One common method is through the Start Menu, you need local administrator rights to open this utility. 

The System Configuration utility has five tabs across the top:

1. General  
2. Boot  
3. Services  
4. Startup  
5. Tools  

#### General Tab

In the **General** tab, we can choose what devices and services Windows should load during startup. The available options are:

- **Normal startup** – Loads all device drivers and services  
- **Diagnostic startup** – Loads only basic devices and services (used for troubleshooting)  
- **Selective startup** – Allows you to choose which services and startup items to load  

#### Boot Tab

The **Boot** tab allows you to configure various boot options for the operating system, such as:

- Safe Mode  
- Boot logging  
- Timeout settings  
- Default operating system selection  

This tab is commonly used for advanced troubleshooting.

#### Services Tab

The **Services** tab lists all services configured on the system, regardless of whether they are currently running or stopped.

A **service** is a special type of application that runs in the background and typically does not require user interaction.

From this tab, you can enable or disable services to help diagnose startup issues.

#### Startup Tab

In modern versions of Windows, the **Startup** tab in `msconfig` does not directly manage startup programs.

Microsoft recommends using **Task Manager (`taskmgr`)** to enable or disable startup applications instead.

The System Configuration utility is primarily a troubleshooting tool and is **not intended to be a startup management program**.


### Advanced System Settings

Windows gives you some additional configuration settings as well, which you can use to control the performance behavior and system recovery. To access this option, you can search for `View advanced system settings` in your search bar and open it. This will open a `System Properties panel`

Windows uses a page file as an extra virtual memory space when the physical RAM becomes full. This helps to prevent slowdowns or application crashes when the system runs out of memory. You can view or modify the page file by navigating to the `Advanced` option at the top and clicking `Settings` under the `Performance` tab.

In the Performance tab, the Advanced option can also provide information about the page file size configured for the drives. The settings shown here can give you the following details:

- The drive where the page file is stored  
- The initial size (in MB)  
- The maximum size  
- Whether Windows manages the size automatically  

Another useful configuration that you can find in Advanced System Settings is called `Startup and Recovery`.

Windows can create a crash dump file whenever it encounters a critical error, such as a Blue Screen of Death (BSOD). This crash dump helps administrators or analysts understand what went wrong during the crash. You can view or modify the crash dump settings by navigating to the `Advanced` tab and then clicking `Settings` under the `Startup and Recovery` section.

Here, you will find different settings for Startup and Recovery. The "Write debugging information" dropdown shows the type of crash dump configured for the system.

Windows supports different dump types, such as:

- Automatic memory dump  
- Kernel memory dump  
- Small memory dump (256 KB)  
- Complete memory dump  
- None  

This setting determines how much information Windows will save in the crash dump when a system crash occurs.

## Change UAC Settings

The UAC settings can be changed or even turned off entirely (not recommended). You can move the slider to see how the setting changes UAC behavior and Microsoft’s recommended security stance for each level.

This slider has four security levels, each controlling how Windows alerts you when apps or users attempt to make system-level changes. They fall into four standard categories, explained below:

**Always notify:**  
This is the highest security level. Windows notifies you whenever apps or you yourself try to make changes, and the desktop dims (Secure Desktop).

**Notify for apps:**  
Windows notifies you only when apps try to make changes, but not when you change Windows settings. This option is enabled by default.

**Notify without dimming:**  
Same as above (Notify for apps), but the screen does not dim.

**Never notify:**  
Notifications are turned off. Windows will not warn you about any changes made by you or by applications.

You can determine the current level by checking the position of the slider in the User Account Control settings window.

 
## Computer Management

The **Computer Management** utility has three primary sections: System Tools, Storage, and Services and Applications.

The command to open Computer Management in Windows is `compmgmt.msc`.

### System Tools

#### **Task Scheduler**

With this tool, we can create and manage tasks that our computer will carry out automatically at specified times.

A task can run an application, a script, or another command, and it can be configured to run under various conditions. For example, a task can run at logon or logoff. Tasks can also be scheduled to run at specific intervals, such as every five minutes.

To view the scheduled tasks present on the system, click **Task Scheduler Library**. This will display all scheduled tasks on the system. You can click on any task to view its details.


#### **Event Viewer**

Event Viewer allows us to view events that have occurred on the computer. These event records act as an audit trail that helps us understand the activity of the system. This information is commonly used to diagnose problems and investigate actions performed on the computer.

Event Viewer has three panes:

1. The pane on the left provides a hierarchical tree listing of the event log providers (as shown in the image above).
2. The pane in the middle displays a general overview and summary of the events for the selected provider.
3. The pane on the right is the Actions pane.

There are five types of events that can be logged:

The following table outlines the five event types used in event logging.

| Event type     | Description |
|---------------|------------|
| **Error** | Indicates a significant problem that results in loss of data or functionality. For example, if a service fails to load during system startup, an Error event is generated. |
| **Warning** | Indicates a potential issue that does not immediately impact functionality but may lead to problems in the future. For example, when available disk space is low, a Warning event is generated. If an application can recover from an event without data loss or service interruption, it is typically classified as a Warning. |
| **Information** | Represents the successful operation of an application, driver, or service. For example, when a network driver loads successfully, an Information event may be recorded. Logging an Information event each time a desktop application starts is generally considered unnecessary. |
| **Success Audit** | Records a successful security-related action that is being audited. For example, a user’s successful logon attempt is logged as a Success Audit event. |
| **Failure Audit** | Records a failed security-related action that is being audited. For example, if a user attempts to access a network resource and the attempt fails, it is logged as a Failure Audit event. |

---

The standard logs are visible under **Windows Logs**. The event log contains the following standard logs, as well as custom logs:

| Log | Description |
|------|------------|
| **Application** | Contains events logged by applications. For example, a database application might record a file error. The application developer determines which events are recorded in this log. |
| **Security** | Contains events such as successful and failed logon attempts, as well as events related to resource usage, including creating, opening, or deleting files and other objects. An administrator can enable auditing to record events in the Security log. |
| **System** | Contains events logged by system components, such as the failure of a driver or other system component to load during startup. |
| **Custom Log** | Contains events logged by applications that create a custom log. Using a custom log allows an application to control log size or apply Access Control Lists (ACLs) for security purposes without affecting other applications. |
---
#### **Shared Folders**

Shared Folders displays a complete list of shared folders and resources that other users can connect to. As with any object in Windows, we can right-click a folder to view its properties, such as **Permissions** (which define who can access the shared resource).

Under **Sessions**, you will see a list of users who are currently connected to the shared resources. In this VM, no users are connected to the shares. All folders and/or files accessed by connected users are listed under **Open Files**.

The **Local Users and Groups** section should be familiar from Windows Fundamentals 1, as it corresponds to `lusrmgr.msc`.

Under **Performance**, we will find a utility called **Performance Monitor (perfmon)**.

Perfmon is used to view performance data either in real time or from a log file. This utility is useful for troubleshooting performance issues on a computer system, whether local or remote.

#### **Device Manager**

Device Manager allows us to view and configure the hardware, such as disabling any hardware attached to the computer.


#### **Storage**

Under Storage is Windows Server Backup and Disk Management.

Disk Management is a system utility in Windows that enables you to perform advanced storage tasks.  Some tasks are:

1. Set up a new drive
2. Extend a partition
3. Shrink a partition
4. Assign or change a drive letter (ex. E:) 


### Services and Application

A service is a special type of application that runs in the background.

You can view all services and their current status by clicking the **Services** option under the **Services and Applications** section.

To obtain more information about a specific service, right-click the service and select **Properties**. This will display additional details, such as:

- The service name (which differs from the display name)
- The path to the executable file
- The startup type
- Other relevant configuration information

Within the service’s **Properties** window, there is a field called **Startup type**. This setting determines how and when the service starts.

A service can be configured as:

- **Automatic** — The service starts automatically every time the system boots.
- **Manual** — The service starts only when triggered by another process or by a user.
- **Disabled** — The service is prevented from running.


## System Information

The **System Information** (`msinfo32`) tool collects detailed information about your computer and provides a comprehensive overview of its hardware, system components, and software environment. This information can be used to diagnose and troubleshoot system-related issues.

The  information in System Summary is divided into three sections:

1. Hardware Resources
2. Components
3. Software Environment

**System Summary** displays general technical specifications of the computer, such as the processor brand and model.

Under **Components**, you can view detailed information about the hardware devices installed on the system. Some sections may not display any data, while others, such as **Display** and **Input**, typically contain relevant information.

In the **Software Environment** section, you can find details about software integrated into the operating system, as well as applications that have been installed. This section also includes additional information, such as **Environment Variables** and **Network Connections**.


## Resource Monitor

**Resource Monitor** (`resmon`) is a Windows utility that provides detailed information about system resource usage, including per-process and overall CPU, memory, disk, and network activity. It also shows which processes are using specific file handles and modules. The tool offers advanced filtering capabilities that allow users to isolate data for particular processes (applications or services), as well as start, stop, pause, or resume services and close unresponsive applications directly from the interface. 

Additionally, it includes a process analysis feature that helps identify deadlocks and file locking conflicts, enabling users to troubleshoot issues without necessarily terminating applications and risking data loss. This utility is primarily intended for advanced users who need to perform in-depth system troubleshooting.

In the Overview tab, Resmon has four sections:
- CPU
- Disk
- Network
- Memory

## Command Prompt

In early operating systems, the command line was the only method available for interacting with the system.

When the GUI (Graphical User Interface) was introduced, it allowed users to perform complex tasks with just a few clicks, instead of manually entering commands in the command prompt. Although the GUI is now the primary method of interacting with the operating system, users can still interact with the system through the command prompt.

There are some basic commands that are important to know at the beginning, such as `hostname` and `whoami`.

The `hostname` command displays the name of the computer.


```
C:User\Administrator>hostname
User123
```
The `whoami` command displays the fully qualified name of the currently logged-in user (including the domain or computer name).

```
C:\Users\Administrator> whoami
user123\administrator
```

A command used often is `ipconfig`. This command will show the network address settings for the computer.

```
C:\Users\Administrator> ipconfig

Windows IP Configuration

Ethernet adapter Ethernet:

Connection-specific DNS Suffix . : eu-xxxx.internal
Link-local IPv6 Address . . . . . : fe80::6486:c81a:3db5:a0ed%7
IPv4 Address. . . . . . . . . . . : 10.10.xx.xx
Subnet Mask . . . . . . . . . . . : 255.255.0.0
Default Gateway . . . . . . . . . : 10.10.xx.xx
``` 

Each command includes a help manual that explains the correct syntax required to execute it properly, along with any additional parameters that can be used to extend its functionality.

To access the help manual for a command in Windows, you can use the `/ ?` switch.For example, to view the help manual for `ipconfig`, use the following command: `ipconfig /?`

The next command is `netstat`. According to its help manual, this command displays protocol statistics and current TCP/IP network connections.

```
C:\Users\Administrator> netstat

Active Connections

Proto Local Address Foreign Address State
TCP 10.10.xx.xx:3389 ip-10-13-xx-xx:38150 ESTABLISHED

C:\Users\Administrator> netstat /?

Displays protocol statistics and current TCP/IP network connections.

NETSTAT [-a] [-b] [-e] [-f] [-n] [-o] [-p proto] [-r] [-s] [-x] [-t] [interval]
```
The last line shows an example of the command’s syntax.

The structure indicates that the `netstat` command can be executed by itself or with additional parameters, such as `-a`, `-b`, `-e`, and others.

When parameters are appended to the root command (`netstat` in this case), the output changes accordingly. You can experiment with different parameters to observe how the results vary.

| Parameter | Description |
|------------|------------|
| `-a` | Displays all active connections and listening ports. |
| `-b` | Displays the executable involved in creating each connection or listening port (requires administrative privileges). |
| `-e` | Displays Ethernet statistics (such as bytes sent and received). |
| `-f` | Displays fully qualified domain names (FQDN) for foreign addresses. |
| `-n` | Displays addresses and port numbers in numerical form (does not resolve DNS names). |
| `-o` | Displays the owning Process ID (PID) associated with each connection. |
| `-p proto` | Shows connections for the specified protocol (e.g., TCP, UDP, TCPv6, UDPv6). |
| `-r` | Displays the routing table. |
| `-s` | Displays per-protocol statistics (e.g., TCP, UDP, ICMP). |
| `-x` | Displays NetworkDirect connections, listeners, and shared endpoints. |
| `-t` | Displays the current connection offload state. |
| `[interval]` | Redisplays selected statistics at a specified interval (in seconds). |


The `net` command is primarily used to manage network resources. This command supports multiple sub-commands.

If you type `net` without specifying a sub-command, the output will display the root command syntax along with a list of available sub-commands you can use.


## Registry Editor

The **Windows Registry** (`regedit`) is a central hierarchical database used to store configuration information required by the operating system, applications, hardware devices, and one or more users.

The Registry contains information that Windows continuously references during operation, including:

- Profiles for each user
- Applications installed on the system and the file types they are associated with
- Property sheet settings for folders and application icons
- Hardware installed on the system
- Ports currently in use

The registry is for advanced computer users. Making changes to the registry can affect normal computer operations. 

