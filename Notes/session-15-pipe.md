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
   * Example: `grep -i "hello" myfile.txt` searches for "hello" or "Hello" regardless of case.
2. **`-v:`** Invert match.
   * Example: `grep -v "error" logfile.txt` displays lines that *don't* contain "error".
3. **`-c:`** Count matches.
   * Example: `grep -c "pattern" file.txt` counts the number of lines containing "pattern".
4. **`-e:`** Extended regular expressions.
   * Example: `grep -e "pattern1\|pattern2" file.txt` searches for either "pattern1" or "pattern2".
    > [!NOTE] 
    > **You can also use the `egrep` command which is equivalent to `grep -e`**
5. **`-h:`** Suppress file names.
   * Example: `grep -h "pattern" file1.txt file2.txt` doesn't prepend file names to matches.
6. **`-H:`** Print file names with matches.
   * Example: `grep -H "pattern" file1.txt file2.txt` prints the filename before each match.
7. **`-A `num:** Print lines after the match.
   * Example: `grep -A 2 "pattern" file.txt` prints the matching line plus two lines after it.
8. **`-B `num:** Print lines before the match.
   * Example: `grep -B 2 "pattern" file.txt` prints the matching line plus two lines before it.
9. **`-C `num:** Print lines before and after the match.
   * Example: `grep -C 2 "pattern" file.txt` prints the matching line plus two lines before and after it.

> [!NOTE]  
> **These are just a few of the many options available for `grep`. Refer to the `grep` manual page (`man grep`) for a complete list and detailed explanations.**


### Types
1.  egrep
2.  fgrep
3.  pdfgrep
4.  zgrep
## cut
### options:
1.  d
2.  c
3.  f
4.  range using -
## tr
### options:
1.  d
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