# Introduction to Windows

The Windows operating system (OS) is a complex product with many system files, utilities, settings, features, etc. 

## The File System

The file system used in modern versions of Windows is the **New Technology File System (NTFS)**. Before NTFS, older file systems such as **FAT16/FAT32** (File Allocation Table) and **HPFS** (High Performance File System) were used.

We still see FAT partitions in use today. For example, FAT is commonly used on USB drives, MicroSD cards, and other removable storage devices, but it is not typically used on modern Windows computers or Windows servers.

NTFS is known as a **journaling file system**. In the event of a failure, the file system can automatically repair folders and files on disk using information stored in a log file. This recovery feature is not available with FAT file systems.

NTFS addresses many of the limitations of previous file systems, including:

- Support for files larger than 4GB  
- The ability to set specific permissions on files and folders  
- File and folder compression  
- File system encryption

On NFTS volumes, you can set permissions that grant or deny access to files and folders.

| Permission | Meaning for Folders | Meaning for Files |
|------------|---------------------|-------------------|
| **Read** | Permits viewing and listing of files and subfolders | Permits viewing or accessing the file’s contents |
| **Write** | Permits adding files and subfolders | Permits writing to a file |
| **Read & Execute** | Permits viewing and listing of files and subfolders as well as executing files; inherited by files and folders | Permits viewing and accessing the file’s contents as well as executing the file |
| **List Folder Contents** | Permits viewing and listing of files and subfolders as well as executing files; inherited by folders only | N/A |
| **Modify** | Permits reading and writing of files and subfolders; allows deletion of the folder | Permits reading and writing of the file; allows deletion of the file |
| **Full Control** | Permits reading, writing, changing, and deleting of files and subfolders | Permits reading, writing, changing, and deleting of the file |

Another feature of NTFS is **Alternate Data Streams (ADS)**. ADS is a file attribute specific to the Windows NTFS file system.

Every file has at least one data stream (`$DATA`), but ADS allows files to contain more than one stream of data. By default, Windows Explorer does not display alternate data streams to the user. However, third-party tools can be used to view ADS, and PowerShell also provides the ability to inspect alternate data streams associated with files.

From a security perspective, ADS has been abused by malware authors to hide malicious data within files, making it less visible to users and some security tools.

## The Windows\System32 Folders
The Windows folder (`C:\Windows`) is traditionally known as the directory that contains the Windows operating system files. However, it does not strictly have to reside on the C: drive. Technically, it can exist on another drive or even within a different folder structure.

This is where **environment variables** come into play, more specifically, **system environment variables**.

One important system environment variable is `%windir%`, this variable points to the location of the Windows directory, regardless of where it is installed on the system. Programs use `%windir%` so they can reliably find system files without needing to know the exact drive or folder path.
 
The System32 folder holds the important files that are critical for the operating system, we should proceed with extreme caution when interacting with this folder. Accidentally deleting any files or folders within System32 can render the Windows OS inoperational.

## User Accounts, Profiles, and Permissions

User accounts can be one of two types on a typical local Windows system: Administrator & Standard User. 

The user account type will determine what actions the user can perform on that specific Windows system:
- An Administrator can make changes to the system: add users, delete users, modify groups, modify settings on the system, etc.
- A Standard User can only make changes to folders/files attributed to the user & can't perform system-level changes, such as install programs.

When a user account is created, a profile is created for the user. The location for each user profile folder will fall under is C:\Users.

For example, the user profile folder for the user account Max will be C:\Users\Max.

The user profile is created the first time the user logs in. During this initial login, Windows prepares the profile by setting up folders, default settings, and configuration files.

We may notice messages such as **"User Profile Service"** on the login screen during this process. This indicates that Windows is working in the background to create and configure the new user’s profile.

Another way to access this information, and then some, is using Local User and Group Management. Right-click on the Start Menu and click Run(Windows + R). Type `lusrmgr.msc.` 

We should see two folders: Users and Groups.  If you click on Groups, you see all the names of the local groups along with a brief description for each group. 

Each group has permissions set to it, and users are assigned/added to groups by the Administrator. When a user is assigned to a group, the user inherits the permissions of that group. A user can be assigned to multiple groups.

## User Account Control (UAC)

Most home users are logged into their Windows systems using accounts that have **local administrator** privileges. An account with administrator rights can make significant changes to the system.

However, users do not need elevated (high-level) privileges to perform everyday tasks such as browsing the internet or working on documents. Running with elevated privileges all the time increases the risk of system compromise because malware executed under an administrator account would also gain those powerful permissions.

To help reduce this risk, Microsoft introduced **User Account Control (UAC)**.

When a user with an administrator account logs in, their session does not run with full elevated privileges by default. Instead, Windows runs most tasks with standard user permissions.  

If an action requires higher-level privileges, such as installing software or modifying system settings, the user is prompted to confirm whether they want to allow the operation to proceed. This prompt is known as the **UAC prompt**.

UAC helps prevent unauthorized or accidental changes to the system by requiring user approval before sensitive actions are performed.

# Settings and the Control Panel

On a Windows system, the primary places to make system changes are the **Settings** menu and the **Control Panel**.

For many years, the Control Panel was the main location used to manage system settings, such as adding a printer or uninstalling a program.

The **Settings** menu was introduced in Windows 8, which was designed with touchscreen devices in mind, and it continues to be used in Windows 10 and later. Today, Settings is the primary location most users go to when they want to change system options.

If you want to see which applications are installed on a Windows system using the Control Panel:

1. Open the **Control Panel**  
2. Click on **Programs**  
3. Select **Programs and Features**

This will display a list of installed applications along with details such as their names, publishers, and versions. This can help you identify and verify software that has been installed on the system.


## Task Manager

The Task Manager provides information about the applications and processes currently running on the system. Other information is also available, such as how much CPU and RAM are being utilized, which falls under Performance. 

The keyboard shortcut to open Task Manager is CTRL + Shift + ESC