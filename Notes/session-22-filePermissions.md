# Session 22: Standard File Permissions

## Default File Permissions

### What is umask?
Umask (user file-creation mode mask) is a default setting in Linux that determines the permissions assigned to newly created files and directories. It acts as a filter that restricts the default permissions.

### How to See the Value?
To check the current umask value, run:
```sh
$ umask

0022
```

### How to Change the umask Value
You can change the umask value temporarily for the current session using:
```sh
$ umask <value>
```
For example:
```sh
$ umask 0027
```
This sets new files to have permissions of 640 (rw-r-----).

## File Permissions

To view file permissions and types, you can use:
```sh
$ ls -li        # l is for long listing and i for inode numbers

1234567 -rw-r--r--  1 user group 12345 Sep 19 12:00 filename.txt
```
There are totoal of 10 columns which are explained as follows:

### 1. Inode Numbers

**What is it?**
An inode (index node) is a data structure on a filesystem that stores information about a file or a directory. Each file and directory is associated with a unique inode number, which serves as its identifier in the filesystem.

**Why is it used?**
- **File Metadata:** The inode contains metadata about the file, such as its size, ownership (user and group), permissions, timestamps (creation, modification, and access), and pointers to the data blocks where the actual file content is stored.
- **Efficient Management:** Inodes allow the filesystem to manage files efficiently. When you access a file, the operating system retrieves its inode to obtain the necessary metadata without needing to traverse the filesystem hierarchy.
- **Uniqueness:** Each inode number is unique within a filesystem, enabling the operating system to quickly locate the corresponding file or directory.


### 2. Permissions (10 bits)

#### 1st bit:
Certainly! Let's break down the first bit of the file permissions from the given output:

1. **Normal/Regular File (`-`)**:
   - **Description:** This symbol indicates that the file is a regular file, which can contain data, such as text documents, images, scripts, or executables. Regular files are the most common type of files you will encounter.
   - **Example:** A text document (`filename.txt`) or a script file (`script.sh`) falls into this category.

2. **Directory (`d`)**:
   - **Description:** If the first character were a `d`, it would indicate that the entry is a directory. Directories can contain files and other directories, organizing the filesystem into a hierarchy.
   - **Example:** A folder named `documents` that contains various files and subdirectories.

3. **Special Files**:
   - Special files serve specific purposes in the Linux operating system. Here are the types:
   1. **Block File (`b`)**:
      - **Description:** Represents block devices that manage data in blocks. These files are typically associated with storage devices.
      - **Example:** A hard disk drive (HDD) or USB storage device.
   
   2. **Character File (`c`)**:
      - **Description:** Represents character devices that transmit data one character at a time. These files are often associated with hardware devices.
      - **Example:** A keyboard or a serial port.
   
   3. **Socket File (`s`)**:
      - **Description:** Used for inter-process communication (IPC). Sockets allow processes to communicate with each other over the network or locally.
      - **Example:** A network socket used by a web server.
   
   4. **Named Pipe (`p`)**:
      - **Description:** A method for IPC that allows processes to communicate with each other by reading and writing to a named pipe.
      - **Example:** A pipe created for communication between different processes.
   
   5. **Symbolic Link (`l`)**:
      - **Description:** A pointer that links to another file or directory. Symbolic links are similar to shortcuts in Windows.
      - **Example:** A shortcut to another file, like `shortcut_to_file.txt`.

#### 9 bits (actual file permissions)
The actual 9 bits of permissions are divided into three groups of three characters each, representing the permissions for the **owner**, the **group**, and **others**. Here’s a breakdown:

### 1. Owner Permissions (First 3 Characters)
- **`r` (Read):** The owner can read the file. This means they can view the contents of the file.
- **`w` (Write):** The owner can modify or delete the file. This allows them to change the file's content or remove the file entirely.
- **`x` (Execute):** The owner can execute the file if it is a script or a program. If this permission is not set, the owner cannot run the file as a program.

**Example:** In `-rw-`, the owner has read and write permissions but cannot execute the file.

### 2. Group Permissions (Next 3 Characters)
- **`r` (Read):** Users who are part of the file's group can read the file.
- **`w` (Write):** Users in the group can modify or delete the file.
- **`x` (Execute):** Users in the group can execute the file if it is a script or executable.

**Example:** In `r--`, group members can only read the file.

### 3. Other Permissions (Last 3 Characters)
- **`r` (Read):** All other users (not the owner or in the group) can read the file.
- **`w` (Write):** All other users can modify or delete the file.
- **`x` (Execute):** All other users can execute the file if it is a script or executable.

**Example:** In `r--`, other users can only read the file.

### Summary
To summarize, the nine bits of permissions dictate who can do what with a file:
- The **first three bits** indicate permissions for the **owner**.
- The **second three bits** indicate permissions for the **group**.
- The **last three bits** indicate permissions for **others**.

Each permission can be represented as follows:
- **Read (`r`)** = 4
- **Write (`w`)** = 2
- **Execute (`x`)** = 1

This means that permissions can be represented in octal (base 8) as a combination of these values. For example, `rw-r--r--` translates to:
- Owner: `rw-` = 4 (read) + 2 (write) = **6**
- Group: `r--` = 4 (read) = **4**
- Others: `r--` = 4 (read) = **4**

So, the octal representation would be `644`. Understanding these permissions helps in managing file security and access control effectively.

Here’s a table that summarizes all the possible 3-bit combinations for file permissions in Linux:

| Binary | Octal | Permissions   | Description                           |
|:------:|:-----:|:-------------:|:-------------------------------------:|
| 000    | 0     | ---           | No permissions                        |
| 001    | 1     | --x           | Execute only                          |
| 010    | 2     | -w-           | Write only                            |
| 011    | 3     | -wx           | Write and execute                     |
| 100    | 4     | r--           | Read only                             |
| 101    | 5     | r-x           | Read and execute                      |
| 110    | 6     | rw-           | Read and write                        |
| 111    | 7     | rwx           | Read, write, and execute              |


### 3. Number of Links to File
- **Explanation:** This column indicates the number of hard links pointing to the file. A hard link is essentially an additional directory entry for a file. 
- **Importance:** If the number is greater than one, it means there are multiple directory entries (links) for the same inode. When the link count drops to zero (i.e., when all links to the file are deleted), the file data is removed from the filesystem.

### 4. Owner
- **Explanation:** This column displays the username of the individual who owns the file. Each file in Linux is associated with a specific user.
- **Importance:** The owner has specific permissions and rights to access and modify the file, which can differ from those of other users and groups.

### 5. Group
- **Explanation:** This column shows the name of the group associated with the file. A group can contain multiple users, and they share the same permissions on the file.
- **Importance:** Permissions set for the group allow all users within that group to access the file in the specified way, which helps in managing access control for collaborative work.

### 6. File Size in Bytes
- **Explanation:** This column indicates the size of the file in bytes. It tells you how much space the file occupies on the disk.
- **Importance:** Knowing the file size is useful for storage management and understanding the nature of the file (e.g., whether it is a large data file or a small script).

### 7. Date and Time Stamp
- **Explanation:** This column displays the last modification date and time of the file. It indicates when the file was last changed.
- **Importance:** The timestamp is crucial for version control, backup management, and understanding the recency of changes to a file.

### 8. Name of the File
- **Explanation:** This is the final column that shows the actual name of the file or directory.
- **Importance:** The file name is essential for identifying the content and purpose of the file. It is how users refer to the file in commands and scripts.

## How to Change the Permissions?

### Introducing the `chmod` Command
The `chmod` (change mode) command in Linux is used to change the file permissions for users, groups, and others. You can modify permissions using two methods: the **absolute method** and the **relative method**.

### 1. Absolute Method
The absolute method uses octal numbers to represent the permissions. Each permission (read, write, execute) has a specific value:
- **Read (`r`)** = 4
- **Write (`w`)** = 2
- **Execute (`x`)** = 1

These values are summed up to set permissions for the owner, group, and others.

**How it Works:**
- Each group of permissions (owner, group, others) is represented by a single digit (0-7). 
- For example, `chmod 754 filename.txt` sets:
  - Owner: `7` (read + write + execute)
  - Group: `5` (read + execute)
  - Others: `4` (read only)

**Examples:**
- To set permissions to `rw-r--r--` (read and write for the owner, read for the group and others):
  ```bash
  chmod 644 filename.txt
  ```
- To allow the owner full permissions and group/others to read and execute:
  ```bash
  chmod 755 filename.txt
  ```

### 2. Relative Method
The relative method modifies permissions based on the current settings using symbols:
- **`u`**: user (owner)
- **`g`**: group
- **`o`**: others
- **`a`**: all (user, group, and others)

You can add (`+`), remove (`-`), or set (`=`) permissions.

**How it Works:**
- You specify the change you want to make, followed by the file name.

**Examples:**
- To add execute permission for the owner:
  ```bash
  chmod u+x filename.txt
  ```
- To remove write permission for the group:
  ```bash
  chmod g-w filename.txt
  ```
- To set permissions to read and write for everyone:
  ```bash
  chmod a=rw filename.txt
  ```

## How to Change the Group?

### Introducing the `chgrp` Command
The `chgrp` command is used to change the group ownership of a file or directory.

**Example:**
To change the group of `filename.txt` to `newgroup`:
```bash
chgrp newgroup filename.txt
```
This command makes `newgroup` the group owner of the file, allowing members of that group to access it based on the group's permissions.

## How to Change the Ownership?

### Introducing the `chown` Command
The `chown` command changes the ownership of a file or directory. You can specify a new owner and optionally a new group.

**Examples:**
1. To change the owner of `filename.txt` to `newowner`:
   ```bash
   chown newowner filename.txt
   ```

2. To change both the owner and the group:
   ```bash
   chown newowner:newgroup filename.txt
   ```
