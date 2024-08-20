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

