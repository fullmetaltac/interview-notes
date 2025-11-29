# Table of Contents
- [Table of Contents](#table-of-contents)
  - [Interacting With the Filesystem](#interacting-with-the-filesystem)
    - [Basic commands](#basic-commands)
    - [Searching for Files](#searching-for-files)
  - [Shell Operators](#shell-operators)
  - [Permissions](#permissions)
    - [Users](#users)
    - [Superuser](#superuser)
    - [Groups](#groups)
    - [Ownership and Permissions](#ownership-and-permissions)
  - [Directory Structure](#directory-structure)
  - [Linux Processes](#linux-processes)
    - [Types of Linux Processes](#types-of-linux-processes)
    - [Process States](#process-states)
    - [Essential Commands](#essential-commands)
  - [References](#references)

## Interacting With the Filesystem

### Basic commands

| Command | Full Name                       | Purpose                                 |
| ------- | ------------------------------- | --------------------------------------- |
| ls      | listing                         | List directory contents                 |
| cd      | change directory                | Change current working directory        |
| cat     | concatenate                     | View or concatenate file contents       |
| pwd     | print working directory         | Show current working directory path     |
| touch   | touch                           | Create an empty file                    |
| mkdir   | make directory                  | Create a new folder                     |
| cp      | copy                            | Copy a file or folder                   |
| mv      | move                            | Move or rename a file or folder         |
| rm      | remove                          | Remove a file or folder                 |
| file    | file                            | Determine the type of a file            |
| man     | manual                          | Show the manual page for a command      |
| echo    | echo                            | Print text or variables to the terminal |
| grep    | global regular expression print | Search text using patterns              |
| head    | head                            | Show the first lines of a file          |
| tail    | tail                            | Show the last lines of a file           |
| less    | less                            | View file contents one page at a time   |
| find    | find                            | Search for files and directories        |
| which   | which                           | Show the full path of a command         |
| history | history                         | Display command history                 |
| clear   | clear                           | Clear the terminal screen               |


### Searching for Files

```shell
tryhackme@linux1:~$ find -name *.txt
./folder1/passwords.txt
./Documents/todo.txt
tryhackme@linux1:~$
```

```shell
tryhackme@linux1:~$ grep "81.143.211.90" access.log
81.143.211.90 - - [25/Mar/2021:11:17 + 0000] "GET / HTTP/1.1" 200 417 "-" "Mozilla/5.0 (Linux; Android 7.0; Moto G(4))"
tryhackme@linux1:~$
```

## Shell Operators

| Symbol / Operator | Description                                                                                                                                      |
| ----------------- | ------------------------------------------------------------------------------------------------------------------------------------------------ |
| &                 | This operator allows you to run commands in the background of your terminal.                                                                     |
| &&                | This operator allows you to combine multiple commands together in one line of your terminal.                                                     |
| >                 | This operator is a redirector - meaning that we can take the output from a command (such as using cat to output a file) and direct it elsewhere. |
| >>                | This operator does the same function of the > operator but appends the output rather than replacing (meaning nothing is overwritten).            |

## Permissions

### Users

In Linux, there are two types of users: **system users** and **regular users**. Traditionally, system users are used to run non-interactive or background processes on a system, while regular users are used for logging in and running processes interactively. When you first initialize and log in to a Linux system, you may notice that it starts out with many system users already created to run the services that the OS depends on. This is normal.

You can view all of the users on a system by looking at the contents of the `/etc/passwd` file. Each line in this file contains information about a single user, starting with its username (the name before the first `:`). You can print the contents of the `passwd` file with `cat`:

```shell
$ cat /etc/passwd

sshd:x:109:65534::/run/sshd:/usr/sbin/nologin
landscape:x:110:115::/var/lib/landscape:/usr/sbin/nologin
pollinate:x:111:1::/var/cache/pollinate:/bin/false
systemd-coredump:x:999:999:systemd Core Dumper:/:/usr/sbin/nologin
lxd:x:998:100::/var/snap/lxd/common/lxd:/bin/false
vault:x:997:997::/home/vault:/bin/bash
stunnel4:x:112:119::/var/run/stunnel4:/usr/sbin/nologin
sammy:x:1001:1002::/home/sammy:/bin/sh
```

### Superuser

In addition to the two user types, there is the **superuser**, or root user, that has the ability to override any file ownership and permission restrictions. In practice, this means that the superuser has the rights to access anything on its own server. This user is used to make system-wide changes.

It is also possible to configure other user accounts with the ability to assume "superuser rights". This is often referred to as having `sudo`, because users who have permissions to temporarily gain superuser rights do so by preceding admin-level commands with `sudo`.

### Groups

Groups are collections of zero or more users. A user belongs to a default group, and can also be a member of any of the other groups on a server.

You can view all the groups on the system and their members by looking in the `/etc/group` file, as you would with `/etc/passwd` for users.

### Ownership and Permissions

In Linux, every file is owned by a single user and a single group, and has its own access permissions. Let's look at how to view the ownership and permissions of a file.

The most common way to view the permissions of a file is to use `ls` with the long listing option `-l`, e.g. `ls -l myfile`.

```shell
$ ls -l
```

<p align="center">
    <img src="images/ls-rights.png" width="50%"> 
</p>

Here is a breakdown of the mode metadata of the first file in the above example:

<p align="center">
    <img src="images/mode.png" width="30%"> 
</p>

**File Type**

In Linux, there are two types of files: **normal** and **special**. The file type is indicated by the first character of the mode of a file — in this guide, this will be referred to as the “file type field”.

Normal files can be identified by a hyphen (`-`) in their file type fields. Normal files can contain data or anything else. They are called normal, or regular, files to distinguish them from special files.

Special files can be identified by a non-hyphen character, such as a letter, in their file type fields, and are handled by the OS differently than normal files. The character that appears in the file type field indicates the kind of special file a particular file is. For example, a directory, which is the most common kind of special file, is identified by the `d` character that appears in its file type field.

**Permissions Classes**

From the diagram, you can see that the mode column indicates the file type, followed by three triads, or classes, of permissions: user (owner), group, and other. The order of the classes is consistent across all Linux systems.

The three permissions classes work as follows:

- **User**: The owner of a file belongs to this class.
- **Group**: The members of the file's group belong to this class. Group permissions are a useful way of assigning - permissions on a given file to multiple users.
- **Other**: Any users that are not part of the user or group classes for this file belong to this class.

In each triad, read, write, and execute permissions are represented in the following way:

- **Read**: Indicated by an `r` in the first position
- **Write**: Indicated by a `w` in the second position
- **Execute**: Indicated by an `x` in the third position.

A hyphen (`-`) in the place of one of these characters indicates that the respective permission is not available for the respective class. For example, if the group (second) triad for a file is r--, the file is “read-only” to the group that is associated with the file.

## Directory Structure
| Directory | Description                                                                                                                                                               |
| --------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| /         | The root directory. Everything, all the files and directories, in Linux are located under 'root' represented by '/'. Similar to a plant's root.                           |
| /bin      | Binaries. Contains executable files of basic shell commands like `ls`, `cp`, `cd`, etc.                                                                                   |
| /dev      | Device files. Contains special virtual files related to devices, not physically on the disk. Examples: `/dev/null`, `/dev/zero`, `/dev/random`.                           |
| /etc      | Configuration files. Contains core system configuration files, used primarily by administrator and services.                                                              |
| /usr      | User binaries and program data. Contains executable files, libraries, sources of most system programs. Subdirectories: `/usr/bin`, `/usr/sbin`, `/usr/lib`, `/usr/share`. |
| /home     | User personal data. Contains personal directories for users with their data and configuration files.                                                                      |
| /lib      | Shared libraries. Holds libraries needed by binaries in `/bin` and `/sbin`. Libraries for `/usr/bin` and `/usr/sbin` are in `/usr/lib`.                                   |
| /sbin     | System binaries. Similar to `/bin` but contains binaries that can only be run by root or sudo users.                                                                      |
| /tmp      | Temporary files. Holds temporary files; contents are deleted on system restart. Some systems delete old files automatically.                                              |
| /var      | Variable data files. Stores runtime information like logs, caches, and files created/managed by system programs.                                                          |
| /boot     | Boot files. Contains kernel files and boot images (LILO, GRUB). Usually on a partition at the beginning of the disk.                                                      |
| /proc     | Process and kernel files. Contains information about currently running processes and kernel parameters.                                                                   |
| /opt      | Optional software. Used for third-party applications not in the distribution's repository. Code is stored here, binaries often linked to `/bin`.                          |
| /root     | Home directory of the root user. Not to be confused with the root directory `/`.                                                                                          |
| /media    | Mount point for removable media. Directories are created automatically for USB, SD cards, DVDs, etc.                                                                      |
| /mnt      | Mount directory. Used by system administrators to manually mount filesystems.                                                                                             |
| /srv      | Service data. Contains data for system services (e.g., web server files).                                                                                                 |

## Linux Processes

In the Linux operating system, a process is defined as a program in execution. It represents an instance of a running program, encompassing both the program code and its current activity. Each process in Linux is assigned a unique Process ID (PID), which allows the operating system to manage and track it effectively.

### Types of Linux Processes

Linux processes can be broadly categorized into two main types:

- **Foreground Processes**: These are interactive processes that require user input and are executed in the foreground. They are directly associated with a terminal and can be managed using job control commands. Foreground processes typically occupy the terminal until they complete or are manually suspended.

- **Background Processes**: These processes run independently of user interaction and are often used for system services and long-running tasks. Background processes can be initiated by appending the `&` symbol at the end of a command or by using the `nohup` command to ensure they continue running even after the user logs out.

### Process States

Throughout its lifecycle, a Linux process can transition through several states:

- **Running**: The process is currently being executed by the CPU.
- **Sleeping**: The process is waiting for an event to occur, such as I/O completion.
- **Stopped**: The process has been halted, usually by receiving a signal.
- **Zombie**: The process has completed execution, but its parent has not yet read its exit status.

### Essential Commands

**The `ps` Command: Process Status**

The `ps` command, short for “process status,” is used to display information about currently running processes on a Linux system. It provides a snapshot of the processes at the time the command is executed.

- `ps -A` or `ps -e`: Lists all processes on the system.
- `ps -u username`: Displays processes for a specific user.
- `ps -f`: Shows a full-format listing, including parent-child relationships.
- `ps aux`: Provides a detailed list of all processes with information such as CPU and memory usage.

**The `top` Command: Real-time Process Monitoring**

When you run `top`, you'll see a dynamic list of processes that updates regularly. The output includes:

- Process ID (PID)
- User
- Priority
- CPU and memory usage
- Command name

You can interact with the `top` interface using various keyboard commands:

- Press `k` to kill a process (you’ll need to enter the PID)
- Press `r` to renice a process (change its priority)
- Press `q` to quit the `top` command

**The `jobs` Command: Managing Background Jobs**

This command will display a list of all jobs with their statuses (running, stopped, etc.). You can use additional options for more specific information:

- `jobs -l`: Lists process IDs in addition to the normal information.
- `jobs -r`: Restricts output to running jobs.
- `jobs -s`: Restricts output to stopped jobs.

The `jobs` command is essential for keeping track of background processes and managing multiple tasks simultaneously.


**The `bg` Command: Resuming Background Jobs**

The `bg` command is used to resume a suspended job in the background. This is particularly useful when a process has been stopped (e.g., using `Ctrl+Z`) and you want it to continue running without occupying the terminal.

```shell
bg %job_id
```

After suspending a job with `Ctrl+Z`, you can use `bg` followed by the job ID (which you can find using the `jobs` command) to resume it in the background. This allows for multitasking by letting users continue working on other tasks while the background job runs.

--- 

## References
 - https://tryhackme.com/room/linuxfundamentalspart1
 - https://tryhackme.com/room/linuxfundamentalspart2
 - https://tryhackme.com/room/linuxfundamentalspart3
 - https://linuxhandbook.com/linux-file-permissions/
 - https://linuxhandbook.com/linux-directory-structure/
 - https://www.digitalocean.com/community/tutorials/process-management-in-linux