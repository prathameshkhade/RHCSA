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

> [!TIP] <b> Remember:
>The `-d` option is crucial for specifying the delimiter character used in your data. Common delimiters include commas (,), tabs (\t), and spaces.

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


## wc
### options:
1.  l
2.  w
3.  c

## sort
### options:
1.  r
2.  n
3.  h
4.  o
5.  u

## comm (compare)

## sed