# Session 24: Access Control List (ACL)

## What is ACL?

Access Control Lists (ACLs) provide a way to define more granular permissions on files and directories than the traditional owner/group/other model. With ACLs, you can specify permissions for individual users or groups, allowing for greater flexibility in managing access.

## Install ACL

### **On Debian:**
```sh
$ sudo apt install acl -y
```

### **On RHEL:**
To install ACL (Access Control Lists) on RHEL (Red Hat Enterprise Linux), follow these steps:

1. **Check if ACL is installed:**
   First, check if ACL is already installed by running:
    ```bash
    $ getfacl --version
    ```
    If it's installed, you’ll see the version information. If not, you'll get an error.

2. **Install the ACL package:**
    If ACL is not installed, you can install it using `yum` or `dnf`, depending on your RHEL version. Run the following command:
    ```bash
    $ sudo yum install acl
    ```
    or
    ```bash
    $ sudo dnf install acl
    ```

3. **Verify the installation:**
    After installation, confirm that ACL is available by running:
    ```bash
    $ getfacl --version
    ```

4. **Enable ACL on filesystems:**
    You may need to enable ACL support on specific filesystems. Check the current mount options with:
    ```bash
    $ mount | grep acl
    ```

    If ACL is not enabled, you can modify the `/etc/fstab` file. Find the line for the filesystem you want to enable ACL on and add `acl` to the options. For example:
    ```
    /dev/mapper/rhel-root /                       xfs     defaults,acl  0 0
    ```

    After editing `/etc/fstab`, remount the filesystem to apply the changes:
    ```bash
    $ sudo mount -o remount /
    ```

5. **Set ACLs:**
    You can now set ACLs using `setfacl`. For example, to give a user read permission on a file:
    ```bash
    $ setfacl -m u:username:r file.txt
    ```

6. **Get ACLs:**
    To view the ACLs of a file or directory, use:
    ```bash
    $ getfacl file.txt
    ```

## Checking the ACL of a File or Directory

To view the ACL of a file or directory, use the `getfacl` command. This command displays all the permission details associated with the file.

### Example:
```bash
$ getfacl ubuntu-server
# file: ubuntu-server
# owner: prathamesh
# group: prathamesh
user::rw-
group::rw-
other::r--
```
In this example, the file `ubuntu-server` has the following permissions:
- Owner (`prathamesh`): read and write
- Group (`prathamesh`): read and write
- Others: read

## Set the ACL

To add specific permissions for a user, use the `-m` (modify) option with `setfacl`.

### Command Syntax:
```bash
$ setfacl -m u:<username>:<permissions> filename
```
You can also specify permissions using octal numbers.

### Example:
To set read and write permissions for user `atharv` on the file `ubuntu-server`:
```bash
$ setfacl -m u:atharv:rw ubuntu-server      # rw = 4(read) + 2(write) = 6
```

### Specifying ACL from a File
You can use the `-M` option to specify the ACL list in a file:
```bash
$ setfacl -M aclfile.txt ubuntu-server
```
Where `aclfile.txt` contains the ACL specifications.

## Remove ACL

To remove specific permissions from a user, use the `-x` (remove) option.

### Example:
To remove the write permission of user `atharv` from the `ubuntu-server` file:
```bash
$ setfacl -x u:atharv:w ubuntu-server
```

To completely remove all permissions for a user, use the `-b` option:
```bash
$ setfacl -b ubuntu-server
```
This will remove all ACL entries for the file, including those for `atharv`.

### Example of Removing Group Permissions
To remove specific permissions for a group, use a similar command with `g` for groups.

**Example:** Remove read permission for group `devs` from `ubuntu-server`:
```bash
$ setfacl -x g:devs:r ubuntu-server
```

## Managing Group ACLs

### Setting Group Permissions
To set specific permissions for a group:
```bash
$ setfacl -m g:<groupname>:<permissions> filename
```

**Example:** To give read and execute permissions to group `devs` for `ubuntu-server`:
```bash
$ setfacl -m g:devs:rx ubuntu-server
```

### Removing Group Permissions
To remove write permission for group `devs`:
```bash
$ setfacl -x g:devs:w ubuntu-server
```

## Using the `--no-mask` Option

The `--no-mask` option allows you to set permissions for a user or group without being restricted by the current mask, which may limit permissions based on the highest granted permission among users.

### Example:
Set read and write permissions for user `atharv` and full permissions for group `devs` without being restricted by the mask:
```bash
$ setfacl -m u:atharv:rw --no-mask ubuntu-server
$ setfacl -m g:devs:rwx --no-mask ubuntu-server
```

Using `--no-mask` ensures that the specified permissions are applied regardless of any existing mask limitations.