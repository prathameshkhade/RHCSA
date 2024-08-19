# Lecture-13 

# File Globbing


## What is File Globbing?
File globbing means regression expressions. These are called as the `meta-characters` and also known as `wildcard characters` which are nothing but they are some keywords which are reserved for some specific pupose and they have a special meaning.

## Wildcard Characters

1.  **Asterisk (*):** Matches any number of characters (including zero).
    *   Example: *.txt matches all files ending with ".txt".
2.  **Question Mark (?):** Matches exactly one character.
    *   Example: le?ter.txt matches files like "letter.txt" or "later.txt".
3.  **Square Brackets ([]):** Matches any single character within the brackets.
    *   Example: [abc].txt matches "a.txt", "b.txt", or "c.txt".
    *   You can also specify a range: [a-z].txt matches any file starting with a lowercase letter and ending with ".txt".

> [!IMPORTANT] 
> * **Hyphen (-):** Used to specify a range of characters. Example: `[0-9]` matches any `single digit.`
> * **Limitation:** Ranges are limited to `single characters only`. You cannot use `[11-20]` to match numbers `11 to 20.`
> * **Escape Character (\\):** To match a literal character that has special meaning, precede it with a backslash.
Example: \[ matches the opening square bracket literally.

## Examples
*   ***.log:** Matches all files ending with `.log`.
*   **report_?.txt:** Matches files like `report_1.txt`, `report_2.txt`, etc.
*   **[abc]123.txt:** Matches `a123.txt`, `b123.txt`, or `c123.txt`.
[0-9][0-9].txt: Matches two-digit numbers followed by `.txt`.
*   **Remember:** Globbing is `case-sensitive` by default. To match both uppercase and lowercase letters, use [a-zA-Z].

#### By understanding these basic patterns, you can efficiently manage and manipulate files in your system.