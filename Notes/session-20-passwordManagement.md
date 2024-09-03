# Managing password of user

## `passwd` Command 
This command prompts you to change your own password.

### Options

1. **-a, --all:** Report password status on all accounts.
   ```bash
   $ sudo passwd -a # Don't know why, but this option is not working.
   ```
   This will display the password status for all user accounts on the system.

2. **-d, --delete:** Delete the password for the named account.
   ```bash
   $ sudo passwd -d atharv

   [sudo] password for prathamesh:
   Removing password for user atharv.
   passwd: Success
   ```
   This will delete the password for the user "atharv", effectively disabling the account.

3. **-e, --expire:** Force expire the password for the named account.
   ```bash
   $ sudo passwd -e atharv

   Expiring password for user atharv.
   passwd: Success
   ```
   This will immediately expire the password for the user "atharv", requiring them to change it upon next login.

4. **-n, --mindays MIN_DAYS:** Set the minimum password age.
   ```bash
   $ sudo passwd -n 14 atharv

   Adjusting aging data for user atharv.
   passwd: Success
   ```
   This sets the minimum password age for the user "atharv" to 14 days.

5. **-x, --maximum DAYS:** Set the maximum password age.
   ```bash
   $ sudo passwd -x 30 atharv

   Adjusting aging data for user atharv.
   passwd: Success
   ```
   This sets the maximum password age for the user "atharv" to 30 days.

6. **-i, --inactive DAYS:** Specifies the number of inactive days for a user.
   ```bash
   $ sudo passwd -i 5 atharv

   Adjusting aging data for user atharv.
   passwd: Success
   ```
   This will set the inactivity period to 5 days for the user "atharv" after which the account will be disabled if the password is not changed.

7. **-w, --warning DAYS:** Set the number of days in advance the user will begin receiving warnings that her password will expire.
   ```bash
   $ sudo passwd -w 3 atharv

   Adjusting aging data for user atharv.
   passwd: Success
   ```
   This will gives the warning message for changing the password before 3 days of minimum days

8. **-S, --status:** Report password status on the named account.
   ```bash
   $ sudo passwd -S atharv

   atharv NP 2024-08-31 14 30 3 5 (Empty password.)
   ```

   -  `atharv`: The username for which the status is being checked.
   -  `NP`: It stand for "No Password", indicating that the user does not have a password set.
   -  `2024-08-31`: The date when the password was last changed.
   -  `14`: Then minimum age (days) before the password can be changed again.
   -  `30`: Then maximum age (days) before the password can be changed again.
   -  `3`: Then warning period (days) before the password has to be changed.
   -  `5`: The inactivity period (days) after which the account will be disabled if the password is not changed the password can be changed again.

   The summary of this is, the user `atharv` dows not have a password set (Empty password). The passwrod status was last changed  on `2024-08-31`. The password cannot be changed for 14 days, must be changed after 30 days, has a warning period of 3 days, and the account will be disabled after 5 days of inactivity if the password is not changed.


> [!NOTE] 
> To use these options, you typically need to have `sudo` privileges.

# Understanding Password Management in Linux

## Creating Users with `openssl`

**`openssl`** is a powerful cryptographic tool that can be used to generate encrypted passwords.

**Command Breakdown:**

```bash
$ sudo useradd -p $(openssl passwd password1) atharv
```

* **`sudo useradd`:** Creates a new user named "atharv".
* **`-p`:** Specifies the password for the new user.
* **`$(openssl passwd password1)`:** Generates an encrypted password using `openssl` with the plain-text password "password1".

## Default Password Settings

The default password settings for new users are typically defined in the `/etc/login.defs` file. This file contains configuration options that affect password aging, expiration, and other policies.

## Modifying Password Configuration with `chage`

**`chage`** is a command-line tool used to modify password aging information for specific users.

This command allows you to change the following password configuration settings for the user "atharv":
```bash
$ sudo chage atharv

Changing the aging information for atharv
Enter the new value, or press ENTER for the default

	Minimum Password Age [0]: 30
	Maximum Password Age [99999]: 45
	Last Password Change (YYYY-MM-DD) [2024-09-03]:
	Password Expiration Warning [7]: 7
	Password Inactive [-1]: 7
	Account Expiration Date (YYYY-MM-DD) [-1]: 2024-12-31
```

This command allows you to check the password configuration setting for the user "atharv":
```bash
$ sudo chage -l atharv

Last password change					            : Sep 02, 2024
Password expires					                : Oct 17, 2024
Password inactive					                : Oct 24, 2024
Account expires						                : Dec 30, 2024
Minimum number of days between password change		: 30
Maximum number of days between password change		: 45
Number of days of warning before password expires	: 7

```