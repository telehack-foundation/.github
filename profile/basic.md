# TeleBASIC Reference Guide

```
Dartmouth DTSS TeleBASIC (c) 1964,1966,1969,1970,1971,1979,2023
```

## What is TeleBASIC?

TeleBASIC is the flavour of [BASIC](https://en.wikipedia.org/wiki/BASIC) (Beginners' All-purpose Symbolic Instruction Code), used on [Telehack](https://telehack.com/).  TeleBASIC is based on [Dartmouth Time Sharing System](https://en.wikipedia.org/wiki/Dartmouth_Time_Sharing_System) BASIC, but with a large number of additional features, such as support for regular expressions, UNIX timestamps, many common hashing/encoding algorithms, multi-dimensional arrays, and the ability to use alphanumeric indeces.

Features from other types of BASIC such as [HP2000 Access BASIC](https://en.wikipedia.org/wiki/HP_Time-Shared_BASIC), and [Commodore BASIC](https://en.wikipedia.org/wiki/Commodore_BASIC) have been added for increased compatibility and functionality.

TeleBASIC is actively maintained by [The Telehack Foundation](https://github.com/orgs/telehack-foundation/people/).

<hr>

## Table of Contents

1. [Set Up Your Editor for BASIC Programming](#1-set-up-your-editor-for-basic-programming)
2. [Comparing/Logical Operators](#2-comparing--logical-operators)
3. [Variables and Data Types](#3-variables-and-data-types)
4. [Arrays & Hashes](#4-arrays-and-hashes)
5. [Command Overview](#5-command-overview)
6. [FAQ](#6-faq)
7. [ANSI Escape Sequences](#7-ansi-escape-sequences)

<hr>

## 1. Set Up Your Editor for BASIC Programming

### Using External Text Editors

There are currently four user-made plugins, which enable syntax-highlighting in various editors:

 - **Atom** - [Website](https://github.com/atom/atom) - [Plugin](https://atom.io/packages/language-thbasic)
 - **Sublime Text 3** - [Website](https://www.sublimetext.com/3) - [Plugin](https://github.com/thunderpoot/telebasic-sublime-syntax)
 - **Visual Studio Code** - [Website](https://code.visualstudio.com/) - [Plugin](https://marketplace.visualstudio.com/items?itemName=vscode-th-basic.vscode-th-basic)
 - **Nova** - [Website](https://nova.app/) - [Plugin](https://github.com/thunderpoot/NovaTeleBASIC)

##

### Using `PED`

You can also use the text editor `PED` within Telehack.  Based on [ped](https://github.com/daansystems/ped) by Niek Albers, but with a vast amount of extra features included, such as TeleBASIC syntax highlighting, and the ability to run basic programs without closing the editor.

These features are accessible via emacs-style meta-key shortcuts.

To see a list of available features within the editor, type:
```
M-x list-packages RET
```

#### What does that mean?

The "M" refers to the "meta" key on your keyboard (most often, this is the escape key) and "RET" refers to the "return" key.

For example, to enable BASIC syntax highlighting, you would press escape, then x, then type "basic" and hit return.  Thus, the shorthand would be `M-x basic RET`.

Additionally, you do not need to type the full name of the command.  It is sufficient to simply `M-x ba RET`.

To run a basic program within `PED` type `M-x r RET`.

```
Command-line options
====================
ped /nomouse     disables mouse input support
ped /noexpand    disables tab expansion
ped /basic       enables BASIC syntax highlighting
ped /tablen=<n>  set tab length to <n>
```

<hr>

## 2. Comparing / Logical Operators

### Comparing Operators

- `=` (equal to)
    ```
    10  A% = 0 : IF A% = 0 THEN PRINT "It is equal!"
    ```

- `>` (greater than)
    ```
    10  A% = 5 : IF A% > 0 THEN PRINT "It is greater!"
    ```

- `>=` (greater than or equal to)
    ```
    10  A% = 0 : IF A% >= 0 THEN PRINT "It is greater or equal!"
    ```

- `<` (less than)
    ```
    10  A% = -1 : IF A% < 0 THEN PRINT "It is less!"
    ```

- `<=` (less than or equal to)
    ```
    10  A% = 0 : IF A% <= 0 THEN PRINT "It is less or equal!"
    ```

- `<>` (not equal to)
    ```
    10  A% = 1 : IF A% <> 0 THEN PRINT "It is not equal!"
    ```


### Logical Operators

- `AND` (bitwise "and" operation)
    ```
    10  PRINT 5 AND 1
    ```

- `AND` (using within "if" to check if both conditions are true)
    ```
    10  A% = 3 : B% = 5
    20  IF A% = 3 AND B% = 5 THEN PRINT "Both conditions are true"
    ```

- `OR` (bitwise "or" operation)
    ```
    10  PRINT 5 OR 1
    ```

- `OR` (using within "if" to check if one condition is true)
    ```
    10  A% = 3 : B% = 5
    20  IF A% = 3 OR B% = 5 THEN PRINT "At least one condition is true"
    ```

- `XOR` (exclusive "or" operation)
    ```
    10  PRINT 1 XOR 0
    ```

- `NOT` (negation)
    ```
    10  PRINT NOT 0
    ```

<hr>

## 3. Variables and Data Types

You can store either text or numerical values in variables.

Variable names can contain letters and digits, but they have to start with a letter (e.g `FOO`, `BAR123$`).

You cannot use reserved keywords (e.g [`FOR`](#for-x--startvalue-to-maxvalue-step-n), [`IF`](#if-expression-then-statements)) as variable names.

Variable names are most often suffixed with a type definition character (called a "sigil"):

 - `$` represents a text (string) value
 - `%` represents a numeric (integer) value
 - `!` represents a numeric (single-precision) value

Strings MUST include the `$` sigil.  If a variable is missing a sigil, then it is a number.

For example:
```
10 NAME$ = "some name"
```
would represent a string variable `NAME$`, but
```
10 NAME = "some name"
```
...would throw a `TYPE MISMATCH ERROR`, since you cannot assign a string to a numeric variable.


<hr>

## 4. Arrays and Hashes

An array variable is basically a list of values.  These can be accessed by specifying an index number.
In traditional Dartmouth BASIC, we define a string array of size 10:
```
10  DIM MYLIST$(10)
```

Now we can modify the 5th Entry (note that the array index usually starts at 0, and can also be negative):
```
20  MYLIST$(4) = "some text"
```

TeleBASIC, however, does not require you to define the array's size before accessing it, so `DIM` is not necessary.

In addition to this, TeleBASIC allows for creation of multi-dimensional arrays, such as:
```
10  MYSTUFF( X, Y ) = 42
```

... and indexes do not need to be numerical.  So in essence, you can create unordered lists (hashes) such as:
```
10  FAV$("fruit") = "Apple"
20  FAV$("vehicle") = "Bicycle"
30  FAV$("language") = "TeleBASIC"
```

<hr>

## 5. Command Overview

### `ABS(n)`

Returns the absolute value of the specified value `n`
```
10  PRINT ABS(-40)
```
```
40
```
##

### `ACCESS`

Currently not implemented, does nothing
##

### `ASC(character)`, `NUM(character)`

Returns the ASCII-Code for its equivalent character
```
10  PRINT ASC(" ")
```
```
32
```

##

### `ARG$`

A string variable this is populated with a string containing the command line arguments when a BASIC program is run from the shell command prompt.
```
10  PRINT ARG$
```
```
@program foo bar
foo bar
```
##

### `ARGV$(n)`

An array containing all of the arguments passed to the program (see example for [`ARGC%`](#argc) below)

##

### `ARGC%`

The number of arguments passed to the program
```
10  FOR I = 0 TO ARGC%-1
20  PRINT ARGV$(I)
30  NEXT I
```
```
@program foo "hello world" bar
[run program.bas foo "hello world" bar]
program.bas
foo
hello world
bar
```
##

### `ASC(s$)`
Returns the ASCII value of the first character in the string `s$`
```
10  PRINT ASC("A")
```
```
 65
```
_See also [`NUM`](#nums)_
##

### `ATN(n)`

Returns the arctangent of the specified value `n`
```
10  PRINT ATN(40)
```
```
1.546
```
##

### `BIN$(n)`

Returns the binary representation of the integer `n` as a string
```
10  PRINT BIN$(123)
```
```
1111011
```
##

### `BRK(n)`

Currently not implemented, does nothing
##

### `CALL`

Currently not implemented, does nothing
##

### `CHR$(n)`

Convert an ASCII code `n` to its equivalent character
```
10  PRINT CHR$(42)
```
```
*
```
##

### `CINT(n)`

Returns the nearest integer of the specified value (9.5 becomes 10)
```
10  PRINT CINT(5.7)
```
```
 6
```
##

### `CIRCLE`

Currently not implemented, does nothing
##

### `COLOR(a, b)`

Changes the background `b` and/or foreground `a` color of the terminal
```
10  COLOR 3, 4
20  PRINT "Hello"
```
_Prints `Hello` with blue `b` background and yellow `a` foreground text.  A list of possible colors can be found with the command `SHOW COLORS`._

##

### `COS(n)`

Returns the cosinus of a specified value `n` in radians
```
10  PRINT COS(67)
```
```
 -0.517769799789505
```
##

### `CSNG(n)`
Convert a specified value `n` to a single precision number
```
10  PRINT CSNG("3.45")
```
```
 3.450
```
##

### `DATA n...`

Store the numeric and string constants that are accessed by the program [`READ`](#read-n) statements
```
10  DATA 4.1, 5.6, 9.98
20  READ A, B, C
30  PRINT A, B, C
```
```
 4.100          5.600          9.980
```
##

### `DEF FNname(Argument) = Expression`

Define a function with the name `FNname` which accepts an `Argument` and returns the defined `Expression`.
The function name must always begin with `FN`, followed by an optional space.
```
10 DEF FN square(x) = x^2
20 DEF FNcube(x) = x^3
30 PRINT FNsquare(5),FNcube(5)
```
```
 25       125
```
##

### `DEFDBL (Variable)`

Declare a variable as double precision number (currently not implemented, does nothing)
##

### `DEFINT (Variable)`

Declare a variable as integer number (currently not implemented, does nothing)
##

### `DEFSNG (Variable)`

Declare a variable as single precision number (currently not implemented, does nothing)
##

### `DEFSTR (Variable)`

Declare a variable as string (currently not implemented, does nothing)
##

### `DIM (Variable)`
Define an array of a fixed size (currently not implemented, does nothing)

##

### `DIR$`

Returns the filenames in your local directory, separated by spaces
```
10  PRINT DIR$
```
```
advent.gam againstip.txt basic15.a2 bbslist.txt c8test.c8 changelog.txt colossus.txt command.txt crackdown.txt do-well.txt etewaf.txt finger.txt fireworks.vt fnord.txt future.txt hammurabi.bas hckr_hnd.txt ien137.txt jfet.a2 johnnycode.txt k-rad.txt learncode.txt leaves.txt lem.bas lostpig.gam mastermind.bas notes.txt orange-book.txt oregon.bas porthack.exe privacy.txt rogue.gam rootkit.exe satcom.man smile.c8 starwars.txt sysmon.txt telehack.txt ttest.vt underground.txt unix.txt valentin.vt wardial.exe wumpus.bas xmodem.exe zork.gam
```
##

### `DO`

Currently not implemented, does nothing
##

### `DRAW`

Currently not implemented, does nothing
##

### `EOF(n)`

Returns -1 if the file pointer in file number `n` is currently at the end of the document, otherwise returns 0.

_See also [`TYP`](#typn)._
##

### `EXP(n)`

Return the base of natural logarithms to the power of the specified value `n`
```
10  PRINT EXP(13)
```
```
 442413.392
```
##

### `FOR x = startValue TO maxValue [STEP n]`

Execute a series of instructions a specified number of times in a loop, optionally incrementing `x` by `n` each time

```
10  FOR I = 1 TO 40
20  PRINT I
30  NEXT I
```
_This would run 40 times and output every time the current counter, incrementing `I` by 1 each time._

```
10  FOR I = 1 TO 40 STEP 2
20  PRINT I
30  NEXT I
```

_This would run 40 times and output the current counter in each iteration, and would increase `I` by 2 each time._
```
10  FOR I = 1 TO 0 STEP 0
20  PRINT I
30  NEXT I
```
_This would create an endless loop, printing `1` over and over until terminated._

##

### `GOSUB (LineNumber)`

Branch to a subroutine and return
```
 10  GOSUB 100
 20  PRINT "Now I'm back from the subroutine"
 30  END
100  REM Subroutine starts here
110  PRINT "I am now in the subroutine"
120  RETURN
```
```
I am now in the subroutine
Now I'm back from the subroutine
```
##

### `GOTO (LineNumber)`

Branch unconditionally out of the normal program sequence to a specified line number
```
 10  PRINT "Hello World!";
 20  GOTO 10
```
```
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
Hello World!
[...]
```
_You might want to use a [SLEEP](#sleep-n) statement here!_

##

### `HEIGHT`

Returns your terminal height
##

### `HEX$(n)`

Returns a string which represents the hexadecimal value of the specified number `n`
```
10  PRINT HEX$(127)
```
```
7F
```
##

### `IF expression THEN statements`

Make a decision regarding program flow based on the result of a returned expression

```
10  K = 3
20  J = 10
30  IF J > K THEN PRINT "J is bigger than K"
```
```
J is bigger than K
```
_See [section 2. Comparing/Logical Operators](#2-comparing--logical-operators)_

##

### `INKEY$`

Returns one character read from the terminal. It will wait until a character is typed. For a non-blocking alternative, see [`POLKEY$`](#polkeyn)
```
10  A$ = INKEY$
20  PRINT A$
```
##

### `INPUT prompt$, var$`

Shows `prompt$` and reads input from the users terminal and saves it into `var$`
```
10  INPUT "Enter something>", A$
20  PRINT A$
```
##

### `INPUT FileNo, var$`

Reads a line from an open file and saves it into `var$`
```
10 INPUT# 1, A
20 PRINT A
```
##

### `INSTR(string$, search$, startPos)`
Returns the position (starting with 0) of a substring within a string
```
10  TEXT$ = "Hello World"
20  SEARCHFOR$ = "W"
30  PRINT INSTR(TEXT$, SEARCHFOR$, 0)
```
```
 6
```
##

### `INT (n)`

Truncate a value to a whole number
```
10  PRINT INT(5.6)
```
```
 5
```
##

### `ITM(fileNumber)`

Returns the number of the data item currently pointed to in the current record of file `fileNumber`.
In TeleBASIC this will almost always be 1.
```
10  PRINT #1;A,B,C
20  READ #1,1;A
30  PRINT REC(1),ITM(1)
```
```
 1            2
```
##

### `LEFT$(String, Number)`

Returns a string that comprises the left-most specified number characters of a specified string
```
10  A$ = "Hello World"
20  B$ = LEFT$(A$, 5)
30  PRINT B$
```
```
Hello
```
##

### `LEN(String)`

Returns the number of characters in the specified string
```
10  A$ = "Hello World"
20  PRINT LEN(A$)
```
```
 11
```
##

### `LET Variable = Value`

Assigns a value to a variable.  Traditionally this is for use with constants, which are not supported in TeleBASIC, and so `LET` is superfluous.
```
10  LET A = 12345
20  PRINT A
```
```
 12345
```
##

### LIN(n)
Returns `n` newlines
```
10  PRINT "A" LIN(2) "B"
```
```
A

B
```
##

### `LOCATE y, x`

Change the cursors position to `y`, `x`
```
10  LOCATE 5, 5
```
##

### `LOG(n)`

Returns the natural logarithm of `n` using [Euler's Number](https://en.wikipedia.org/wiki/E_(mathematical_constant)) as the base
```
10  PRINT LOG(6)
```
```
 1.792
```
##

### `LOG10(n)`

Returns the natural logarithm of `n` using 10 as the base (decimal).
```
10  PRINT LOG10(6)
```
```
 0.778
```
##

### `MID$(s$, n, [l])`

Returns a string of `l` characters from `s$` beginning with the `n`th character
```
10  A$ = "Hello World"
20  PRINT MID$(A$,3,3)
```
```
llo
```
##

### `NINT(n)`

Returns the nearest integer of the specified value (9.5 becomes 9)
```
10  PRINT NINT(5.6)
```
```
 6
```
##

### `NUM(s$)`

Returns the ASCII value of the first character in the string `s$`
```
10  PRINT NUM("A")
```
```
 65
```
_See also [`ASC`](#ascs)_
##

### `OCT$(n)`

Returns a octal value of `n`
```
10  PRINT OCT$(66)
```
```
 102
```
##

### `OPEN filename¢, AS fileNumber`

Opens a file
```
10  OPEN "filename.txt", AS #1
```
##

### `ON NUMBER%`

Jump conditionally to [`GOTO`](#goto-linenumber)/[`GOSUB`](#gosub-linenumber), based on value given
```
 10  NUMBER% = 2
 20  ON NUMBER% GOTO 100,200,300
100  PRINT "Goto 100, will NOT jump here" : END
200  PRINT "Goto 200, will jump here" : END
300  PRINT "Goto 300, will NOT jump here" : END
```
```
Goto 200, will jump here
```
##
### `PCLEAR0`

Currently not implemented, does nothing
##

### `PCLEAR1`

Currently not implemented, does nothing
##

### `PEEK(n)`

Read a value from the specified memory location `n`
```
10  PRINT PEEK(1300)
```
```
 83
```
##

### `PLAY`

Currently not implemented, does nothing
##

### `PMODE0`

Currently not implemented, does nothing
##

### `POKE n, m`

Write a byte of data `m` into the specified memory location `n`
```
10  POKE 1300, 255
```
##

### `POLKEY$(n)`

Returns one character read from the terminal. When no key is hit within `n` seconds, it returns the empty string
```
10  A$ = POLKEY$(5)
20  REM This will wait 5 seconds, waiting for user input
30  PRINT A$
```
##

### `PORT%`

Returns the port from the currently logged in user.  Not to be confused with the current socket (e.g 23 for telnet)
```
10  PRINT USER$ + " is logged in on port: " + STR$(PORT%)
```
##

### `POS(s1$,s2$)`

Returns the position of `s2$` in `s1$` indexed from 1, or 0 if not found
```
10  A$="ABCDE"
20  PRINT POS(A$,"CD")
```
```
 3
```
##

### `PRINT expression`

Prints a expression to the screen
```
10  A = 5
20  B = 10
30  PRINT A + B
```
```
 15
```
```
10  A$ = "Hello "
20  B$ = "World"
30  PRINT A$;
40  PRINT B$
50  PRINT A$ + B$
60  PRINT A$ B$
```
```
Hello World
Hello World
Hello World
```
_`&` and `?` are available aliases for `PRINT`_

_Adding a `;` at the end of `PRINT` will suppress the newline_

##

### `PRINT #fileNumber[,recordNumber]; expression`

Prints a expression into an open file, with optional record (line) number
```
10  OPEN "myfile.txt", AS #1
20  PRINT# 1, "Hello world"
30  CLOSE #1
```
##

### `PRINT #fileNumber[,recordNumber];END`

Prints an EOF mark to a file, truncating the file at that record
```
10  PRINT #1;A$
20  PRINT #1,1;"Overwriting A$ in record 1"
30  PRINT #1,1;END : REM Truncates file at record 1
```
_Observe the placement of the `#` in `PRINT`, `AS`, and `CLOSE` statements in the above examples_

##

### `PUT`

Currently not implemented, does nothing
##

### `R2D(n)`

Converts `n` radians to degrees
##
```
10  PRINT R2D(1.2)
```
```
 68.755
```
##

### `READ n...`

Read a value from [`DATA`](#data-n) or a file and assign them to variables
```
10  DATA 4.1, 5.6, 9.98
20  READ A, B, C
30  PRINT A, B, C
```
```
 4.100          5.600          9.980
```
##

### `READ #fileNumber[,recordNumber];variables`

Read a value from [`DATA`](#data-n) or a file and assign them to variables
```
10  READ #1;A$
20  READ #1,4;B$
```
##

### `REC(n)`

Returns the current record number (line number) in the specified file. Starts at 1
```
10  OPEN "telehack.txt", AS #1
20  INPUT# 1, DUMP$
30  INPUT# 1, DUMP$
40  INPUT# 1, DUMP$
50  PRINT REC(1)
60  CLOSE #1
```
```
 3
```
##

### `RENUMBER [start,[inc]]`
Renumbers the statements of the current program in memory. When optional parameters are not specified, number starts at 10 and increments by 10 for each line. Can be abbrieviated to `REN` or `RENUM`. Useful if you want to add more lines between existing statements
```
>1 GOTO 2
>2 END
>REN
>LIST

   10 GOTO 20
   20 END

```
##

### `RESTORE`

Allow [`DATA`](#data-n) statements to be reread
```
10  DATA 4.1, 5.6, 9.98
20  READ A, B, C
30  PRINT A, B, C
40  RESTORE
50  READ A, B, C
60  PRINT A, B, C
```
```
 4.100          5.600          9.980
 4.100          5.600          9.980
```
##

### `RETURN`

Return from a subroutine, for use with [`GOSUB`](#gosub-linenumber).
```
10  GOSUB 30
20  END
30  PRINT "Hello"
40  RETURN
```
```
Hello
```
##

### `RIGHT$(s$, n)`

Returns the rightmost `n` characters of the specified string `s$`
```
10  A$ = "Hello World"
20  PRINT RIGHT$(A$, 5)
```
```
World
```
##

### `RND(n)`

If `n < 0`, returns a random number in the interval `[0, 1]` seeded by `INT(n)`

If `n = 0`, returns a random number in the interval `[0, 1]`

If `n > 0`, returns a random number in the interval `[0, INT(n)]`
```
10  PRINT RND(-5)
20  PRINT RND(0)
30  PRINT RND(5)
```
```
 0.249
 0.912
 2.376
```
##

### `SCRATCH`
Delete a file from the disk
```
10  SCRATCH "FOOBAR.TXT"
```
```
  ARE YOU SURE? Y/n y
  FOOBAR.TXT removed.
```
_Any input that is not `Y` (case insensitive) will cancel the operation._

Runs silently when run with variable assignment, i.e will not prompt for confirmation
```
10  PRINT "HELLO"
20  SCRATCH "FOOBAR.TXT" ; FOO$
30  PRINT "WORLD"
```
```
HELLO
WORLD
```
##

### `SCREEN`

Currently not implemented, does nothing
##

### `SGN(n)`

Returns the sign of the specified value `n`
```
10  PRINT SGN(5)
20  PRINT SGN(0)
30  PRINT SGN(-7)
```
```
 1
 0
 -1
```
##

### `SIN(n)`
Returns the trigonometric sine of the specified value `n` in radians
```
10  PRINT SIN(36)
```
```
 -0.991778853443116
```
##

### `SLEEP n`

Pauses the program for `n` seconds
```
10  SLEEP 5
```
##

### `SOUND`

Currently not implemented, does nothing
##

### `SOUNDRND`

Currently not implemented, does nothing
##

### `SPACE$(n)`, `SPC$(n)`, `SPA(n)`

Returns `n` spaces
```
10  PRINT "ABC" SPACE$(10) "ABC"
```
```
abc          abc
```
##

### `SQR(n)`

Returns the square root of `n`
```
10  PRINT SQR(36)
```
```
 6
```
##

### `STOP`
Halts the program and prints the current line.  Useful for debugging programs

##

### `STR$(n)`

Returns `n` as a string value
```
10  PRINT STR$(12345)
```
```
12345
```
##

### `STRING$(n, s$)`
Repeats the string `s$` `n` times
```
10  PRINT STRING$(10, "A")
```
```
AAAAAAAAAA
```
##

### `TAB(n)`, `TAB$(n)`

Returns `n` spaces (not tabs!)
```
10  PRINT "ABC" TAB$(10) "ABC"
```
```
abc          abc
```
##

### `TAN(n)`

Returns the trigonometric tangent of the specified value `n` in radians
```
10  PRINT TAN(38)
```
```
 0.310
```
##

### `TH_SYSLEVEL`

Returns the user's Telehack system level (int)
```
10  PRINT TH_SYSLEVEL
```
```
 12
```
_The user executing the above code would evidently have **12** badges._
##

### `TH_HASBADGE(badge$)`

Returns a UNIX timestamp of when the user earned `badge$`, or 0

```
10  PRINT TH_HASBADGE("ACCT")
```
```
 1559673339
```
```
10  PRINT TH_HASBADGE("ACCT", "doesntexist")
```
```
 0
```
##

### `TH_HASLOGIN(host$)`

Returns 1 if the user has login on `host$`, otherwise 0
```
10  PRINT TH_HASLOGIN("mimsy")
```
```
 1
```
```
10  PRINT TH_HASLOGIN("ames")
```
```
 0
```
##

### `TH_HASROOT(host$)`

Returns 1 if the user has root on `host$`, otherwise 0
```
10  PRINT TH_HASROOT("mimsy")
```
```
 1
```
```
10  PRINT TH_HASROOT("ames")
```
```
 0
```
##

### `TH_HASSYSOP(bbs$)`

Returns 1 if the user has sysop on `bbs$`, otherwise 0
```
10  PRINT TH_HASSYSOP("maccavern")
```
```
 1
```
```
10  PRINT TH_HASSYSOP("illuminati")
```
```
 0
```
##

### `TH_HASADMIN(sat$)`

Returns 1 if the user has admin on `sat$`, otherwise 0
```
10  PRINT TH_HASADMIN("sat_BT 5")
```
```
 1
```
##

### `TH_DEFGROUP$`

Returns the user's defgroup, separated by spaces
```
10  PRINT TH_DEFGROUP$
```
```
 archer lorelei
```
##

### `TH_PLAN$`

Returns the user's `.plan` as a string

```
10  PRINT TH_PLAN$
```
```
  To write a BASIC program
  <3
```
##

### `TH_TIME`

Returns the current UNIX timestamp
```
10  PRINT TH_TIME
```
```
 1675018633.67413
```
##

### `TH_LOCALTIME[$]`

Returns a human-readable local time for the given UNIX timestamp.
```
10  PRINT TH_LOCALTIME$(TH_TIME)
```
```
Wednesday, December 9, 2020 6:40:49 PM PST
```
Returns values of time and date if options are supplied, and no sigil:

 - `0` - `sec`
 - `1` - `min`
 - `2` - `hour`
 - `3` - `mday`
 - `4` - `mon`
 - `5` - `year`
 - `6` - `wday`
 - `7` - `yday`
 - `8` - `isdst`
```
10  FOR I = 0 TO 8 : PRINT TH_LOCALTIME(I,0) : NEXT I
```
```
 0
 0
 16
 31
 11
 69
 3
 364
 0
```
##

### `TH_GMTIME[$]`

Returns a human-readable UTC time for the given UNIX timestamp with the same options as [`TH_LOCALTIME[$]`](#th_localtime)
##

### `TH_MODEM$`

Returns modem information depending on option passed:

 - `0` number
 - `1` filename
 - `2` hostname
 - `3` description
 - `4` baud rate
 - `5` administrator
 - `6` location
##

### `TH_HOSTNAME$`

Returns current hostname or hostname of argument passed.  Supports `OSPROBER` plugin.

```
10  PRINT TH_HOSTNAME$
```
```
telehack
```
##

### `TH_NETSTAT$`

Returns current netstat, or netstat of hostname passed as argument, separated by spaces

```
adaptex cotds mimsy oddjob oracle tandem veritas
```
##

### `TH_MD5HEX$`

Returns md5 hex of argument passed as hex
```
10  PRINT TH_MD5HEX$("FOO")
```
```
901890a8e9c8cf6d5a1a542b229febff
```
##

### `TH_MD5BASE64$`

Returns md5 hex of argument passed as base64
```
10  PRINT TH_MD5BASE64$("FOO")
```
```
kBiQqOnIz21aGlQrIp/r/w
```
##

### `TH_B64E$`

Returns argument encoded to base64
```
10  PRINT TH_B64E$("Telehack")
```
```
VGVsZWhhY2s=
```
##

### `TH_B64D$`

Returns argument decoded from base64
```
10  PRINT TH_B64D$("VGVsZWhhY2s=")
```
```
Telehack
```
##

### `TH_EXEC`

Executes a shell command and returns to the current BASIC program
```
10  TH_EXEC "echo foo" : TH_EXEC "echo bar"
```
```
foo
bar
```
```
10  TH_EXEC "fnord", OUT$ : PRINT OUT$
```
```
The iguana from Austin will go to Austin.
```
_Note that variables assigned with `TH_EXEC` will have trailing `CRLF` characters, much like back-ticks in shell scripts._

##

### `TH_RE(txt$,pat$,countmode$,ignorecase)`

Number context, returns a boolean (1 or 0) depending on regex match
```
10  IF TH_RE( "hello", "l{2}" ) THEN PRINT "it matches"
```
```
it matches
```
_If countmode is true, returns number of matches_
```
10  PRINT TH_RE( "HELLO", "L", 1 )
```
```
 2
```
##

### `TH_RE$(txt$,pat$,ind$,ignorecase$)`

String context, returns single captured group of match
```
10  PRINT TH_RE$( "hello world", "he\w+" )
```
```
hello
```

_If an index `n` is provided, the string returned will be the `n`th captured group_

```
10  PRINT TH_RE$( "FOO BAR BAZ BINGO BANGO", "BA...", 2 )
```
```
BANGO
```
##

### `TH_SED$(txt$,find$,replace$,opt$)`

Stream editor, replaces matched substring with substitution

Available options:
   - "i" = case insensitive
   - "g" = global mode
```
10  PRINT TH_SED$( "foo bAR", "oo|ar", "izz", "gi" )
```
```
fizz bizz
```
##

### `TIM(n)`

Returns values of time and date depending on `n`

 - `0` - current minute (0-59)
 - `1` - current hour (0-23)
 - `2` - current day (1-366)
 - `3` - current year (0-99)
 - `4` - current second (0-59)

```
10  PRINT TIM(0)
```
```
 29
```
##

### `TIME$`
Returns the local system time
```
10  PRINT TIME$
```
```
07:49:38
```
##

### `TIMER`

Returns the number of seconds since midnight
```
10  PRINT TIMER
```
```
 28210
```
##

### `TYP(n)`

Returns the type of the next record in a file

Return values:
 - `1` - Numeric data (not currently working)
 - `2` - String data
 - `3` - End of file

```
 10  REM CREATE A FILE FOR TESTING
 20  FILENAME$ = "TEST" + STR$(INT(RND(1)*128*2)) + ".TXT"
 30  OPEN FILENAME$, AS #1
 40  REM POPULATE FILE WITH TEST DATA
 50  PRINT# 1, "some text"
 60  REM SAVE FILE
 70  CLOSE #1
 80  REM TEST TYP() COMMAND
 90  OPEN FILENAME$, AS #1
100  PRINT TYP(1)
110  REM ADVANCE ONE RECORD
120  INPUT# 1, DUMP$
130  PRINT TYP(1)
140  CLOSE #1
```
```
 2
 3
```

_See also [`EOF`](#eofn)._
##

### `TROFF`

Stops tracing of program statements.  Useful for debugging
##

### `TRON`

Starts tracing of program statements.  Useful for debugging
##

### `UPS$(string)`

Returns the uppercase value of the given string
```
10  PRINT UPS$("hello")
```
```
HELLO
```
##

### `USER$`

Returns the current logged in user
```
10  PRINT USER$
```
```
archer
```
##

### `WIDTH`

Returns your terminal width
##

### `VAL(s$)`

Returns the numerical value of `s$`
```
10  PRINT VAL("12345")
```
```
 12345
```
##

<hr>

## 6. FAQ

### `Q:` I need a `NAND` function, but there is none.

 `A:` Create the function with:
```
DEF FNNAND(v1, v2) = NOT (v1 AND v2)
```

Now you can call it with:

```
10  PRINT FNNAND(69, 420)
```
```
 0
```
##

### `Q:` How do I read from a file?

 `A:` Like this:
```
10  OPEN "filename.txt", AS #1
20  IF EOF(1) = -1 THEN GOTO 60
30  INPUT# 1, A
40  PRINT A
50  GOTO 20
60  CLOSE #1
```
##

### `Q:` How do I write to a file?

 `A:` Like this:
```
10  OPEN "filename.txt", AS #1
20  PRINT# 1, "Hello World!"
30  CLOSE #1
```

##

### `Q:` How do I _append_ a file?

 `A:` You have to open the file and put the file-pointer at the end of file, like this:
```
10  OPEN "filename.txt", AS #1
20  IF EOF(1) = -1 THEN GOTO 50
30  INPUT# 1, DUMPP$
40  GOTO 20
50  PRINT# 1, "We are now at the EOF, and appending stuff"
60  CLOSE #1
```

##

### `Q:` How do I create a BBS?

 `A:` You can create a BBS by running `PPPD.EXE`, and pointing it at your BASIC program file. Your BBS will then appear in `bbslist.txt`.

Your BBS baud-rate must be 115200 (11.520 kbps) in order for it to appear in the Telehack netstat.  To gain access to faster baud-rates requires you to upgrade your modem firmware (both `SYSADM` and `BLUEBOX` badges are required.)

##

### `Q:` How do I split a string into an Array?

 `A:` There are two methods. The [Traditional "Pure BASIC" Method](#traditional-pure-basic-method), and the [Modern RegEx Method](#modern-regex-method).  Both methods are detailed below.

##
#### Traditional "Pure BASIC" Method

This method involves iterating through your string `YOURSTRING$` and looking for a delimiter `DELIMITER$`.

For every iteration put the actual character at that position in the string `YOURSTRING$` in a temporary variable `TSTR$`.

Once you have found the delimiter `DELIMITER$`, save the result of the temporary variable `TSTR$` into an array. `MAXSTACK` tells you how many items are actually in the array.

See the example below:
```
 10  DIM ARRAY(2)
 20  DELIMITER = " "
 30  YOURSTRING = "Hello World"
 40  MAXSTACK = 0
 45  REM PUT YOUR PROGRAM LOGIC HERE
 50  GOSUB 100
 55  REM PUT YOUR PROGRAM LOGIC HERE
 60  END
100  REM split
110  TSTR = ""
120  FOR I = 1 TO LEN(YOURSTRING)
130  IF MID$(YOURSTRING, I, 1) = DELIMITER THEN GOTO 200
140  TSTR = TSTR + MID$(YOURSTRING, I, 1)
150  IF I = LEN(YOURSTRING) THEN GOTO 200
160  NEXT I
170  RETURN
200  REM We have found a delimiter and are pushing it into the Array
210  MAXSTACK = MAXSTACK + 1
220  ARRAY(MAXSTACK) = TSTR
230  TSTR = ""
240  GOTO 160
```
##

#### Modern RegEx Method

Let's say, for this example, you have the string `NAMES$` which is a list of names separated by a comma `,`.  To access this as an array is very straightforward using Telehack language extentions:
```
10  NAMES$ = "Tom,Dick,Harry,Bob,Steve,Imhotep"
20  PATTERN$ = "[^\,]+"
30  FOR I = 1 TO TH_RE(NAMES$,PATTERN$,1)
40  PRINT TH_RE$(NAMES$,PATTERN$,I)
50  NEXT I
```
```
Tom
Dick
Harry
Bob
Steve
Imhotep
```
_The above example uses both [`TH_RE`](#th_retxtpatcountmodeignorecase) (number context), and [`TH_RE$`](#th_retxtpatindignorecase) (string context)._

##

### `Q:` How can I learn how to write regular expressions?

 `A:` The executable `GOLF.EXE` contains multiple lessons on regular expressions.  You can also find many RegEx-related challenges in the `DOJO`.

##

### `Q:` How do I generate a random number?

 `A:` Like this:
```
10  RANDOMIZE TIMER
20  MAXNR = 10
20  RNR = INT(RND(1)*MAXNR)
30  PRINT RNR
```
_The above example is a pseudorandom number generator, with [`TIMER`](#timer) being the seed._

##

### `Q:` I would like to code in BASIC, but all those line numbers are messy!

 `A:` You don't actually have to use line numbers at all in TeleBASIC!  They are only necessary for when using [`GOTO`](#goto-linenumber) or [`GOSUB`](#gosub-linenumber).

You also don't have to put everything in uppercase, but doing so means your code will be more compatible with other historical flavours of BASIC.

Here is an example of a modern TeleBASIC program:

```
1 ' begin

input "What is your name? " n$
print "Hello, " n$ "! There are" len( n$ ) "characters in your name:"

for l = 1 to len( n$ )
    ? l ": " mid$( n$, l, 1 )
next : ?

input "Again? [y/n] " ; yn$
if yn$ = "y" then goto 1

? "Goodbye!"
end
```
```
What is your name? bob
Hello, bob! There are 3 characters in your name:
 1 : b
 2 : o
 3 : b

Again? [y/n] y
What is your name? steve
Hello, steve! There are 5 characters in your name:
 1 : s
 2 : t
 3 : e
 4 : v
 5 : e

Again? [y/n] n
Goodbye!

```

Additionally, there is a script written by archer which allows you to use labels instead of numbers.  You can find it on [archer's GitHub](https://p85.github.io/renumber/renumber.html).

##

### `Q:` How do I use `COMM.EXE` via BASIC?
 `A:` Refer to [this guide by archer](comm.md).
##

<hr>

## 7. ANSI Escape Sequences

### General Info

An ANSI escape sequence is a sequence of ASCII characters, the first two of which are the ASCII "escape" character (`chr$(27)`) and the left-bracket character `[` (`chr$(91)`).

The character or characters following the escape and left-bracket characters specify an alphanumeric code that controls a keyboard or display function.

For example, these can be used instead of, or in addition to [`LOCATE`](#locate-y-x) (for locating the cursor in the window); [`COLOR`](#colora-b) (for setting text and background colors) and getting the user's arrow-key input.

Using escape sequences can give you greater control over how your program displays its output.  Be aware that not all terminal types support some of these sequences, and your terminal must support 256-bit colors in order to display such colours.

Standard escape codes are prefixed with Escape, which is represented in the following ways:

 | Format      | Value
 | ------      | -----
 | Ctrl-Key    | `^[` (Hold `Ctrl` and type a left square bracket)
 | Octal       | `\033`
 | Unicode     | `\u001b`
 | Hexadecimal | `\'x1b`
 | Decimal     | `27` (`chr$(27)`)

This is then followed by the command, somtimes delimited by opening square bracket `[` known as a Control Sequence Introducer (CSI), optionally followed by arguments and the command itself.

Arguments are delimeted by semi colon (`;`), for example `boldred$ = chr$(27) + "[1;31m"`.

### General ASCII Codes

| Name | Decimal | Octal | Hex    | C-escape | Ctrl-Key | Description
| ---- | ------- | ----- | ---    | -------- | -------- | -----------
| `BEL`| 7       | 007   | `0x07` | `\a`     | `^G`     | Terminal bell
| `BS` | 8       | 010   | `0x08` | `\b`     | `^H`     | Backspace
| `HT` | 9       | 011   | `0x09` | `\t`     | `^I`     | Horizontal TAB
| `LF` | 10      | 012   | `0x0A` | `\n`     | `^J`     | Linefeed (newline)
| `VT` | 11      | 013   | `0x0B` | `\v`     | `^K`     | Vertical TAB
| `FF` | 12      | 014   | `0x0C` | `\f`     | `^L`     | Formfeed (also: New page NP)
| `CR` | 13      | 015   | `0x0D` | `\r`     | `^M`     | Carriage return
| `ESC`| 27      | 033   | `0x1B` | `\e`     | `^[`     | Escape character
| `DEL`| 127     | 177   | `0x7F` | `<none>` | `<none>` | Delete character

_Note: Some control escape sequences, like `\e` for ESC, are not guaranteed to work in all languages and compilers. It is recommended to use the decimal, octal or hex representation as escape code._

_The Ctrl-Key representation is simply associating the non-printable characters from ASCII code 1 with the printable characters from ASCII code 65 ("A"). ASCII code 1 would be `^A` (Ctrl-A), while ASCII code 7 (BEL) would be `^G` (Ctrl-G). This is a common representation (and input method) and historically comes from one of the VT series of terminals._
##

### Cursor Controls

| Sequence               | Description
| --------               | -----------
| `ESC[H`                | Moves cursor to home position (0, 0)
| `ESC[{line};{column}H` | Moves cursor to line #, column #
| `ESC[{line};{column}f` | Moves cursor to line #, column #
| `ESC[#A`               | Moves cursor up # lines
| `ESC[#B`               | Moves cursor down # lines
| `ESC[#C`               | Moves cursor right # columns
| `ESC[#D`               | Moves cursor left # columns
| `ESC[#E`               | Moves cursor to start of next line, # lines down
| `ESC[#F`               | Moves cursor to start of previous line, # lines up
| `ESC[#G`               | Moves cursor to column #
| `ESC[6n`               | Request cursor position (reports as ESC[#;#R)
| `ESC7`                 | Save cursor position (DEC)
| `ESC8`                 | Restores the cursor to the last saved position (DEC)
| `ESC[s`                | Save cursor position (SCO)
| `ESC[u`                | Restores the cursor to the last saved position (SCO)
| `ESC[?25h`             | Show cursor
| `ESC[?25l`             | Hide cursor

_Note: Some sequences, like saving and restoring cursors, are private sequences and are not standardized. While some terminal emulators (i.e. xterm and derived) support both SCO and DEC sequences, they are likely to have different functionality. It is therefore recommended to use DEC sequences._

### Erase Functions

| Sequence | Description
| -------- | -----------
| `ESC[J`  | Clears the screen
| `ESC[0J` | Clears from cursor until end of screen
| `ESC[1J` | Clears from cursor to beginning of screen
| `ESC[2J` | Clears entire screen
| `ESC[K`  | Clears the current line
| `ESC[0K` | Clears from cursor to end of line
| `ESC[1K` | Clears from cursor to start of line
| `ESC[2K` | Clears entire line

### Colours / Graphics Mode / Character Attributes

| Sequence          | Reset Sequence | Description
| --------          | -------------- | -----------
| `ESC[1;34;{...}m` |                | Set graphics modes for cell
| `ESC[m`           |                | Reset all modes (styles and colours)
| `ESC[0m`          |                | Same as above
| `ESC[1m`          | `ESC[22m`      | Set bold mode.
| `ESC[2m`          | `ESC[22m`      | Set dim/faint mode.
| `ESC[3m`          | `ESC[23m`      | Set italic mode.
| `ESC[4m`          | `ESC[24m`      | Set underline mode.
| `ESC[5m`          | `ESC[25m`      | Set blinking mode
| `ESC[7m`          | `ESC[27m`      | Set inverse/reverse mode
| `ESC[8m`          | `ESC[28m`      | Set hidden/invisible mode
| `ESC[9m`          | `ESC[29m`      | Set strikethrough mode.

_Note: Some terminals may not support some of the graphic mode sequences listed above._

_Both dim and bold modes are reset with the `ESC[22m` sequence. The `ESC[21m` sequence is a non-specified sequence for double underline mode and only works in some terminals and is reset with `ESC[24m`._

### Colour Codes

Most terminals support 8 and 16 colours, as well as 256 (8-bit) colours. These colours are set by the user, but have commonly defined meanings.

#### 8-16 Colours

| Colour  | Foreground | Background
| ------  | ---------- | ----------
| Black   | 30         | 40
| Red     | 31         | 41
| Green   | 32         | 42
| Yellow  | 33         | 43
| Blue    | 34         | 44
| Magenta | 35         | 45
| Cyan    | 36         | 46
| White   | 37         | 47
| Default | 39         | 49
| Reset   | 0          | 0

_Note: the Reset colour is the reset code that resets all colours and text effects, Use Default colour to reset colours only._

Most terminals, apart from the basic set of 8 colours, also support the "bright" or "bold" colours. These have their own set of codes, mirroring the normal colours, but with an additional `;1` in their codes:

```
  e$ = chr$(27)

' Set style to bold, red foreground
  hello$ = e$ + "[1;31m" + "Hello"

' Set style to dimmed white foreground with red background
  world$ = e$ + "[2;37;41m" + "World"
```

Terminals that support the `aixterm` specification provide bright versions of the ISO colours, without the need to use the bold modifier:

| Colour         | Foreground | Background
| ------         | ---------- | ----------
| Bright Black   | 90         | 100
| Bright Red     | 91         | 101
| Bright Green   | 92         | 102
| Bright Yellow  | 93         | 103
| Bright Blue    | 94         | 104
| Bright Magenta | 95         | 105
| Bright Cyan    | 96         | 106
| Bright White   | 97         | 107

#### 256 Colours

The following escape codes tells the terminal to use the given colour (`ID`):

| Sequence         | Description
| --------         | -----------
| `ESC[38;5;{ID}m` | Set foreground colour.
| `ESC[48;5;{ID}m` | Set background colour.

Where `ID` should be replaced with the color index from 0 to 255 of the following color table:

<img src="https://underwood.network/telehack/ansi_colours.png" alt="ANSI Colour Table">

_Generate this table with the following BASIC code:_
```
10  FOR I = 0 TO 255
20  ? CHR$(27) "[38;5;" STR$(I) "M" I ;
30  IF NOT I MOD 16 THEN ?
40  NEXT
```
This table starts with the original 16 colors (0-15).

The proceeding 216 colors (16-231) are formed by a 3bpc RGB value offset by 16, packed into a single value.

The final 24 colors (232-255) are grayscale starting from a shade slighly lighter than black, ranging up to shade slightly darker than white.

Some emulators interpret these steps as linear increments (256 / 24) on all three channels, although some emulators may explicitly define these values.

#### RGB Colours

More modern terminals supports Truecolor (24-bit RGB), which allows you to set foreground and background colours using RGB values.

These escape sequences are usually not well documented.

| Sequence                | Description
| --------                | -----------
| `ESC[38;2;{r};{g};{b}m` | Set foreground colour as RGB.
| `ESC[48;2;{r};{g};{b}m` | Set background colour as RGB.

_Note: `;38` and `;48` corresponds to the 16 colour sequence and is interpreted by the terminal to set the foreground and background colour respectively, whereas `;2` and `;5` sets the colour format._

### Common Private Modes

These are some examples of private modes, which are not defined by the specification, but are implemented in most terminals.

| Sequence     | Description
| --------     | -----------
| `ESC[?25l`   | Make cursor invisible
| `ESC[?25h`   | Make cursor visible
| `ESC[?47l`   | Restore screen
| `ESC[?47h`   | Save screen
| `ESC[?1049h` | Enables the alternative buffer
| `ESC[?1049l` | Disables the alternative buffer

### DEC Special Graphics

DEC Special Graphics is a 7-bit character set developed by Digital Equipment Corporation.

This was used very often to draw boxes on the VT100 video terminal and the many emulators, and used by bulletin board software.

| Sequence  | Description
| --------  | -----------
| `ESC(0`   | Enable DEC special graphics
| `ESC(B`   | Disable DEC special graphics

##

### Color Examples (8-bit)

```
10  PRINT CHR$(27) + "[92mThe foreground is green" CHR$(27) "[m"
20  PRINT CHR$(27) + "[103mThe background is yellow" CHR$(27) "[m"
```

### Color Examples (16-bit)

```
10  PRINT CHR$(27) + "[38;5;134mThe foreground is purple" CHR$(27) "[m"
20  PRINT CHR$(27) + "[48;5;117mThe background is sky blue" CHR$(27) "[m"
```

### Get Arrow Key Input

```
10  KEY$ = INKEY$
20  IF KEY$ = CHR$(27) THEN KEY$ = INKEY$ : IF KEY$ = "[" THEN GOTO 40
30  GOTO 10
40  KEY$ = INKEY$
50  IF KEY$ = "A" THEN PRINT "UP"
60  IF KEY$ = "B" THEN PRINT "DOWN"
70  IF KEY$ = "C" THEN PRINT "RIGHT"
80  IF KEY$ = "D" THEN PRINT "LEFT"
90  GOTO 10
```

<hr>

[Back to top](#)
