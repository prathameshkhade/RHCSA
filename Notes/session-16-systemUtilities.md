## Session 15: System Utilities

### `find`

**Purpose:** Locates files in a directory hierarchy based on specified criteria.

**Syntax:**
```bash
find path -options arguments
```

**Common Options:**

* **-type:** Specifies the file type (e.g., `f` for regular files, `d` for directories).
* **-name:** Matches files based on their name.
* **-newer:** Matches files modified after a given file.

**Example:**
```bash
find . -type f -name "*.txt" -newer file.txt
```
This finds all regular files named "*.txt" in the current directory or subdirectories that were modified after `file.txt`.

### `locate`

**Purpose:** Quickly finds files based on their name.

**Syntax:**
```bash
locate pattern
```

**Note:** `locate` uses a database of file names that is periodically updated using the `updatedb` command.

**Example:**
```bash
updatedb
locate myfile.txt
```

### `time`

**Purpose:** Measures the execution time of a command.

**Syntax:**
```bash
time command
```

**Example:**
```bash
time ls -l
```

### `date`

**Purpose:** Displays the current date and time.

**Syntax:**
```bash
date
```

### `timedatectl`

**Purpose:** Provides more detailed information about the system's date and time settings.

**Syntax:**
```bash
timedatectl
```

### `sleep`

**Purpose:** Pauses the execution of a script for a specified number of seconds.

**Syntax:**
```bash
sleep seconds
```

## Compression and Decompression

### 1. `tar`

**Purpose:** Creates and extracts tar archives.

**Syntax:**
```bash
tar -cvzf archive.tar.gz files
```

**Options:**
* **`-c, --create:`** Create a new archive.
* **`-x:`** To extract an archive.
* **`-v:`** Verbose output.
* **`-z:`** Use gzip compression.
* **`-f:`** Specify the archive file.
* **`-r, --apend:`** Append files to the end of an archive.
* **`-t, --list:`** list the contents of an archive

**Example:**
```bash
tar -cvzf backup.tar.gz important_files
```

### 2. `zip`

**Purpose:** Creates ZIP archives.

**Syntax:**
```bash
zip archive.zip files
```

**Example:**
```bash
zip backup.zip important_files
```

### 3. `gzip`

**Purpose:** Compresses and decompresses files using gzip.

**Syntax:**
```bash
gzip -c file.txt > file.txt.gz
gzip -d file.txt.gz
```

**Example:**
```bash
gzip -c myfile.txt > myfile.txt.gz
gzip -d myfile.txt.gz
```

### 4. `bzip2`

**Purpose:** Compresses and decompresses files using bzip2.

**Syntax:**
```bash
bzip2 -c file.txt > file.txt.bz2
bzip2 -d file.txt.bz2
```

**Example:**
```bash
bzip2 -c myfile.txt > myfile.txt.bz2
bzip2 -d myfile.txt.bz2
```

> [!NOTE]
> * **`zcat`** and **`bzcat`** are equivalent to `gzip -dc` and `bzip2 -dc`, respectively.
> * **`zmore`** and **`bzmore`** are similar to `more` but for compressed files.
> * **`zless`** and **`bzless`** are similar to `less` but for compressed files.
