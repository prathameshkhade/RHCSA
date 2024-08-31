# Session 19: User Management

## Basics commands

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
   $ sudo passwd -S atharv

   atharv P 2024-08-30 0 99999 7 -1
   ```

   * **atharv:** The username.
   * **P:** The password status. "P" indicates that the password is valid.
   * **2024-08-30:** The last time the password was changed.
   * **0:** The minimum number of days before the password can be changed.
   * **99999:** The maximum number of days before the password must be changed (essentially no limit).
   * **7:** The number of days before password expiration that a warning is issued.
   * **-1:** The account expiration date (negative value indicates no expiration).

In summary, this output shows that the user "atharv" has a valid password that was last changed on August 30, 2024. There are no restrictions on password changes, and the account does not have an expiration date.


> [!NOTE] 
> To use these options, you typically need to have `sudo` privileges.


## Understanding the `passwd`, `shadow`, and `group` Files

### 1.  `passwd` File

The `/etc/passwd` file contains information about user accounts. Each line represents a user. A typical line looks like this:

```
username:x:UID:GID:GECOS:home_directory:shell
```

* **Username:** The login name of the user.
* **x:** Placeholder for the encrypted password (now stored in the `shadow` file).
* **UID:** Unique user ID number.
* **GID:** Primary group ID number.
* **GECOS:** Comma-separated fields containing information about the user (e.g., full name, room number).
* **home_directory:** Path to the user's home directory.
* **shell:** Default login shell for the user.

### 2.  `shadow` File

The `/etc/shadow` file contains encrypted password information for user accounts. Each line corresponds to a user in the `passwd` file.

```
username:encrypted_password:last_changed:min_days:max_days:warn_days:inactive_days:expire_days:reserved
```

* **Username:** The login name of the user.
* **Encrypted password:** The encrypted password hash.
* **Last changed:** Date of the last password change.
* **Minimum password age:** Number of days before the password can be changed.
* **Maximum password age:** Number of days before the password must be changed.
* **Warning days:** Number of days before password expiration that a warning is issued.
* **Inactive days:** Number of days of inactivity before the account is disabled.
* **Expiration days:** Date when the account expires.
* **Reserved:** For future use.

### 3.  `group` File

The `/etc/group` file contains information about groups. Each line represents a group.

```
group_name:x:GID:member_list
```

* **group_name:** The name of the group.
* **x:** Placeholder for the encrypted password (not used in modern systems).
* **GID:** Group ID number.
* **member_list:** Comma-separated list of users belonging to the group.

### **Example:**

Let's assume a line from each file:

**`/etc/passwd`:**
```
john:x:1000:1000:John Doe:/home/john:/bin/bash
```

**`/etc/shadow`:**
```
john:$6$salt$hash:1685392000:0:90:7:0:0:
```

**`/etc/group`:**
```
users:x:1001:john,mary,bob
```

In this example:
* **John Doe** is a user with UID 1000 and primary group 1000.
* The user's password was last changed on October 1, 2023 (assuming Unix timestamp 1685392000).
* The password must be changed within 90 days.
* The user belongs to the "users" group, along with "mary" and "bob".



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
