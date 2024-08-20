# Session 14: Input Output Redirection

## How the Shell Works?

![Working of Shell](images/shell.png)

Imagine a shell as a translator between you and the computer. When you type a command, the shell:
1. **Reads** your command from the keyboard (standard input).
2. **Executes** the command, processing data.
3. **Displays** the results on the screen (standard output) or sends error messages (standard error).

These three channels are essential for communication between you and the system:

* **Standard Input (stdin):** Typically the keyboard, but can be redirected to a file.
* **Standard Output (stdout):** Usually the screen, but can be redirected to a file.
* **Standard Error (stderr):** Typically the screen, but can be redirected separately from stdout.

## Redirection Operators

Redirection operators are symbols that change the default behavior of stdin and stdout.

### Input Redirection (<)
* **Purpose:** Takes data from a file and feeds it into a command as input.
* **Syntax:** `command < file`
* **Example:** `cat < myfile.txt` reads the contents of `myfile.txt` and displays it on the screen.

### Output Redirection (>)
* **Purpose:** Sends the command's output to a file, overwriting the file if it exists.
* **Syntax:** `command > file`
* **Example:** `ls > filelist.txt` lists files and directories and saves the output to `filelist.txt`.

### Append Output (>>)
* **Purpose:** Sends the command's output to a file, appending to the end of the file if it exists.
* **Syntax:** `command >> file`
* **Example:** `date >> logfile.txt` appends the current date and time to `logfile.txt`.

> [!NOTE]
> These are basic examples. There are more complex ways to use redirection, including combining multiple operators and using temporary files.

## Understanding `1>&2` and `2>&1`

### File Descriptors
Before diving into these operators, let's quickly recap file descriptors:

* **0:** Standard input (stdin)
* **1:** Standard output (stdout)
* **2:** Standard error (stderr)

These numbers represent file-like objects that programs can use to read and write data.

### `1>&2`
This redirection operator means "redirect standard output (1) to standard error (2)". In simpler terms, anything that would normally be printed to the screen as standard output will now be sent to the error stream.

**Example:**
```bash
command 1>&2
```
Any output from the `command` will be sent to the error stream instead of the standard output.

### `2>&1`
This redirection operator means "redirect standard error (2) to standard output (1)". This is commonly used to combine both standard output and standard error into a single stream.

**Example:**
```bash
command 2>&1 > output.log
```
Both the standard output and standard error from the `command` will be redirected to the `output.log` file.

### Why Use Them?
* **Combining output:** When you want to capture both standard output and standard error in a single file.
* **Hiding errors:** Sometimes, you might want to suppress error messages. By redirecting stderr to stdout and then redirecting stdout to `/dev/null`, you can effectively hide errors.

**Example:**
```bash
command 2>&1 > /dev/null
```
This command runs the command, but both its standard output and standard error are discarded.

> [!NOTE] 
> While these operators are powerful, use them judiciously. Overusing them can make troubleshooting difficult. It's often better to handle standard output and standard error separately for better error handling and debugging.
 