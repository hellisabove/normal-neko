# Neko
Unix /bin/cat like - concatenate files and print
out the standard output!


**Neko** is a very fast and lightweight implementaion of the `cat`
utility, written in [V](https://github.com/vlang/v).

# Features

## Performance
Even though **neko** does a lot of checks and replacements, it still performs toe-to-toe with `GNU cat`

```sh
❯ time (for i in {1..10}; do neko LICENSE > /dev/null; done)
0.03s user 0.02s system 11% cpu 0.430 total

❯ time (for i in {1..10}; do cat LICENSE > /dev/null; done)
0.01s user 0.02s system 84% cpu 0.030 total

```

# Installation

```sh
# Clone the repo
git clone https://github.com/hellisabove/normal-neko.git
# build
cd neko && v -prod .

```
# Specification
## NAME
**neko** -- concatenate files and print ouy the standard output

## SYNOPSIS
`neko [-benst] [file..] [-(stdin)]`

## DESCRIPTION

The **neko** utility reads files sequentially, writing them to the standard
output. The file operands are processed in command-line order. If file
is a single dash (‘-’) or absent, neko reads from the standard input.

The Options are as follows

| Option | Description                                                                                                  |
|--------|--------------------------------------------------------------------------------------------------------------|
| `-b`   | Number the lines, but don't count blank lines.                                                               |
| `-e`   | Print a dollar sign (‘$’) at the end of each line. Implies the -v option to display non-printing characters. |
| `-n`   | Number the output lines, starting at 1.                                                                      |
| `-s`   | Squeeze multiple adjacent empty lines, causing the output to be single spaced.                               |
| `-t`   | Print tab characters as `^I`. Implies the `-v` option to display non-printing characters.                    |
| `-u`   | The output is guaranteed to be unbuffered (*unimplemented*)                                                  |
| `-v`   | Displays non-printing characters so they are visible  (*unimplemented*)                                      |

## EXIT STATUS
The **neko** utility exits 0 on success, and >0 if an error occurs.

# EXAMPLES

1. Sequentially print the contents of `file1` and `file2` to the file
   `file3`, truncating `file3` if it already exists. See the manual page
   for your shell (e.g., sh(1)) for more information on redirection.


```sh
❯ neko file1 file2 > file3
```
   
2. Print the contents of `file1`, print data it receives from the
   standard input until it receives an `EOF` (‘^D’) character, print the
   contents of `file2`, read and output contents of the standard input
   again, then finally output the contents of `file3`. 
   
```sh
❯ neko file1 - file2 - file3
```

## CAVEATS
1. `-v` flag is *not* POSIX standard. As such, there are no plans to implement it

# CREDITS
A Lot of the `README.md` was taken from Openbsd's [cat(1) man page](https://man.openbsd.org/cat.1)
Flinner for creating neko
