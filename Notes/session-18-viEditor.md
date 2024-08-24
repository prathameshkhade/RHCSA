# Session 18: The `vi` Editor

## What is `vi`?
`vi` (Visual Editor) is a powerful text editor commonly used in Linux and Unix environments. It's known for its efficiency and versatility, especially when working with large text files.

## How `vi` Works: Modes

`vi` operates in three primary modes:

1. **Command Mode:** This is the default mode when you first open `vi`. You can enter commands to navigate, edit, and save the file.
2. **Insert Mode:** Used to insert text directly into the document. You enter this mode by pressing `i`, `a`, `o`, or `O`.
3. **Visual Mode:** Used to select blocks of text for editing or copying.

## Shortcuts in Visual Mode

* **`ZZ`:** Save and exit.
* **`A`:** Append text to the end of the current line.
* **`o`:** Open a new line below the current line.
* **`O`:** Open a new line above the current line.
* **`u`:** Undo the last change.
* **`yy`:** Yank (copy) the current line.
* **`dd`:** Delete the current line.
* **`p`:** Paste from the system clipboard.
* **`P`:** Paste before the cursor.
* **`d0`:** Delete from the beginning of the line to the cursor.
* **`d$`:** Delete from the cursor to the end of the line.
* **`w`:** Move the cursor to the beginning of the next word.
* **`w <filename>`:** Save the current file as a new file with the specified name.
* **Character-level commands:**
  * **`x`:** Delete the character under the cursor.
  * **`X`:** Delete the character before the cursor.
  * **`r`:** Replace the character under the cursor.
  * **`yw`:** Yank (copy) the current word.
  * **`<num>dw`:** Delete the specified number of words.

## Shortcuts in Command Mode

* **`:wq`:** Write (save) the file and quit.
* **`:q!`:** Quit without saving.
* **`:`:** Enter command mode (you're already in it).
* **`/pattern`:** Search forward for a pattern.
* **`?pattern`:** Search backward for a pattern.
* **`:set nu` or `set number`:** Set the number display option (shows line numbers).

## Opening Multiple Files in `vi`

```bash
vim file1.txt file2.txt
```

* **`:args`:** List the open files.
* **`:rew`:** Rewind to the first file.
* **`:n`:** Go to the next file.
* **`:syntax on`:** Enable syntax highlighting.
* **`:set all`:** List all current settings.

> [!TIP]
> **Remember:** `vi` can be intimidating at first, but with practice, you'll become proficient in its powerful features.
