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
**In essence, piping allows you to chain commands together to create complex workflows and perform data processing efficiently.**

# Filtering Commands

## grep
### options:
1.  i
2.  v
3.  c
4.  e
5.  h
6.  H
7.  A
8.  B
9.  C
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