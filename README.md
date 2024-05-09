# Simpfunk

**Simpfunk** is a simple and pretty useless esoteric programming language that prints out strings.

It was implemented in **ALGO**.

## Dependencies

[FR-ALGO](https://github.com/teegre/fr-algo)

## The language

**Simpfunk** has only 3 instructions: `+`, `.` and `:`

It has a **1-bit register** and a **buffer**.

`+` flips value in the register.

`.` appends current register's value to the buffer.

`:` prints 

### Example:

A program that prints character `A` followed by a new line.

| Char | ASCII | Binary (8-bit) |
|:----:|:-----:|:--------------:|
| A    | 65    | 01000001       |
| \n   | 13    | 00001010       |

Thus:

```
'A' character
  Instructions: | . | + | . | + | . | . | . | . | . | + | . | : |
Register state: | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 1 |
        Buffer: | 0 |   | 1 |   | 0 | 0 | 0 | 0 | 0 |   | 1 | - |

New line character
  Instructions: | + | . | . | . | . | + | . | + | . | + | . | + | . | : |
Register state: | 0 | 0 | 0 | 0 | 0 | 1 | 1 | 0 | 0 | 1 | 1 | 0 | 0 | 0 |
        Buffer: | - | 0 | 0 | 0 | 0 |   | 1 |   | 0 |   | 1 |   | 0 | - |
```

## sf

**sf** is an interpreter that runs **Simpfunk** programs.

```
sf --run my_program.sf
```

**sf** can also generate a **Simpfunk** program out of a given string:

```
$ sf --gen 'Hello, world!'
.+.+..+.+....+..+..+.+.+.+.+..+.+..+...+..+.+..+...+..+.+....+..+.+.+..+....+.+......+...+.+...+.+..+.+....+.+...+..+.+..+..+.+..+...+..+..+.+....+.+....+.+....+.+.+.+.:
$
```

To save the program in a file use:

`sf --gen 'Hello, world!' > hello.sf`

To add a `:` instruction for each character in the string use `-1` option:

`sf --gen 'Hello, world!' -1 > hello.sf`

To run the program:

```
$ sf --run hello.sf
Hello, world!
$
```

