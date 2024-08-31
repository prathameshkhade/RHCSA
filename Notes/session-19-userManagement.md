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
    $ sudo adduser atharv  # Adds a new user named "atharv" to the system.

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

      **Output Breakdown:**

      * **`info: Adding user 'atharv' ...`:** The system is starting the process of creating the new user.
      * **`info: Selecting UID/GID from range 1000 to 59999 ...`:** The system is choosing a unique user ID (UID) and group ID (GID) for the new user. These numbers are typically assigned sequentially to avoid conflicts.
      * **`info: Adding new group 'atharv' (1002) ...`:** A new group with the same name as the user is created. This group will be the primary group for the new user.
      * **`info: Adding new user 'atharv' (1002) with group 'atharv (1002)' ...`:** The new user is created with the specified UID, GID, and group membership.
      * **`info: Creating home directory '/home/atharv' ...`:** A home directory is created for the new user. This directory will be the user's personal workspace.
      * **`info: Copying files from '/etc/skel' ...`:** Essential files and configuration settings are copied from the `/etc/skel` directory to the new user's home directory, providing a basic environment for the user.
      * **`New password:` and `Retype new password:`:** You are prompted to enter a new password for the user.
      * **`passwd: password updated successfully`:** The password has been successfully set.
      * **`Changing the user information for atharv`:** You are given the opportunity to modify the user's information, such as their full name, room number, and contact details.
      * **`info: Adding new user 'atharv' to supplemental / extra groups 'users' ...`:** The user is added to additional groups, such as the "users" group, which may grant the user specific privileges.

2. **`useradd`** is a more granular command for creating new user accounts, allowing you to customize various aspects of the user.

   **Options:**

   1. **-c, --comment COMMENT:** Sets the GECOS field, which contains additional information about the user (e.g., full name, room number).
   2. **-d, --home-dir HOME_DIR:** Specifies the home directory for the new user. If not specified, the default is `/home/username`.
   3. **-g, --gid GROUP:** Sets the primary group for the new user. If not specified, a new group with the same name as the user is created.
   4. **-k, --skel SKEL_DIR:** Uses an alternative skeleton directory for the user's home directory. By default, the `/etc/skel` directory is used.
   5. **-m, --create-home:** Creates the user's home directory. If not specified, the home directory is not created.
   6. **-s, --shell SHELL:** Sets the login shell for the user. If not specified, the default login shell is used.
   7. **-M, --no-create-home:** Prevents the creation of the user's home directory.
   8. **-N, --no-user-group:** Prevents the creation of a group with the same name as the user.
   9. **-Z, --selinux-user SEUSER:** Specifies the SELinux user mapping for the new user (relevant for SELinux-enabled systems).

   **Example:**

   ```bash
   $ sudo useradd atharv -c "Atharv Hiremath, QA Team" -m -d /home/atharv -g QnA -s /bin/bash
   ```

   This command creates a new user named "atharv" with the following settings:

   * **GECOS:** "Atharv Hiremath, QA Team"
   * **Home directory:** `/home/atharv`
   * **Primary group:** "QnA"
   * **Login shell:** `/bin/bash`

   The `-m` option ensures that the home directory is created, and the `-g` option assigns the user to the "QnA" group.

   By using these options, you can tailor the creation of new user accounts to your specific needs and security requirements.


## `userdel` vs. `deluser`

Both `userdel` and `deluser` are used to remove user accounts. However, `userdel` provides more options for customization.

### Common Options

* **-f:** Force removal even if the user is still logged in or files are not owned by the user.
* **-r:** Remove the user's home directory and mail spool.
* **-R:** Chroot to a specified directory before performing the removal.
* **-P:** Specify a prefix directory for `/etc/*` files.
* **-Z:** Remove any SELinux user mapping for the user.

### Example: Removing the User "atharv"

```bash
$ sudo userdel -rf atharv

[sudo] password for prathamesh:
userdel: atharv mail spool (/var/mail/atharv) not found
```

This command will remove the user "atharv," including their home directory and mail spool. The `-r` option ensures that the user is completely removed, even if they are still logged in or if files are not owned by them.

> [!NOTE]
> Removing a user can have significant consequences. Ensure that you have a backup of any important data before proceeding.


## Modifying user
### usermod
### options:
1.  -c, --comment COMMENT         new value of the GECOS field
2.  -d, --home HOME_DIR           new home directory for the user account
3.  -e, --expiredate EXPIRE_DATE  set account expiration date to EXPIRE_DATE
4.  -L, --lock                    lock the user account
5.  -m, --move-home               move contents of the home directory to the new location (use only with -d)
