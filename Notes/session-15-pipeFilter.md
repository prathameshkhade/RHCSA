# Session 15: Pipes and Filtering

**Piping** in Linux is a powerful technique that allows you to connect the output of one command to the input of another. It's represented by the vertical bar (`|`) symbol.

**Example:**

```bash
ls -l | grep "txt"
```

In this example:
* `ls -l` lists all files in the current directory with detailed information.
* The pipe (`|`) symbol connects the output of `ls -l` to the input of `grep`.
* `grep "txt"` filters the output of `ls -l` to only show files with the ".txt" extension.

> [!NOTE]
> **In essence, piping allows you to chain commands together to create complex workflows and perform data processing efficiently.**

# Filtering Commands

## grep: A Powerful Command-Line Tool

**grep** is a versatile command-line tool used to search for patterns within text files. It's a fundamental utility for anyone working with text data.

### Common Options

Here's a breakdown of some frequently used options:

1. **`-i:`** Ignore case.

    ```bash
    grep -i "hello" myfile.txt  # Searches for "hello" or "Hello" regardless of case.
    ```

2. **`-v:`** Invert match.

    ```bash
    grep -v "error" logfile.txt  # Displays lines that *don't* contain "error".
    ```

3. **`-c:`** Count matches.

    ```bash
    grep -c "pattern" file.txt  # Counts the number of lines containing "pattern".
    ```

4. **`-e:`** Extended regular expressions.

    ```bash
    grep -e "pattern1\|pattern2" file.txt  # Searches for either "pattern1" or "pattern2".
    ```
    > [!NOTE] 
    > **You can also use the `egrep` command which is equivalent to `grep -e**

5. **`-h:`** Suppress file names.

    ```bash
    grep -h "pattern" file1.txt file2.txt  # Doesn't prepend file names to matches.
    ```

6. **`-H:`** Print file names with matches.

    ```bash
    grep -H "pattern" file1.txt file2.txt  # Prints the filename before each match.
    ```

7. **`-A <num>`:** Print lines after the match.

    ```bash
    grep -A 2 "pattern" file.txt  # Prints the matching line plus two lines after it.
    ```

8. **`-B <num>`:** Print lines before the match.

    ```bash
    grep -B 2 "pattern" file.txt  # Prints the matching line plus two lines before it.
    ```

9. **`-C <num>`:** Print lines before and after the match.

    ```bash
    grep -C 2 "pattern" file.txt  # Prints the matching line plus two lines before and after it.
    ```



> [!NOTE]  
> **These are just a few of the many options available for `grep`. Refer to the `grep` manual page (`man grep`) for a complete list and detailed explanations.**


## Types of `grep`

**1. `egrep`:** Extended grep

**Purpose:** Uses extended regular expressions, which offer more powerful pattern-matching capabilities than basic regular expressions.

**Example:** 
``` bash
egrep -i "hello|world" file.txt
# searches for "hello" or "world" (case-insensitive) using extended regular expressions.
``` 

**2. `fgrep`:** Fixed string grep

**Purpose:** Searches for fixed strings rather than regular expressions. This can be faster for simple pattern matching.

**Example:** 
```bash 
fgrep "hello" file.txt
# searches for the exact string "hello".
```

**3. `pdfgrep`:** Grep for PDF files

**Purpose:** A specialized version of `grep` designed to search for text within PDF files.

**Example:** 
```bash 
pdfgrep "keyword" myfile.pdf 
# searches for the keyword "keyword" within the PDF file "myfile.pdf".
```

**4. `zgrep`:** Grep for compressed files

**Purpose:** Searches for patterns within compressed files (e.g., gzip, bzip2).

**Example:** 
```bash 
zgrep "pattern" compressed_file.gz 
# searches for "pattern" within the compressed file "compressed_file.gz".
```

> [!NOTE] 
> These are just a few of the available `grep` variants. There are other specialized versions for different file formats and use cases.


## `cut`: Extracting Columns or Fields from Text

**`cut`** is a command-line utility used to extract specific columns or fields from text data. It's particularly useful for working with tabular data.

### Common Options

1. **`-d:`** Specify the delimiter character.
```bash
cut -d ',' -f 2 file.csv
# extracts the second field (column) from `file.csv`, assuming the fields are separated by commas.
```
2. **`-c:`** Specify the character positions to extract.
```bash
cut -c 1-5 file.txt
# extracts characters 1 to 5 from each line of `file.txt`.
```
3. **`-f:`** Specify the fields to extract.
```bash
cut -f 1,3 file.csv
# extracts the first and third fields from `file.csv`.
```
4. **`- range:`** Specify a range of characters or fields.
```bash
cut -c 1-5 file.txt
# extracts characters 1 to 5 (same as using -c).

cut -f 2-5 file.csv
# extracts fields 2 to 5 from `file.csv`.
```

### Examples

**Extracting the second field from a CSV file:**
  ```bash
  cut -d ',' -f 2 file.csv
  ```
**Extracting characters 1 to 5 from each line of a file:**
  ```bash
  cut -c 1-5 file.txt
  ```
**Extracting fields 2 to 4 from a tab-delimited file:**
  ```bash
  cut -d '\t' -f 2-4 file.tsv
  ```

> [!TIP]
> The `-d` option is crucial for specifying the delimiter character used in your data. Common delimiters include commas (,), tabs (\t), and spaces.

## `tr`: Translating Characters

**`tr`** is a command-line utility used to translate characters from one set to another. It's often used for simple text manipulation tasks.

### Common Options

* **`-d:`** Delete characters.
   * Example: `tr -d '[:punct:]' file.txt` removes punctuation characters from `file.txt`.

### Examples

* **Convert lowercase letters to uppercase:**
  ```bash
  tr 'a-z' 'A-Z' < file.txt
  ```
* **Remove all vowels from a file:**
  ```bash
  tr -d 'aeiouAEIOU' < file.txt
  ```
* **Replace spaces with underscores:**
  ```bash
  tr ' ' '_' < file.txt
  ```

> [!NOTE]
> `tr` can also be used to squeeze repeated characters or translate characters based on a one-to-one mapping.


## `wc`: Word Count

**`wc`** is a command-line utility used to count the number of lines, words, and characters in a file or standard input.

### Common Options

1. **`-l:`** Count the number of lines.
   * Example: `wc -l file.txt` counts the number of lines in `file.txt`.
2. **`-w:`** Count the number of words.
   * Example: `wc -w file.txt` counts the number of words in `file.txt`.
3. **`-c:`** Count the number of characters.
   * Example: `wc -c file.txt` counts the number of characters in `file.txt`.

### Combining Options

You can combine these options to get multiple counts:

Example: 
```bash 
wc -lwc file.txt
# counts the number of lines, words, and characters in file.txt.
```

> [!NOTE] 
> The definition of a "word" can vary depending on the locale settings and other factors. However, `wc` generally uses whitespace (spaces, tabs, newlines) to delimit words.

## `sort`: Sorting Text Data

**`sort`** is a command-line utility used to sort lines of text based on various criteria.

### Common Options

1. **`-r:`** Reverse the sort order.
   ```bash 
   sort -r file.txt` # sorts the lines in descending order.
   ```
2. **`-n:`** Sort numerically.
   ```bash 
   sort -n file.txt` # sorts lines based on the numeric value of the first field.
   ```
3. **`-h:`** Sort human-readable numbers.
   ```bash 
   sort -h file.txt` # sorts lines based on human-readable numbers (e.g., "100K", "2M").
   ```
4. **`-o:`** Output to a file.
   ```bash 
   sort -o sorted_file.txt file.txt` # sorts `file.txt` and saves the result to `sorted_file.txt`.
   ```
5. **`-u:`** Unique.
   ```bash 
   sort -u file.txt` # removes duplicate lines.
   ```

> [!TIP] 
> The default sorting order is ascending, and the sorting is typically based on the first field unless you specify otherwise.

## `comm`: Comparing Files Line by Line

**`comm`** is a command-line utility used to compare two files line by line and output the lines that are unique to each file or common to both.

### Basic Usage

```bash
comm file1.txt file2.txt
```

This command will output three columns:

1. Lines unique to `file1.txt`
2. Lines unique to `file2.txt`
3. Lines common to both files

### Options

* **-1:** Suppress column 1 (lines unique to `file1.txt`).
* **-2:** Suppress column 2 (lines unique to `file2.txt`).
* **-3:** Suppress column 3 (lines common to both files).

### Example

```bash
comm -12 file1.txt file2.txt
```

This will output only the lines that are common to both `file1.txt` and `file2.txt`.

> [!NOTE] <b> Additional Notes:
> * The files must be sorted for `comm` to produce accurate results.
> * You can use `sort` to sort files before comparing them with `comm`.


## `sed`: A Stream Editor

**`sed`** (Stream Editor) is a powerful command-line tool used to manipulate text streams. It can edit, filter, and transform text based on regular expressions.

### Basic Usage

The general syntax for `sed` is:

```bash
sed 's/pattern/replacement/' file.txt
```

This command substitutes the first occurrence of `pattern` with `replacement` in `file.txt`.

### Common Options

* **`-e:`** Execute multiple commands.
* **`-n:`** Suppress automatic printing of lines.
* **`-i:`** Edit files in-place.
* **`-f:`** Read commands from a file.

### Basic Operations

1. **Substitution:**
   * Replace a pattern with a replacement string:
     ```bash
     sed 's/old_string/new_string/' file.txt
     ```
   * Replace all occurrences:
     ```bash
     sed 's/old_string/new_string/g' file.txt
     ```
   * Use backreferences:
     ```bash
     sed 's/\([a-z]\)\([A-Z]\)/\2\1/' file.txt
     ```
2. **Deletion:**
   * Delete lines matching a pattern:
     ```bash
     sed '/pattern/d' file.txt
     ```
   * Delete lines containing a specific character:
     ```bash
     sed '/^$/d' file.txt  # Delete empty lines
     ```
3. **Insertion:**
   * Insert text before a pattern:
     ```bash
     sed '/pattern/i\new text' file.txt
     ```
   * Insert text after a pattern:
     ```bash
     sed '/pattern/a\new text' file.txt
     ```
4. **Changing:**
   * Change the first character of each line to uppercase:
     ```bash
     sed 's/^./\u&/' file.txt
     ```

### Examples

* **Replace all occurrences of "old" with "new":**
  ```bash
  sed 's/old/new/g' file.txt
  ```
* **Delete lines containing "error":**
  ```bash
  sed '/error/d' file.txt
  ```
* **Insert a new line before lines starting with "#":**
  ```bash
  sed '/^#/i\new line' file.txt
  ```

> [!NOTE] <b> Remember:
> `sed` is a powerful tool with many advanced features. Refer to the `sed` manual page for a complete list of options and examples.

