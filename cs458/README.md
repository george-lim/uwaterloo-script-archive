sploit - CS 458 Sploit GDB Breakpoint Automation
===============

This project automates GDB breakpoint testing in sploit target programs to aid with memory manipulation.

1. [Features/Commands](#featurescommands)
1. [Usage](#usage)

# Features/Commands
`./sploit build sploit1` will simply call `gcc -Wall -ggdb sploit1.c -o sploit1`
`./sploit gdb sploit1` will build and run `gdb` on sploit1, creating a breakpoint in the `main` function of sploit1's target program.
`./sploit gdb sploit1 34 53` will build and run `gdb` on sploit1, creating breakpoints on line 34 and 53 in sploit1's target program.

# Usage
Copy `sploit` into Ugster environment's `~/uml/share` folder. Run `chmod 755 sploit` to give `sploit1` executable permissions. Note that all `sploit.c` files are expected to have a `#define TARGET <target path>` line. This is necessary because `./sploit gdb` uses this line to get the target program path.

Be sure specify your sploit program file name (omitting the .c file extension) when using `sploit`.

There is a `sploit-template.c` file that you may use to write your sploit programs. It already contains the `TARGET` definition.
