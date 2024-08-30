# Session 19: User Management


**`su`:** Switch user

```bash
$ sudo su root  # Switch to the root user (requires sudo privileges)
```

**`whoami` vs. `who`:**

* `whoami`: Displays your current username.
  ```bash
  $ whoami  # Output: "your_username"
  ```
* `who`: Lists all logged-in users.
  ```bash
  $ who  # Output: "user terminal date time"
  ```

**`w`:** Displays information about logged-in users.

```bash
$ w  # Output: "user terminal uptime CPU load average users processes"
```

**`id`:** Displays user ID, group IDs, and other information.

```bash
$ id  # Output: "uid=your_uid(your_username) gid=your_primary_gid(your_group) groups=your_groups"
```

**`sudo`:** Allows you to execute commands as another user (typically root).

```bash
$ sudo apt update  # Update package lists with root privileges
```

**`visudo`:** Configures the `sudoers` file, which controls which users can execute commands as other users.

```bash
$ sudo visudo  # Edit the sudoers file (requires root privileges)
```

## `passwd` Command 
This command prompts you to change your own password.

### Options

1. **-a, --all:** Report password status on all accounts.
   ```bash
   $ sudo passwd -a
   ```
   This will display the password status for all user accounts on the system.

2. **-d, --delete:** Delete the password for the named account.
   ```bash
   $ sudo passwd -d olduser
   ```
   This will delete the password for the user "olduser", effectively disabling the account.

3. **-e, --expire:** Force expire the password for the named account.
   ```bash
   $ sudo passwd -e olduser
   ```
   This will immediately expire the password for the user "olduser", requiring them to change it upon next login.

4. **-n, --mindays MIN_DAYS:** Set the minimum password age.
   ```bash
   $ sudo passwd -n 10 user
   ```
   This sets the minimum password age for the user "user" to 10 days.

5. **-S, --status:** Report password status on the named account.
   ```bash
   $ sudo passwd -S olduser
   ```
   This will display the password status for the user "olduser", including information like expiration date, password age, and whether the account is locked.

> [!NOTE] 
> To use these options, you typically need to have `sudo` privileges.


shadow and group files
#### detailes of a line info in passwd and shadow and group: explain each word meaning in each file


## Adding user
1.  **`adduser`:**
    It will handle the all the things. It creates the user and it's group, selects the uid and gid, creates the home directory and ask for the password. 

    ```bash
    $ sudo adduser atharv

    info: Adding user `atharv' ...
    info: Selecting UID/GID from range 1000 to 59999 ...
    info: Adding new group `atharv' (1002) ...
    info: Adding new user `atharv' (1002) with group `atharv (1002)' ...
    info: Creating home directory `/home/atharv' ...
    info: Copying files from `/etc/skel' ...
    New password:
    Retype new password:
    passwd: password updated successfully
    Changing the user information for atharv
    Enter the new value, or press ENTER for the default
        Full Name []: Atharv Hiremath
        Room Number []:
        Work Phone []:
        Home Phone []:
        Other []:
    Is the information correct? [Y/n] y
    info: Adding new user `atharv' to supplemental / extra groups `users' ...
    info: Adding user `atharv' to group `users' ...
    ```

2.  **`useradd`:**
    All the things are done manually. flexibility to customize the new user while creating

    ### **Options:**
    1.  -c, --comment COMMENT         GECOS field of the new account
    2.  -d, --home-dir HOME_DIR       home directory of the new account
    3.  -g, --gid GROUP               name or ID of the primary group of the new account 
    4.  -k, --skel SKEL_DIR           use this alternative skeleton directory
    5.  -m, --create-home             create the user's home directory
    6.  -s, --shell SHELL             login shell of the new account
    7.  -M, --no-create-home          do not create the user's home directory
    8.  -N, --no-user-group           do not create a group with the same name as the user
    9.  -Z, --selinux-user SEUSER     use a specific SEUSER for the SELinux user mapping

    ```bash 
    $ sudo useradd atharv -c "part of QA team" -m -d /home/atharv -s /bin/sh

## Removing user
### userdel vs deluser
Explain some very important options like -r which are frequently used. with example

## Modifying user
### usermod
### options:
1.  -c, --comment COMMENT         new value of the GECOS field
2.  -d, --home HOME_DIR           new home directory for the user account
3.  -e, --expiredate EXPIRE_DATE  set account expiration date to EXPIRE_DATE
4.  -L, --lock                    lock the user account
5.  -m, --move-home               move contents of the home directory to the new location (use only with -d)
