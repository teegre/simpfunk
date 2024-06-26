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

A program that prints character `A` followed by a `new line`.

| Char | ASCII | Binary (8-bit) |
|:----:|:-----:|:--------------:|
| A    | 65    | 01000001       |
| \n   | 10    | 00001010       |

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

### Executing programs

**sf** is an interpreter that runs **Simpfunk** programs.

```
sf --run my_program.sf
```

### Generating programs

**sf** can also generate a **Simpfunk** program out of a given string:

```
$ sf --gen 'Hello, world!'
Generating...
Generated 156 instructions in 0.13 seconds.
.+.+..+.+....+..+..+.+.+.+.+..+.+..+...+..+.+..+...+..+.+....+..+.+.+..+....+.+......+...+.+...+.+..+.+....+.+...+..+.+..+..+.+..+...+..+..+.+....+.+....+.:
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
### Compression/Decompression

**sf** can compress a program:

```
$ sf --compress hello.sf
Compressing...
Compressed 44.23% in 0.06 seconds.
0.0+1+1.2.5.4+7.3.5+9+8+8.9.10.14.6+16.17.15.6.11.4.13.20.20+18+16+12.14+30.13+29.33.9:
$
```

**sf** uses the LZ78 algorithm.

To save a compressed program, same as above:

```
$ sf --compress hello.sf > hello.sfx
Compressing...
Compressed 44.23% in 0.06 seconds.
$
```

Of course, it is possible to directly generate a compressed program like so:

```
$ sf --gen-c 'Hello, world!' -1
Generating...
Generated 168 instructions in 0.16 seconds.
Compressing...
Compressed 36.90% in 0.29 seconds.
0.0+1+1.2.5.1:3.8.5+8:10.8+4+4:9+16.7.6+9.7+14.12.6:22+4.15.6.23.0:23+20.30+20+25.30.19.37.36+22.23:35.22:
```

You can also run a compressed program:

```
$ sf --run hello.sfx
Hello, world!
$
```

To decompress a program, use:

```
$ sf --decompress hello.sfx
Decompressing...
100%
Decompressed in 0.06 seconds.
.+.+..+.+...:.+..+..+.+.+.:+.+..+.+..+..:.+..+.+..+..:.+..+.+....:+..+.+.+..+..:..+.+.....:.+...+.+...:+.+..+.+....:+.+...+..+.+.:.+..+.+..+..:.+..+..+.+..:..+.+....+.:
$
```
