hexify - CS 241 Hexadecimal (.word) Converter
===============

This project outputs the hexadecimal representation (using the .word notation) of a file. It is meant to be used in conjunction with `cs241.wordasm` to translate assembly into MIPS code. Use the `-p` flag if the input file should be interpreted as a MIPS program, or the `-s` flag if the input should be interpreted as a string literal.

1. [Usage](#usage)

# Usage
Run `usage: ./hexify [-s | -p] <input file path> > <output file path>`. If you run into a permission error, run `chmod 755 hexify`.
Example usage: `./hexify -p input > output`.
