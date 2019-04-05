buildSuite - CS 246 Rapid Test Suite Creation
===============

This project allows students to create entire test suites from a single file. The script takes a buildSuite input file and creates the necessary `suiteq#.txt`, `<test>.in`, and `<test>.args` files.

1. [Writing Test Suites](#writing-test-suites)
1. [Usage](#usage)

# Writing Test Suites
Test suites are written in a specific buildSuite input format. While the syntax is intuitive, there are rules that must be followed for `buildSuite` to execute correctly.

To understand the syntax, consider the following `helloworld.txt` test suite input:

```
This is the input for the first test.
This is the second line for the input to the first test.
This is the third, etc.
This input will be saved in a .in file.
When you want to start a new test, you simply...


do this. Any number of blank lines will do.
We are now writing the input for the second test.
This test is called "test2", and the previous test is called "test1".
By default, test aliases are auto incremented with "test{#}"
To add a custom test alias...


"youDoThis"
This MUST be declared on the first line of a new test.
It is optional.
Custom test aliases MUST not contain whitespace.
Filename illegal characters are also not permitted.
What about adding arguments to tests?


/a -l -w
Adds the arguments "-l -w" to your test .args file.
It is also optional.
Arguments must be declared before writing input for your test.


Finally, to make comments, only single line
comments are currently supported.
// This comment will not be read.
also, // this comment will not be read.
Multi-line comments are not currently supported.

```

Please note that you **MUST** end your test file with a new line. Putting **EVERYTHING** all together, we can effectively produce test suites like this.

```
// a9q1.input

"printZero"
read a 0
print a

"incrementZero"
/a -l
read a 0
read b 1
add c a b
print c

// Only 1 argument, no test alias.
/a -d
read a 1
read a 0
print a

```

After running `buildSuite`, we would expect to produce a folder called `a9q1-tests` with the following files:

**suiteq1.txt**
```
printZero
incrementZero
test3

```

**printZero.in**
```
read a 0
print a

```

**incrementZero.in**
```
read a 0
read b 1
add c a b
print c

```

**incrementZero.args**
```
-l

```

**test3.in**
```
read a 1
read a 0
print a

```

**test3.args**
```
-d

```

# Usage
After writing your test suite, place the input file inside the directory containing the script.

Run `./buildSuite <test file path> <assignment #> <question #>`. If you run into a permission error, run `chmod 755 buildSuite`.
Example usage: `./buildSuite a3q1.txt 3 1`.
