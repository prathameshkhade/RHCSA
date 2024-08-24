## Regular Expressions with `grep`

Regular expressions are powerful tools for pattern matching in text processing. `grep` can leverage different flavors of regular expressions to search for complex patterns within files.

**Syntax:**

```bash
grep [OPTION] PATTERN FILE
```

* **OPTION:** Can include flags like `-E` or `-P` for specific regex flavors.
* **PATTERN:** The regular expression you want to search for.
* **FILE:** The file(s) to search within.

## Regular Expression Flavors:

1. **BRE (Basic Regular Expressions):** Use `-G` flag (default)
   * Simpler syntax.
   * Limited features compared to ERE and PRE.
2. **ERE (Extended Regular Expressions):** Use `-E` flag
   * More powerful syntax.
   * Supports features like character classes, backreferences, and grouping.
3. **PRE (Perl Compatible Regular Expressions):** Use `-P` flag
   * Most powerful syntax (similar to Perl regular expressions).
   * Supports advanced features like lookarounds, assertions, and possessive quantifiers.

## Useful Options:

* **`-e:`** Specify the search pattern as an argument instead of using a single quoted string.

## Metacharacters and Examples:

* **`^:`** Matches the beginning of the line.
   ```bash
   grep "^hello" file.txt  # Matches lines that start with "hello".
   ```
* **`$:`** Matches the end of the line.
   ```bash
   grep "world$" file.txt  # Matches lines that end with "world".
   ```
* **`. (dot):`** Matches any single character (except newline by default).
   ```bash
   grep "c.t" file.txt  # Matches "cat", "cut", "cot", etc.
   ```
* **`[] (character class):`** Matches any character within the brackets.
   ```bash
   grep "[aeiou]" file.txt  # Matches lines containing any vowel.
   ```
* **`- (hyphen):`** Inverts the character class (negation).
   ```bash
   grep "[^aeiou]" file.txt  # Matches lines without any vowels.
   ```
* **`* (asterisk):`** Matches the preceding character zero or more times.
   ```bash
   grep "col*or" file.txt  # Matches "color", "colour", "colooor", etc.
   ```


> [!TIP]
> **Remember:** There are many more metacharacters available in EREs. Refer to the `man grep` page for a complete list and explanations. 
> For more, refer [Pipes and Filter](./session-15-pipeFilter.md)