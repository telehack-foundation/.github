![TeleBASIC](https://raw.githubusercontent.com/telehack-foundation/.github/main/profile/svg/telebasic.svg)

# TeleBASIC Reference Guide

```
                               +*#+=.
              -=++==-:.:-    :@@@@@@%-.
            +@@@%##@@@@@@#. .******###+.
  :-:       #@@%###*:=*+*#%@@@@@@@@@@@@@@%#+=:.
 *@@@%+     .@@@@#-=#@@@@@@@@@@@@@@@@@@@@*=--+@@#+-.
 -@@@%#*:     ..-#@@@@@@@@@@@@@@@@@@@@%-=**:-@@@= :@@%*:
  +@@%%%+*. :=#@@@@@@@@@@@@@@@@%@@@@@+ *@@:=%@@@@#%*#+-**.
   #@@@*=.*@@@@@@@@@@@@%#*****=***##@:=-@@.**@@@+:=#-#@=
    #@##++@@@@@#####***#%%@@@@ =@%#%#+:#:#=**#%*=@#:@@#
     #@*+:=+**#@@@@@@@@@@@@@@@%--#%++-.=@:-:+#####%%#**-+#
      @#+=+=+=:*++++**#@@@@@@@@@@**==*@+=@#=.   .=+*###*=.
      =@*@*   -@@@@@@@@*-+%@@@@@%+#@@#**#=+#@@%%#*+-:
      :@@=    .@@@@@#%*.    ....=@@@@#+-
       @=       ...==.         -#++++##
       :                           =+-

Dartmouth DTSS TeleBASIC (c) 1964,1966,1969,1970,1971,1979,2023
```

## What is TeleBASIC?

TeleBASIC is the flavour of BASIC (Beginners' All-purpose Symbolic Instruction Code), used on [Telehack](https://telehack.com/).  TeleBASIC is based on the original Dartmouth BASIC, but with a large number of additional features, such as support for regular expressions, UNIX timestamps, many common hashing/encoding algorithms, multi-dimensional arrays, and the ability to use alphanumeric indices.

Features from other types of BASIC such as HP2000 Access BASIC and Commodore BASIC have been added for increased compatibility and functionality.

TeleBASIC has a wide user-base and is actively maintained by members of [The Telehack Foundation](https://github.com/orgs/telehack-foundation/people/).

## Table of Contents

 1. [Set Up Your Editor for BASIC Programming](#1-set-up-your-editor-for-basic-programming)
 2. [Comparing/Logical Operators](#2-comparing--logical-operators)
 3. [Variables and Data Types](#3-variables-and-data-types)
 4. [Arrays & Hashes](#4-arrays-and-hashes)
 5. [Command Overview](#5-command-overview)
 6. [FAQ](#6-faq)
 7. [ANSI Escape Sequences](#7-ansi-escape-sequences)


## 1. Set Up Your Editor for BASIC Programming

### Using External Text Editors

There are currently four user-made plugins, which enable syntax-highlighting in various editors:

 - [**Atom**](https://telehack.com/r/tg9sD)
 - [**Nova**](https://telehack.com/r/gDAbA)
 - [**Sublime Text 3**](https://telehack.com/r/lP7iz)
 - [**Visual Studio Code**](https://telehack.com/r/vxEjh)


### Using `PED`

You can also use the text editor `PED` within Telehack - a massively augmented version of the original program by Niek Albers.  Extra features include syntax highlighting, and the ability to run programs without closing the editor.

These features are accessible via emacs-style meta-key shortcuts.

To see a list of features type `M-x list-packages RET`.

#### What does that mean?

The "M" refers to the "meta" key on your keyboard (most often, this is the escape key) and "RET" refers to the "return" key.

For example, to enable BASIC syntax highlighting, you would press escape, then x, then type "basic" and hit return.

Thus, the shorthand would be `M-x basic RET`.

Additionally, you do not need to type the full name of the command.  It is sufficient to simply type `M-x ba RET`.

To run a BASIC program within `PED` type `M-x run RET`.

```
Command-line options
====================
ped /nomouse     disables mouse input support
ped /noexpand    disables tab expansion
ped /basic       enables BASIC syntax highlighting
ped /tablen=<n>  set tab length to <n>
```


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

- `OR` (bitwise "or" operation)

- `XOR` (exclusive "or" operation)

- `NOT` (negation)

- `EQV` (material equivalence)

- `IMP` (implication)

#### Results Returned by Logical Operations

Operation | Value | Value | Result
--------- | ----- | ----- | ------
`NOT`     | `X`   |       | `NOT X`
`NOT`     | True  |       | False
`NOT`     | False |       | True

Operation | Value | Value | Result
--------- | ----- | ----- | ------
`AND`     | `X`   | `Y`   | `X AND Y`
`AND`     | True  | True  | True
`AND`     | True  | False | False
`AND`     | False | True  | False
`AND`     | False | False | False

Operation | Value | Value | Result
--------- | ----- | ----- | ------
`OR`      | `X`   | `Y`   | `X OR Y`
`OR`      | True  | True  | True
`OR`      | True  | False | True
`OR`      | False | True  | True
`OR`      | False | False | False

Operation | Value | Value | Result
--------- | ----- | ----- | ------
`XOR`     | `X`   | `Y`   | `X XOR Y`
`XOR`     | True  | True  | False
`XOR`     | True  | False | True
`XOR`     | False | True  | True
`XOR`     | False | False | False

Operation | Value | Value | Result
--------- | ----- | ----- | ------
`EQV`     | `X`   | `Y`   | `X EQV Y`
`EQV`     | True  | True  | True
`EQV`     | True  | False | False
`EQV`     | False | True  | False
`EQV`     | False | False | True

Operation | Value | Value | Result
--------- | ----- | ----- | ------
`IMP`     | `X`   | `Y`   | `X IMP Y`
`IMP`     | True  | True  | True
`IMP`     | True  | False | False
`IMP`     | False | True  | True
`IMP`     | False | False | True

### Arithmetic Operators

TeleBASIC supports the following standard mathematical operators:

`()`, `^`, `**`, `mod`, `/`, `*`, `+`, and `-`.


## 3. Variables and Data Types

You can store either text or numeric values in variables.

Variable names can contain letters and digits, but they have to start with a letter (e.g `FOO`, `BAR123$`).

You cannot use reserved keywords (e.g [`FOR`](#for-x--startvalue-to-maxvalue-step-n), [`IF`](#if-expression-then-statements)) as variable names. You also cannot begin a variable name with one of the logical operator keywords (e.g. `ORIGIN` is invalid because it begins with `OR`).

Variable names are most often suffixed with a type definition character (called a "sigil"):

 - `$` represents a text (string) value
 - `%` represents a numeric (integer) value
 - `!` represents a numeric (single-precision) value

Strings MUST include the `$` sigil.  If a variable is missing a sigil, then it is a number.

For example:

```
10  NAME$ = "some name"
```

would represent a string variable `NAME$`, but

```
10  NAME = "some name"
```

...would throw a `TYPE MISMATCH ERROR`, since you cannot assign a string to a numeric variable.



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

... and indices do not need to be numeric.  Thus, you can create unordered lists (hashes) such as:

```
10  FAV$("fruit") = "Apple"
20  FAV$("vehicle") = "Bicycle"
30  FAV$("language") = "TeleBASIC"
```


## 5. Command Overview

### Index

#### A

- [`ACCESS`](#access)  Currently not implemented, does nothing
- [`ARG$`](#arg)  A string containing all command line arguments
- [`ARGC%`](#argc)  The number of arguments passed to the program
- [`ARGV$(n)`](#argvn)  An array containing all of the arguments passed to the program
- [`ASC(s$)`](#ascs)  Returns the ASCII value of the first character in the string `s$`
- [`ATN(n)`](#atnn)  Returns the arctangent (in radians) of the specified value `n`

#### B

- [`BIN$(n)`](#binn)  Returns the binary representation of the integer `n` as a string
- [`BRK(n)`](#brkn)  Currently not implemented, does nothing

#### C

- [`CALL`](#call)  Currently not implemented, does nothing
- [`CHR$(n)`](#chrn)  Convert an ASCII code `n` to its equivalent character
- [`CINT(n)`](#cintn)  Returns the nearest integer of the specified value
- [`CIRCLE`](#circle)  Currently not implemented, does nothing
- [`COLOR(a, b)`](#colora-b)  Changes the colours of the terminal
- [`CONT`](#cont)    Continue execution after STOP, END, Control-C, or runtime error
- [`COS(n)`](#cosn)  Returns the trigonometric cosine of the angle `n` (in radians)
- [`CSNG(n)`](#csngn)  Convert a specified value `n` to a single precision number

#### D

- [`D2R(n)`](#d2rn) Convert degrees to radians
- [`DATA n...`](#data-n) Store variables accessed by the program [`READ`](#read-n) statements
- [`DEF FNname(Argument) = Expression`](#def-fnnameargument--expression)  Define a function
- [`DEFDBL (Variable)`](#defdbl-variable)  Currently not implemented, does nothing
- [`DEFINT (Variable)`](#defint-variable)  Currently not implemented, does nothing
- [`DEFSNG (Variable)`](#defsng-variable)  Currently not implemented, does nothing
- [`DEFSTR (Variable)`](#defstr-variable)  Currently not implemented, does nothing
- [`DIM (Variable)`](#dim-variable)  Currently not implemented, does nothing
- [`DIR$`](#dir)  Returns the filenames in your local directory, separated by spaces
- [`DO`](#do)  Currently not implemented, does nothing
- [`DRAW`](#draw)  Currently not implemented, does nothing

#### E

- [`END`](#end)  End program execution silently, without additional output
- [`EOF(n)`](#eofn)  Returns file pointer information
- [`ERASE (arrays)`](#erase-arrays)  To eliminate arrays from a program
- [`EXP(n)`](#expn)  Return base of natural logarithms to the power of `n`

#### F

- [`FOR x = startValue TO maxValue [STEP n]`](#for-x--startvalue-to-maxvalue-step-n)  Execute a series of instructions
- [`FRE`](#fre)  Return available memory

#### G

- [`GOSUB (LineNumber)`](#gosub-linenumber)  Branch to a subroutine and return
- [`GOTO (LineNumber)`](#goto-linenumber)  Branch unconditionally to a specified line number

#### H

- [`HEIGHT`](#height)  Returns your terminal height
- [`HEX$(n)`](#hexn)  Returns hexadecimal value of the specified number `n`

#### I

- [`IF expression THEN statements`](#if-expression-then-statements)  Make a decision regarding program flow
- [`INKEY$`](#inkey)  Returns one character read from the terminal
- [`INPUT FileNo, var$`](#input-fileno-var)  Reads a line from an open file
- [`INPUT var$`](#input-var)  Read user input
- [`INPUT "prompt", var$`](#input-prompt-var)  Read user input
- [`INPUT varA$, varB$, ...`](#input-vara-varb-)  Read user input
- [`INPUT "prompt", varA$, varB$, ...`](#input-prompt-vara-varb-)  Read user input
- [`INSTR(string$, search$, startPos)`](#instrstring-search-startpos)  Returns the position of a substring
- [`INT (n)`](#int-n)  Truncate a value to a whole number
- [`ITM(fileNumber)`](#itmfilenumber)  Returns the number of a data item

#### L

- [`LEFT$(s$, n)`](#lefts-n)  Returns the leftmost `n` characters of `s$`
- [`LEN(s$)`](#lens)  Returns the number of characters in the specified string
- [`LET Variable = Value`](#let-variable--value)  Assigns a value to a variable
- [`LIN(n)`](#linn)  Returns `n` newlines
- [`LOCATE y, x`](#locate-y-x)  Change the cursor position to `y`, `x`
- [`LOG(n)`](#logn)  Returns the natural logarithm of `n`
- [`LOG10(n)`](#log10n)  Returns the natural logarithm of `n` (base 10)

#### M

- [`MID$(s$, n, [l])`](#mids-n-l)  Returns a substring of `l` characters from `s$` beginning with the `n`th character

#### N

- [`NINT(n)`](#nintn)  Returns the nearest integer of the specified value
- [`NUM(s$)`](#nums)  Returns the ASCII value of the first character in the string `s$`

#### O

- [`OCT$(n)`](#octn)  Returns the octal value of `n`
- [`ON NUMBER%`](#on-number)  Jump conditionally to a line number based on value given
- [`OPEN filename$, AS fileNumber`](#open-filename-as-filenumber)  Opens a file

#### P

- [`PCLEAR0`](#pclear0)  Currently not implemented, does nothing
- [`PCLEAR1`](#pclear1)  Currently not implemented, does nothing
- [`PEEK(n)`](#peekn)  Read a value from the specified memory location `n`
- [`PLAY`](#play)  Currently not implemented, does nothing
- [`PMODE0`](#pmode0)  Currently not implemented, does nothing
- [`POKE n, m`](#poke-n-m)  Write a byte of data `m` into the specified memory location `n`
- [`POLKEY$(n)`](#polkeyn)  Returns one character read from the terminal
- [`PORT%`](#port)  Returns the port from the currently logged in user
- [`POS(string$, search$, [startPos])`](#posstring-search-startpos)  Returns the position of a substring
- [`PRINT expression`](#print-expression)  Prints an expression to the screen
- [`PUT`](#put)  Currently not implemented, does nothing

#### R

- [`R2D(n)`](#r2dn)  Converts `n` radians to degrees
- [`READ n...`](#read-n)  or a file and assign to variable
- [`REC(n)`](#recn)  in the specified file
- [`RENUMBER [start,[inc]`](#renumber-startinc)  Renumbers the statements of the current program
- [`RESTORE`](#restore)  statements to be reread
- [`RETURN`](#return)  Return from a subroutine
- [`RIGHT$(s$, n)`](#rights-n)  Returns the rightmost `n` characters of `s$`
- [`RND(n)`](#rndn)  Returns a random number

#### S

- [`SCRATCH`](#scratch)  Delete a file from the disk
- [`SCREEN`](#screen)  Currently not implemented, does nothing
- [`SGN(n)`](#sgnn)  Returns the sign of the specified value `n`
- [`SIN(n)`](#sinn)  Returns the trigonometric sine of the angle `n` (in radians)
- [`SLEEP n`](#sleep-n)  Pauses the program for `n` seconds
- [`SOUND`](#sound)  Currently not implemented, does nothing
- [`SOUNDRND`](#soundrnd)  Currently not implemented, does nothing
- [`SPACE$(n)`, `SPC$(n)`, `SPA(n)`](#spacen-spcn-span)  Returns `n` spaces
- [`SQR(n)`](#sqrn)  Returns the square root of `n`
- [`STOP`](#stop)  Halts the program and prints the current line
- [`STR$(n)`](#strn)  Returns `n` as a string value
- [`STRING$(n, s$)`](#stringn-s)  Repeats the string `s$` `n` times
- [`SYS(n)`](#sysn)  HP2000 Access BASIC system information
- [`SYSTEM`](#end)  End program execution silently, without additional output

#### T

- [`TAB(n), TAB$(n)`](#tabn-tabn)  Returns `n` spaces (not tabs!)
- [`TAN(n)`](#tann)  Returns the trigonometric tangent of the angle `n` (in radians)
- [`TH_B64D$`](#th_b64d)  Returns argument decoded from base64
- [`TH_B64E$`](#th_b64e)  Returns argument encoded to base64
- [`TH_DEFGROUP$`](#th_defgroup)  Returns the user's defgroup, separated by spaces
- [`TH_EXEC`](#th_exec)  Executes a shell command and returns to the program
- [`TH_GMTIME[$]`](#th_gmtime)  Returns a human-readable UTC time for a timestamp
- [`TH_HASADMIN(sat$)`](#th_hasadminsat)  Returns 1 if the user has admin on `sat$`
- [`TH_HASBADGE(badge$)`](#th_hasbadgebadge)  Returns when the user earned `badge$`
- [`TH_HASLOGIN(host$)`](#th_hasloginhost)  Returns 1 if the user has login on `host$`
- [`TH_HASROOT(host$)`](#th_hasroothost)  Returns 1 if the user has root on `host$`
- [`TH_HASSYSOP(bbs$)`](#th_hassysopbbs)  Returns 1 if the user has sysop on `bbs$`
- [`TH_HOSTNAME$`](#th_hostname)  Returns current hostname or hostname of argument passed
- [`TH_LOCALTIME[$]`](#th_localtime)  Returns a human-readable local time for a timestamp
- [`TH_MD5BASE64$`](#th_md5base64)  Returns md5 hex of argument passed as base64
- [`TH_MD5HEX$`](#th_md5hex)  Returns md5 hex of argument passed as hex
- [`TH_MODEM$`](#th_modem)  Returns modem information depending on option passed
- [`TH_NETSTAT$`](#th_netstat)  Returns a netstat, separated by spaces
- [`TH_PLAN$`](#th_plan)  Returns the user's `.plan` as a string
- [`TH_RE(txt$,pat$,count,case)`](#th_retxtpatcountmodeignorecase)  Returns regex matches
- [`TH_RE$(txt$,pat$,ind$,case)`](#th_retxtpatindignorecase)  Returns regex matches
- [`TH_REV$(s$)`](#th_revs)  Returns the string `s$` in reverse order
- [`TH_SED$(txt$,find$,replace$,opt$)`](#th_sedtxtfindreplaceopt)  Substitute matched substring
- [`TH_SPRINTF$(fmt$,[...])`](#th_sprintffmt)  Returns a formatted string
- [`TH_STATUS$`](#th_status)  Returns the user's status as a string
- [`TH_SYSLEVEL`](#th_syslevel)  Returns the user's Telehack system level
- [`TH_TIME`](#th_time)  Returns the current UNIX timestamp
- [`TH_UUD$(s$)`](#th_uuds)  Decodes a uuencoded string
- [`TH_UUE$(s$)`](#th_uues)  Returns uuencoded form of input string
- [`TIM(n)`](#timn)  Returns values of time and date depending on `n`
- [`TIME$`](#time)  Returns the local system time
- [`TIMER`](#timer)  Returns the number of seconds since midnight
- [`TROFF`](#troff)  Stops tracing of program statements
- [`TRON`](#tron)  Starts tracing of program statements
- [`TYP(n)`](#typn)  Returns the type of the next record in a file

#### U

- [`UPS$(string)`](#upsstring)  Returns the uppercase value of the given string
- [`USER$`](#user)  Returns the current logged in user

#### V

- [`VAL(s$)`](#vals)  Returns the numeric value of `s$`

#### W

- [`WIDTH`](#width)  Returns your terminal width


## Detailed Overview

### `ABS(n)`

Returns the absolute value of the specified value `n`

```
10  PRINT ABS(-40)
```
```
 40
```


### `ACCESS`

Currently not implemented, does nothing


### `ARG$`

A string variable this is populated with a string containing the command line arguments when a BASIC program is run from the shell command prompt.

```
10  PRINT ARG$
```
```
@program foo bar
foo bar
```


### `ARGV$(n)`

An array containing all of the arguments passed to the program (see example for [`ARGC%`](#argc) below)


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


### `ASC(s$)`
Returns the ASCII value of the first character in the string `s$`

```
10  PRINT ASC("A")
```
```
 65
```

_See also [`NUM`](#nums)_


### `ATN(n)`

Returns the arctangent (in radians) of the specified value `n`

```
10  PI = 3.14159
20  PRINT ATN(1)
30  PRINT PI/4
```
```
 0.785
 0.785
```


### `BIN$(n)`

Returns the binary representation of the integer `n` as a string

```
10  PRINT BIN$(123)
```
```
1111011
```


### `BRK(n)`

Currently not implemented, does nothing


### `CALL`

Currently not implemented, does nothing


### `CHR$(n)`

Convert an ASCII code `n` to its equivalent character

```
10  PRINT CHR$(42)
```
```
*
```


### `CINT(n)`

Returns `n` rounded to the nearest integer, with 0.5 rounding away from 0

```
10  PRINT CINT(5.6)
20  PRINT CINT(5.5)
30  PRINT CINT(5.4)
40  PRINT CINT(-5.5)
```
```
 6
 6
 5
 -6
```

_See also [`NINT`](#nintn)_


### `CIRCLE`

Currently not implemented, does nothing


### `COLOR(a, b)`

Changes the background `b` and/or foreground `a` colour of the terminal

```
10  COLOR 3, 4
20  PRINT "Hello"
```
_Prints `Hello` with blue `b` background and yellow `a` foreground text.  A list of possible colours can be found with the command `SHOW COLORS`._

### `CONT`

Continue execution at the statement after STOP, END, Control-C, or runtime error.

```
>10 print 123 : STOP : print 456
>run
 1

   10  print 123 : STOP : print 456
                     ^
STOP AT LINE 10
>CONT
 456
>10 STOP
>20 print "back on track"
>run

   10  STOP
           ^
STOP AT LINE 10
>cont
back on track
```

Another example:
```
> 10  for x = 5 to 10
> 20    for y = 1 to 5
> 30      print 10 / (x-y)
> 40    next y
> 50  next x
>run
 2.500
 3.333
 5
 10

   30  print 10 / (x-y)
                       ^
DIVISION BY ZERO AT LINE 30

>  print "This caused a problem:" x, y
This caused a problem: 5              5
>  print "At line " sys(1)
At line 30
```

### `COS(n)`

Returns the trigonometric cosine of the angle `n`, given in radians

```
10  PI = 3.14159
20  PRINT COS(PI/6)
30  PRINT SQRT(3)/2
```
```
 0.866
 0.866
```


### `CSNG(n)`

Convert a specified value `n` to a single precision number

```
10  PRINT CSNG("3.45")
```
```
 3.450
```


### `D2R(n)`

Convert degrees to radians

```
10  PRINT D2R( 90 )
```
```
 1.571
```

_See also [`R2D`](#r2dn)_


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


### `DEF FNname(Argument) = Expression`

Define a function with the name `FNname` which accepts an `Argument` and returns the defined `Expression`.
The function name must always begin with `FN`, followed by an optional space.

```
10  DEF FN square(x) = x^2
20  DEF FNcube(x) = x^3
30  DEF FNtood$(s$) = s$ + "tood"
40  PRINT FNsquare(5),FNcube(5),FNtood$("foo")
```
```
 25             125           footood
```


### `DEFDBL (Variable)`

Declare a variable as double precision number (currently not implemented, does nothing)


### `DEFINT (Variable)`

Declare a variable as integer number (currently not implemented, does nothing)


### `DEFSNG (Variable)`

Declare a variable as single precision number (currently not implemented, does nothing)


### `DEFSTR (Variable)`

Declare a variable as string (currently not implemented, does nothing)


### `DIM (Variable)`

Define an array of a fixed size (currently not implemented, does nothing)


### `DIR$`

Returns the filenames in your local directory, separated by spaces

```
10  PRINT DIR$
```
```
advent.gam againstip.txt basic15.a2 bbslist.txt c8test.c8 changelog.txt colossus.txt command.txt crackdown.txt do-well.txt etewaf.txt finger.txt fireworks.vt fnord.txt future.txt hammurabi.bas hckr_hnd.txt ien137.txt jfet.a2 johnnycode.txt k-rad.txt learncode.txt leaves.txt lem.bas lostpig.gam mastermind.bas notes.txt orange-book.txt oregon.bas porthack.exe privacy.txt rogue.gam rootkit.exe satcom.man smile.c8 starwars.txt sysmon.txt telehack.txt ttest.vt underground.txt unix.txt valentin.vt wardial.exe wumpus.bas xmodem.exe zork.gam
```


### `DO`

Currently not implemented, does nothing


### `DRAW`

Currently not implemented, does nothing

### `END`

End execution of the program silently, without additional output (in contrast to [`STOP`](#stop)).
Note that `SYSTEM` is an alias for `END`.

```
10 PRINT "hello"
20 GOSUB 100
30 END
40 PRINT "WORLD"
50 RETURN
```

### `EOF(n)`

Returns -1 if the file pointer in file number `n` is currently at the end of the document, otherwise returns 0.

The reason for -1 being used to denote truth is that -1 is 11111111 in binary, and conversely, 0 is 00000000.

_See also [`TYP`](#typn)._


### `ERASE arrays`

Eliminate an array from the program.  Accepts a list of arrays.

```
10  A(1) = 123
20  A(2) = 456
30  B$( "foo" ) = "bar"
40  B$( "bar" ) = "baz"
50  ERASE A, B$
60  PRINT A(1) A(2) "'" B$( "foo" ) "' '" B$( "bar" ) "'"
```
```
 0  0 '' ''
```


### `EXP(n)`

Return the base of natural logarithms to the power of the specified value `n`

```
10  PRINT EXP(13)
```
```
 442413.392
```


### `FOR x = startValue TO maxValue [STEP n]`

Execute a series of instructions a specified number of times in a loop, optionally incrementing `x` by `n` each time.

Note that `FOR I=A TO B STEP S: ... : NEXT I` works like `I=A; do { ... } while ((I+=S) < B);` (in the C programming language), so the last `NEXT I` increases `I` one step beyond `B`.

```
10  FOR I = 1 TO 40
20  PRINT I
30  NEXT I
40  REM the I variable is now 41
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


### `FRE`

Return the available system memory in bytes

```
10  PRINT FRE
```
```
 1048576
```


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


### `GOTO (LineNumber)`

Branch unconditionally out of the normal program sequence to a specified line number

```
10  PRINT "Hello World!"
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

_You might want to use a [`SLEEP`](#sleep-n) statement here!_


### `HEIGHT`

Returns your terminal height


### `HEX$(n)`

Returns a string which represents the hexadecimal value of the specified number `n`

```
10  PRINT HEX$(127)
```
```
7F
```


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


### `INKEY$`

Returns one character read from the terminal. It will wait until a character is typed. For a non-blocking alternative, see [`POLKEY$`](#polkeyn)

```
10  A$ = INKEY$
20  PRINT A$
```


### `INPUT var$`

Shows the default prompt and reads input from the user and saves it into `var$`.

```
10  INPUT A$
20  PRINT A$
```

The builtin `INPUT$` variable has a similar effect, but can be used inside expressions:
```
10  NEVERLEN = LEN(INPUT$)
20  PRINT "You would have won if you had typed" ( 1 + NEVERLEN ) "letters"
```

### `INPUT "prompt", var$`

Shows `prompt$` and reads input from the user and saves it into `var$`. Note that the prompt must be a string literal, not a variable.

```
10  INPUT "Enter something>", A$
20  PRINT A$
```


### `INPUT varA$, varB$, ...`

Shows the default prompt and reads input from the user, splits it at commas, and saves it into `varA$`, `varB$`, ...

```
10  INPUT A$, B$, C$
20  PRINT A$, B$, C$
```


### `INPUT "prompt", varA$, varB$, ...`

Shows `prompt$` and reads input from the user, splits it at commas, and saves it into `varA$`, `varB$`, ... Note that the prompt must be a string literal, not a variable.

```
10  INPUT "Enter something>", A$, B$, C$
20  PRINT A$, B$, C$
```


### `INPUT FileNo, var$`

Reads a line from an open file and saves it into `var$`

```
10  INPUT# 1, A
20  PRINT A
```


### `INSTR(string$, search$, [startPos])`

Returns the position (indexed from 0) of `search$` within `string$`, or -1 if not found. If provided, begin searching at index `startPos`

```
10  TEXT$ = "Hello, World! Hello, Telehack!"
20  PRINT INSTR(TEXT$, "llo")
30  PRINT INSTR(TEXT$, "llo", 3)
40  PRINT INSTR(TEXT$, "foo")
```
```
 2
 16
 -1
```

_See also [`POS`](#posstring-search-startpos)_


### `INT (n)`

Truncate a value to a whole number (towards zero)

```
10  PRINT INT(5.6)
20  PRINT INT(-5.6)
```
```
 5
 -5
```


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


### `LEFT$(s$, n)`

Returns the leftmost `n` characters of the specified string `s$`

If `n` is negative, returns everything except the rightmost `ABS(n)` characters

```
10  A$ = "Hello World"
20  PRINT LEFT$(A$, 5)
30  PRINT LEFT$(A$, -3)
```
```
Hello
Hello Wo
```

_See also [`MID$`](#mids-n-l) and [`RIGHT$`](#rights-n)_


### `LEN(s$)`

Returns the number of characters in the specified string

```
10  A$ = "Hello World"
20  PRINT LEN(A$)
```
```
 11
```


### `LET Variable = Value`

Assigns a value to a variable.  Traditionally this is for use with constants, which are not supported in TeleBASIC, and so `LET` is superfluous.

```
10  LET A = 12345
20  PRINT A
```
```
 12345
```


### `LIN(n)`

Returns `n` newlines

```
10  PRINT "A" LIN(2) "B"
```
```
A

B
```


### `LOCATE y, x`

Change the cursor position to `y`, `x`

```
10  LOCATE 5, 5
```


### `LOG(n)`

Returns the natural logarithm of `n` using [Euler's Number](https://en.wikipedia.org/wiki/E_(mathematical_constant)) as the base

```
10  PRINT LOG(6)
```
```
 1.792
```


### `LOG10(n)`

Returns the natural logarithm of `n` using 10 as the base (decimal).

```
10  PRINT LOG10(6)
```
```
 0.778
```


### `MID$(s$, [n], [l])`

Returns a substring of `l` characters from `s$` beginning with the `n`th character (indexed from 1)

If `l` is omitted or zero, the rest of the string is returned. If `l` is negative, the end of the substring is indexed relative to the end of the string

If `n` is omitted, zero, or negative, the start of the substring is indexed relative to the end of the string.


```
10  A$ = "Hello World"
20  PRINT MID$(A$,3,3)
30  PRINT MID$(A$,3)
40  PRINT MID$(A$,3,-3)
50  PRINT MID$(A$,-3,3)
60  PRINT MID$(A$), MID$(A$,LEN(A$))
70  PRINT MID$(A$,-1)
```
```
llo
llo World
llo Wo
orl
d              d
ld             ld
```

_See also [`LEFT$`](#lefts-n) and [`RIGHT$`](#rights-n)_


### `NINT(n)`

Returns `n` rounded to the nearest integer, with 0.5 rounding towards 0

```
10  PRINT NINT(5.6)
20  PRINT NINT(5.5)
30  PRINT NINT(5.4)
40  PRINT NINT(-5.5)
```
```
 6
 5
 5
 -5
```

_See also [`CINT`](#cintn)_


### `NUM(s$)`

Returns the ASCII value of the first character in the string `s$`

```
10  PRINT NUM("A")
```
```
 65
```

_See also [`ASC`](#ascs)_
_Not to be confused with [`VAL(s$)`](#vals), which returns the numeric value of `s$`._


### `OCT$(n)`

Returns the octal value of `n`

```
10  PRINT OCT$(66)
```
```
 102
```


### `OPEN filename$, AS fileNumber`

Opens a file

```
10  OPEN "filename.txt", AS #1
```


### `ON NUMBER%`

Jump conditionally with [`GOTO`](#goto-linenumber)/[`GOSUB`](#gosub-linenumber), based on value given

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

If `NUMBER% <= 0`, the operation is a no-op. Generally `NUMBER%` is rounded down to nearest integer, but if `0 < NUMBER% < 1`, it will be rounded up instead.
```
10 number% = 3.5
20 ON number% GOTO 100, 200, 300
30 PRINT number% "did not invoke GOTO" : END
100 PRINT number%, ": GOTO 100" : number% = number% - 0.5 : GOTO 20
200 PRINT number%, ": GOTO 200" : number% = number% - 1   : GOTO 20
300 PRINT number%, ": GOTO 300" : number% = number% - 1   : GOTO 20
```
```
 3.500         : GOTO 300
 2.500         : GOTO 200
 1.500         : GOTO 100
 1             : GOTO 100
 0.500         : GOTO 100
 0 did not invoke GOTO
```

### `PCLEAR0`

Currently not implemented, does nothing


### `PCLEAR1`

Currently not implemented, does nothing


### `PEEK(n)`

Read a value from the specified memory location `n`

```
10  PRINT PEEK(1300)
```
```
 83
```


### `PLAY`

Currently not implemented, does nothing


### `PMODE0`

Currently not implemented, does nothing


### `POKE n, m`

Write a byte of data `m` into the specified memory location `n`

```
10  POKE 1300, 255
```


### `POLKEY$(n)`

Returns one character read from the terminal. When no key is hit within `n` seconds, it returns the empty string

```
10  A$ = POLKEY$(5)
20  REM This will wait 5 seconds, waiting for user input
30  PRINT A$
40  B$ = POLKEY$
50  REM The default wait is 1 second.
60  PRINT B$
```


### `PORT%`

Returns the port from the currently logged in user.  Not to be confused with the current socket (e.g 23 for telnet)

```
10  PRINT USER$ + " is logged in on port: " + STR$(PORT%)
```


### `POS(string$, search$, [startPos])`

Returns the position (indexed from 1) of `search$` within `string$`, or 0 if not found. If provided, begin searching at index `startPos`

```
10  TEXT$ = "Hello, World! Hello, Telehack!"
20  PRINT POS(TEXT$, "llo")
30  PRINT POS(TEXT$, "llo", 4)
40  PRINT POS(TEXT$, "foo")
```
```
 3
 17
 0
```

_See also [`INSTR`](#instrstring-search-startpos)_


### `PRINT expression`

Prints an expression to the screen

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

When `PRINT` is immediately followed by `@[n],`, the entire line is indented by `n` spaces:
```
> n = 9
> & @n, "nicely indented"
         nicely indented
```

### `PRINT #fileNumber[,recordNumber]; expression`

Prints a expression into an open file, with optional record (line) number

```
10  OPEN "myfile.txt", AS #1
20  PRINT# 1, "Hello world"
30  CLOSE #1
```


### `PRINT #fileNumber[,recordNumber];END`

Prints an EOF mark to a file, truncating the file at that record

```
10  PRINT #1;A$
20  PRINT #1,1;"Overwriting A$ in record 1"
30  PRINT #1,1;END : REM Truncates file at record 1
```

_Observe the placement of the `#` in `PRINT`, `AS`, and `CLOSE` statements in the above examples_


### `PUT`

Currently not implemented, does nothing


### `R2D(n)`

Converts `n` radians to degrees

```
10  PRINT R2D(1.2)
```
```
 68.755
```

_See also [`D2R`](#d2rn)_


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


### `READ #fileNumber[,recordNumber];variables`

Read a value from [`DATA`](#data-n) or a file and assign them to variables

```
10  READ #1;A$
20  READ #1,4;B$
```


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


### `RENUMBER [start,[inc]]`

Renumbers the statements of the current program in memory. When optional parameters are not specified, number starts at 10 and increments by 10 for each line. Can be abbrieviated to `REN` or `RENUM`. Useful if you want to add more lines between existing statements

```
>1 GOTO 2
>2 END
>REN
>LIST

   10  GOTO 20
   20  END
```

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


### `RIGHT$(s$, n)`

Returns the rightmost `n` characters of the specified string `s$`

```
10  A$ = "Hello World"
20  PRINT RIGHT$(A$, 5)
```
```
World
```

_See also [`LEFT$`](#lefts-n) and [`MID$`](#mids-n-l)_

`RIGHT$(s$,n)` has peculiar semantics when `LEN(s$) < n < 2*LEN(s$)`; if you want *up to `n`* characters and can guarantee `n > 0`, you may want to use [`MID$(s$, 1-n)`](#mids-n-l) instead:
```
> FOR i = 1 TO 14: PRINT i, RIGHT$("ABCDEF", i), MID$("ABCDEF",1-i): NEXT
 1             F              F
 2             EF             EF
 3             DEF            DEF
 4             CDEF           CDEF
 5             BCDEF          BCDEF
 6             ABCDEF         ABCDEF
 7             F              ABCDEF
 8             EF             ABCDEF
 9             DEF            ABCDEF
 10            CDEF           ABCDEF
 11            BCDEF          ABCDEF
 12            ABCDEF         ABCDEF
 13            ABCDEF         ABCDEF
 14            ABCDEF         ABCDEF
```

### `RND(n)`

If `n < 0`, returns a random number in the interval `[0, 1]` seeded by `n`

If `n = 0`, returns a random number in the interval `[0, 1]`

If `n > 0`, returns a random number in the interval `[0, n]`

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


### `SCREEN`

Currently not implemented, does nothing


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


### `SIN(n)`

Returns the trigonometric sine of the angle `n`, given in radians

```
10  PI = 3.14159
20  PRINT SIN(PI/6)
```
```
0.500
```


### `SLEEP n`

Pauses the program for `n` seconds

```
10  SLEEP 5
```


### `SOUND`

Currently not implemented, does nothing


### `SOUNDRND`

Currently not implemented, does nothing


### `SPACE$(n)`, `SPC$(n)`, `SPA(n)`

Returns `n` spaces

```
10  PRINT "ABC" SPACE$(10) "ABC"
```
```
abc          abc
```


### `SQR(n)`

Returns the square root of `n`

```
10  PRINT SQR(36)
```
```
 6
```


### `STOP`

Halts the program and prints the current line.  Useful for debugging programs


### `STR$(n)`

Returns `n` as a string value

```
10  PRINT STR$(12345)
```
```
12345
```


### `STRING$(n, s$)`

Repeats the string `s$` `n` times

```
10  PRINT STRING$(10, "A")
```
```
AAAAAAAAAA
```

### `SYS(n)`

HP2000 Access BASIC system information (compatibility function).

0. Last error code (or 0). Not implemented.
1. Last error line number or 0.
2. Last file number accessed or `0` (tty) or `-1` (none). Not implemented.
3. Returns 1 if BREAK key pressed. Not implemented.
4. Returns terminal type (always `0` for tty).

### `TAB(n)`, `TAB$(n)`

Returns `n` spaces (not tabs!)

```
10  PRINT "ABC" TAB$(10) "ABC"
```
```
abc          abc
```


### `TAN(n)`

Returns the trigonometric tangent of the angle `n`, given in radians

```
10  PI = 3.14159
20  PRINT TAN(PI/3)
30  PRINT SQRT(3)
```
```
 1.732
 1.732
```


### `TH_SYSLEVEL`

Returns the user's Telehack system level.  Optionally takes a username as argument.

```
10  PRINT TH_SYSLEVEL
20  PRINT TH_SYSLEVEL("quantx")
```
```
 12
 81
```

_The user executing the above code would evidently have **12** badges._


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


### `TH_HASADMIN(sat$)`

Returns 1 if the user has admin on `sat$`, otherwise 0

```
10  PRINT TH_HASADMIN("sat_BT 5")
```
```
 1
```


### `TH_DEFGROUP$`

Returns the user's defgroup, separated by spaces

```
10  PRINT TH_DEFGROUP$
```
```
 archer lorelei
```


### `TH_PLAN$`

Returns the user's `.plan` as a string

```
10  PRINT TH_PLAN$
```
```
  To write a BASIC program
  <3
```


### `TH_TIME`

Returns the current UNIX timestamp

```
10  PRINT TH_TIME
```
```
 1675018633.67413
```


### `TH_LOCALTIME[$]`

Returns a human-readable timestamp for the given UNIX timestamp, in the user's timezone.

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


### `TH_GMTIME[$]`

Returns a human-readable UTC time for the given UNIX timestamp with the same options as [`TH_LOCALTIME[$]`](#th_localtime)


### `TH_MODEM$`

Returns modem information depending on option passed:

 - `0` number
 - `1` filename
 - `2` hostname
 - `3` description
 - `4` baud rate
 - `5` administrator
 - `6` location


### `TH_HOSTNAME$`

Returns current hostname or hostname of argument passed.  Supports `OSPROBER` plugin.

```
10  PRINT TH_HOSTNAME$
```
```
telehack
```


### `TH_NETSTAT$`

Returns current netstat, or netstat of hostname passed as argument, separated by spaces

```
adaptex cotds mimsy oddjob oracle tandem veritas
```


### `TH_MD5HEX$`

Returns md5 hex of argument passed as hex

```
10  PRINT TH_MD5HEX$("FOO")
```
```
901890a8e9c8cf6d5a1a542b229febff
```


### `TH_MD5BASE64$`

Returns md5 hex of argument passed as base64

```
10  PRINT TH_MD5BASE64$("FOO")
```
```
kBiQqOnIz21aGlQrIp/r/w
```


### `TH_B64E$`

Returns argument encoded to base64

```
10  PRINT TH_B64E$("Telehack")
```
```
VGVsZWhhY2s=
```


### `TH_B64D$`

Returns argument decoded from base64

```
10  PRINT TH_B64D$("VGVsZWhhY2s=")
```
```
Telehack
```


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

_Note: variables assigned with `TH_EXEC` will have trailing `CRLF` characters, much like back-ticks in bash scripts._


### `TH_RE(txt$,pat$,countmode,ignorecase)`

Number context, returns a boolean (1 or 0) depending on regex match

```
10  IF TH_RE( "hello", "l{2}" ) THEN PRINT "it matches"
```
```
it matches
```

_If countmode is true, returns number of matches:_

```
10  PRINT TH_RE( "HELLO", "L", 1 )
```
```
 2
```


### `TH_RE$(txt$,pat$,ind,ignorecase)`

String context, returns single captured group of match

```
10  PRINT TH_RE$( "hello world", "he\w+" )
```
```
hello
```

_If an index `n` is provided, the string returned will be the `n`th captured group:_

```
10  PRINT TH_RE$( "FOO BAR BAZ BINGO BANGO", "BA...", 2 )
```
```
BANGO
```
_In the above example, the match returned is not "BAZ B", since the "B" in "BAZ" has already been consumed by the first match._

_If the index supplied is 0, it will return the final match.  If no index is supplied, it will return the first match._


### `TH_REV$(s$)`

Returns the string `s$` in reverse order

```
10  PRINT TH_REV$( "deliver" )
```
```
reviled
```


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


### `TH_SPRINTF$(fmt$,[...])`

Returns a formatted string based on given parameters:

   - `%%` - A percent sign
   - `%c` - A character with the given decimal number
   - `%s` - A string of characters
   - `%S` - A string of characters, left aligned
   - `%d` - A signed integer, in decimal
   - `%b` - An unsigned integer, in binary
   - `%u` - An unsigned integer, in decimal
   - `%o` - An unsigned integer, in octal
   - `%x` - An unsigned integer, in hexadecimal
   - `%a` - Hexadecimal floating point
   - `%n` - Interprets width as positional index (see [example 2](#example-2))
   - `%r` - Returns a random value from the list as a string
   - `%e` - A floating-point number, in scientific notation
   - `%f` - A floating-point number, in fixed decimal notation
   - `%g` - A floating-point number, in `%e` or `%f` notation
   - `%h` - A floating-point number, in IEEE-754 notation
   - `%i` - Exactly like `%d`, for compatibility, or something
   - `%y` - Returns the decimal form of a hexadecimal unsigned int value
   - `%z` - Returns decimal form of IEEE-754 input value
   - `%D` - Like `%d`, but longer
   - `%U` - Like `%u`, but longer
   - `%O` - Like `%o`, but longer
   - `%F` - Like `%f`, but longer
   - `%B` - Like `%b`, but LOUDER
   - `%R` - Like `%r`, but left-aligned
   - `%X` - Like `%x`, but using upper-case letters
   - `%E` - Like `%e`, but using an upper-case "E"
   - `%G` - Like `%g`, but with an upper-case "E" (if applicable)
   - `%H` - Like `%h`, but using upper-case letters
   - `%A` - Like `%a`, but using upper-case letters

#### Example 1:

```
10  F$ = "%s likes to %s while %sing"
20  PRINT TH_SPRINTF$( F$, "Sam", "sing", "cook" )
30  PRINT TH_SPRINTF$( F$, "Izumi", "read", "relax" )
40  PRINT TH_SPRINTF$( F$, "Wumpus", "tood", "tood" )
```
```
Sam likes to sing while cooking
Izumi likes to read while relaxing
Wumpus likes to tood while tooding
```

#### Example 2:

```
10  PRINT TH_SPRINTF$( "%2n%1n%1n", "na", "Ba" )
```
```
Banana
```

#### Example 3:

```
10  PRINT TH_SPRINTF$("%42R...YOU LOSE","HEADS","TAILS")
```
```
TAILS                                     ...YOU LOSE
```

#### Example 4:

```
10  F$ = "I got %08b problems but leading zeros ain't %08b."
20  PRINT TH_SPRINTF$( F$, 99, 1 )
```
```
I got 01100011 problems but leading zeros ain't 00000001.
```

#### Example 5:

```
10  DATA "Name", "Car", "Country"
20  DATA "----", "---", "-------"
30  DATA "Bill", "Volvo", "New Zealand"
40  DATA "Alex", "Ferrari", "Italy"
50  DATA "Wumpus", "Tesla", "United States"
60  FOR I = 1 TO 5
70  READ A$, B$, C$
80  PRINT TH_SPRINTF$("%10S%12S%12S", A$, B$, C$)
90  NEXT I
```
```
Name      Car         Country
----      ---         -------
Bill      Volvo       New Zealand
Alex      Ferrari     Italy
Wumpus    Tesla       United States
```


### `TH_STATUS$`

Returns the user's status as a string


### `TH_UUD$(s$)`

Decodes a uuencoded string

```
10  PRINT TH_UUD$("#9F]O")
```
```
foo
```


### `TH_UUE$(s$)`

Returns uuencoded form of input string

```
10  PRINT TH_UUE$("foo")
```
```
#9F]O
```


### `TIM(n)`

Returns values of time and date depending on `n`

 - `0` - Current minute (0-59)
 - `1` - Current hour (0-23)
 - `2` - Current day (1-366)
 - `3` - Current year (0-99)
 - `4` - Current second (0-59)

```
10  PRINT TIM(0)
```
```
 29
```


### `TIME$`

Returns the local system time

```
10  PRINT TIME$
```
```
07:49:38
```


### `TIMER`

Returns the number of seconds since midnight

```
10  PRINT TIMER
```
```
 28210
```


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


### `TROFF`

Stops tracing of program statements.  Useful for debugging


### `TRON`

Starts tracing of program statements.  Useful for debugging


### `UPS$(string)`

Returns the uppercase value of the given string

```
10  PRINT UPS$("hello")
```
```
HELLO
```


### `USER$`

Returns the current logged in user

```
10  PRINT USER$
```
```
archer
```


### `VAL(s$)`

Returns the numeric value of `s$`

```
10  PRINT VAL("12345")
```
```
 12345
```

_Not to be confused with [`NUM(s$)`](#nums), which returns the ASCII value of the first character in the string `s$`._


### `WIDTH`

Returns your terminal width


## 6. FAQ

### **Q:** I need a `NAND` function, but there is none.

**A:** Create the function with:

```
DEF FNNAND( A, B ) = NOT ( A AND B )
```

Now you can call it with:

```
10  PRINT FNNAND( 0, 0 )
```
```
 1
```


### **Q:** How do I read from a file?

**A:** Like this:

```
10  OPEN "filename.txt", AS #1
20  IF EOF(1) THEN GOTO 60
30  INPUT# 1, A$
40  PRINT A$
50  GOTO 20
60  CLOSE #1
```


### **Q:** How do I write to a file?

**A:** Like this:

```
10  OPEN "filename.txt", AS #1
20  PRINT# 1, "Hello World!"
30  CLOSE #1
```


### **Q:** How do I _append_ a file?

**A:** You have to open the file and put the file-pointer at the end of file, like this:

```
10  OPEN "filename.txt", AS #1
20  IF EOF(1) THEN GOTO 50
30  INPUT# 1, DUMP$
40  GOTO 20
50  PRINT# 1, "We are now at the EOF, and appending stuff"
60  CLOSE #1
```

**A2:** The solution above (linear search) is somewhat slow for large files. [Exponential search](https://en.wikipedia.org/wiki/Exponential_search) is more complicated, but finds the end of a 10000-line file in ~`0.03` seconds instead of ~`31.6` seconds (1000x faster). Below is an example subroutine:
```
10 OPEN "filename.txt", AS #1
20 GOSUB 250 : 'probe now points to the last line, but file pointer DOES NOT NECESSARILY.
30 READ #1, probe; lastline$ : 'advance file pointer to probe
40 PRINT# 1, "We are now at EOF, and appending stuff"
50 PRINT "The previous last line", lastline$
60 CLOSE 1
200 END

250 probe=2 : DIM last(2) : last(0)=0 : last(-1)=2^52-1
255 '(0) is last good line , (-1) is last bad line (EOF), initialized to max int
260 READ #1, probe
265 ' read record at index (probe) from file #1, but not into any variables.
266 ' this is slightly faster than input#.
270 last(EOF(1)) = probe
275 'store the probed offset as either good or bad, depending on whether we hit EOF or not.
280 x = probe*2 : y = last(0) + INT((last(-1)-last(0))/2) : 'Exponential search for EOF
285 'halfway between last known good and last EOF (binary search)
290 probe = y XOR ((x XOR y) AND -(x < y))
295 ' probe = min(x,y); picks binary search when probe overshoots
300 IF probe > last(0) GOTO 260
305 ' probe>good implies (bad-good)/2>=1 implies EOF may lie beyond good+1; keep probing.
310 RETURN
```

### **Q:** How do I create a BBS?

**A:** You can create a BBS by running `PPPD.EXE`, and pointing it at your BASIC program file. Your BBS will then appear in `bbslist.txt`.

Your BBS baud-rate must be 115200 (11.520 kbps) in order for it to appear in the Telehack netstat.  To gain access to faster baud-rates requires you to upgrade your modem firmware (both `SYSADM` and `BLUEBOX` badges are required.)


### **Q:** How do I split a string into an array?

**A:** There are two methods. The [Traditional "Pure BASIC" Method](#traditional-pure-basic-method), and the [Modern RegEx Method](#modern-regex-method).  Both methods are detailed below.


#### Traditional "Pure BASIC" Method

This method involves iterating through your string `YOURSTRING$` and looking for a delimiter `DELIMITER$`.

For every iteration put the actual character at that position in the string `YOURSTRING$` in a temporary variable `TSTR$`.

Once you have found the delimiter `DELIMITER$`, save the result of the temporary variable `TSTR$` into an array. `MAXSTACK` tells you how many items are actually in the array.

See the example below:

```
 10  DIM ARRAY$(2)
 20  DELIMITER$ = " "
 30  YOURSTRING$ = "Hello World"
 40  MAXSTACK = 0
 45  REM PUT YOUR PROGRAM LOGIC HERE
 50  GOSUB 100
 55  REM PUT YOUR PROGRAM LOGIC HERE
 60  END
100  REM split
110  TSTR$ = ""
120  FOR I = 1 TO LEN(YOURSTRING$)
130  IF MID$(YOURSTRING, I, 1) = DELIMITER$ THEN GOTO 200
140  TSTR$ = TSTR$ + MID$(YOURSTRING$, I, 1)
150  IF I = LEN(YOURSTRING$) THEN GOTO 200
160  NEXT I
170  RETURN
200  REM We have found a delimiter and are pushing it into the array
210  MAXSTACK = MAXSTACK + 1
220  ARRAY$(MAXSTACK) = TSTR$
230  TSTR$ = ""
240  GOTO 160
```


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


### **Q:** How can I learn how to write regular expressions?

**A:** The executable `GOLF.EXE` contains multiple lessons on regular expressions.  You can also find many RegEx-related challenges in the `DOJO`.


### **Q:** How do I generate a random number?

**A:** Like this:

```
10  RANDOMIZE TIMER
20  MAXNR = 10
20  RNR = INT(RND(1)*MAXNR)
30  PRINT RNR
```

_The above example is a pseudorandom number generator, with [`TIMER`](#timer) being the seed._


### **Q:** I would like to code in BASIC, but all those line numbers are messy!

**A:** You don't actually have to use line numbers at all in TeleBASIC!  They are only necessary for when using [`GOTO`](#goto-linenumber) or [`GOSUB`](#gosub-linenumber).

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

Additionally, there is a script written by archer which allows you to use labels instead of numbers.

Find it on [archer's GitHub](https://p85.github.io/renumber/renumber.html).


### **Q:** How do I use `COMM.EXE` via BASIC?

**A:** Refer to [this guide by archer](https://telehack.com/r/pvELT).


### **Q:** What's with the fish?

**A:** That's our mascot, Bassy the dart-mouthed bass.


## 7. ANSI Escape Sequences

### General Info

An ANSI escape sequence is a sequence of ASCII characters, the first two of which are the ASCII "escape" character (`chr$(27)`) and the left-bracket character `[` (`chr$(91)`).

The character or characters following the escape and left-bracket characters specify an alphanumeric code that controls a keyboard or display function.

For example, these can be used instead of, or in addition to [`LOCATE`](#locate-y-x) (for locating the cursor in the window); [`COLOR`](#colora-b) (for setting text and background colours) and getting the user's arrow-key input.

Using escape sequences can give you greater control over how your program displays its output.  Be aware that not all terminal types support some of these sequences, and your terminal must support 256-bit colours in order to display such colours.

Standard escape codes are prefixed with Escape, which is represented in the following ways:

| Format      | Value             |
| ------      | -----             |
| Ctrl-Key    | `^[`              |
| Octal       | `\033`            |
| Unicode     | `\u001b`          |
| Hexadecimal | `\x1b`            |
| Decimal     | `27`              |

This is then followed by the command, somtimes delimited by opening square bracket `[` known as a Control Sequence Introducer (CSI), optionally followed by arguments and the command itself.

Arguments are delimeted by semi colon (`;`).

For example `boldred$ = chr$(27) + "[1;31m"`.

### General ASCII Codes

| Name | Decimal | Octal | Hex    | C-escape | Ctrl-Key | Description      |
| ---- | ------- | ----- | ---    | -------- | -------- | -----------      |
| `BEL`| 7       | 007   | `0x07` | `\a`     | `^G`     | Terminal bell    |
| `BS` | 8       | 010   | `0x08` | `\b`     | `^H`     | Backspace        |
| `HT` | 9       | 011   | `0x09` | `\t`     | `^I`     | Horizontal TAB   |
| `LF` | 10      | 012   | `0x0A` | `\n`     | `^J`     | Linefeed         |
| `VT` | 11      | 013   | `0x0B` | `\v`     | `^K`     | Vertical TAB     |
| `FF` | 12      | 014   | `0x0C` | `\f`     | `^L`     | Formfeed         |
| `CR` | 13      | 015   | `0x0D` | `\r`     | `^M`     | Carriage return  |
| `ESC`| 27      | 033   | `0x1B` | `\e`     | `^[`     | Escape character |
| `DEL`| 127     | 177   | `0x7F` | `<none>` | `<none>` | Delete character |

_Note: Some control escape sequences, like `\e` for ESC, are not guaranteed to work in all languages and compilers. It is recommended to use the decimal, octal or hex representation as escape code._

_The Ctrl-Key representation is simply associating the non-printable characters from ASCII code 1 with the printable characters from ASCII code 65 ("A"). ASCII code 1 would be `^A` (Ctrl-A), while ASCII code 7 (BEL) would be `^G` (Ctrl-G). This is a common representation (and input method) and historically comes from one of the VT series of terminals._


### Cursor Controls

| Sequence               | Description                                          |
| --------               | -----------                                          |
| `ESC[H`                | Moves cursor to home position (0, 0)                 |
| `ESC[{line};{column}H` | Moves cursor to line #, column #                     |
| `ESC[{line};{column}f` | Moves cursor to line #, column #                     |
| `ESC[#A`               | Moves cursor up # lines                              |
| `ESC[#B`               | Moves cursor down # lines                            |
| `ESC[#C`               | Moves cursor right # columns                         |
| `ESC[#D`               | Moves cursor left # columns                          |
| `ESC[#E`               | Moves cursor to start of next line, # lines down     |
| `ESC[#F`               | Moves cursor to start of previous line, # lines up   |
| `ESC[#G`               | Moves cursor to column #                             |
| `ESC[6n`               | Request cursor position (reports as ESC[#;#R)        |
| `ESC7`                 | Save cursor position (DEC)                           |
| `ESC8`                 | Restores the cursor to the last saved position (DEC) |
| `ESC[s`                | Save cursor position (SCO)                           |
| `ESC[u`                | Restores the cursor to the last saved position (SCO) |
| `ESC[?25h`             | Show cursor                                          |
| `ESC[?25l`             | Hide cursor                                          |

_Note: Some sequences, like saving and restoring cursors, are private sequences and are not standardized. While some terminal emulators (i.e. xterm and derived) support both SCO and DEC sequences, they are likely to have different functionality. It is therefore recommended to use DEC sequences._

### Erase Functions

| Sequence | Description                               |
| -------- | -----------                               |
| `ESC[J`  | Clears the screen                         |
| `ESC[0J` | Clears from cursor until end of screen    |
| `ESC[1J` | Clears from cursor to beginning of screen |
| `ESC[2J` | Clears entire screen                      |
| `ESC[K`  | Clears the current line                   |
| `ESC[0K` | Clears from cursor to end of line         |
| `ESC[1K` | Clears from cursor to start of line       |
| `ESC[2K` | Clears entire line                        |

### Colours / Graphics Mode / Character Attributes

| Sequence          | Reset Sequence | Description                          |
| --------          | -------------- | -----------                          |
| `ESC[1;34;{...}m` |                | Set graphics modes for cell          |
| `ESC[m`           |                | Reset all modes (styles and colours) |
| `ESC[0m`          |                | Same as above                        |
| `ESC[1m`          | `ESC[22m`      | Set bold mode.                       |
| `ESC[2m`          | `ESC[22m`      | Set dim/faint mode.                  |
| `ESC[3m`          | `ESC[23m`      | Set italic mode.                     |
| `ESC[4m`          | `ESC[24m`      | Set underline mode.                  |
| `ESC[5m`          | `ESC[25m`      | Set blinking mode                    |
| `ESC[7m`          | `ESC[27m`      | Set inverse/reverse mode             |
| `ESC[8m`          | `ESC[28m`      | Set hidden/invisible mode            |
| `ESC[9m`          | `ESC[29m`      | Set strikethrough mode.              |

_Note: Some terminals may not support some of the graphic mode sequences listed above._

_Both dim and bold modes are reset with the `ESC[22m` sequence. The `ESC[21m` sequence is a non-specified sequence for double underline mode and only works in some terminals and is reset with `ESC[24m`._

### Colour Codes

Most terminals support 8 and 16 colours, as well as 256 (8-bit) colours. These colours are set by the user, but have commonly defined meanings.

#### 8-16 Colours

| Colour  | Foreground | Background |
| ------  | ---------- | ---------- |
| Black   | 30         | 40         |
| Red     | 31         | 41         |
| Green   | 32         | 42         |
| Yellow  | 33         | 43         |
| Blue    | 34         | 44         |
| Magenta | 35         | 45         |
| Cyan    | 36         | 46         |
| White   | 37         | 47         |
| Default | 39         | 49         |
| Reset   | 0          | 0          |

_Note: the Reset colour is the reset code that resets all colours and text effects, Use Default colour to reset colours only._

Most terminals, apart from the set of 8 regular colours, also support the "bright" or "bold" colours. These have their own set of codes, mirroring the normal colours, but with an additional `;1` in their codes:

```
  e$ = chr$(27)

' Set style to bold, red foreground
  hello$ = e$ + "[1;31m" + "Hello"

' Set style to dimmed white foreground with red background
  world$ = e$ + "[2;37;41m" + "World"
```

Terminals that support the `aixterm` specification provide bright versions of the ISO colours, without the need to use the bold modifier:

| Colour         | Foreground | Background |
| ------         | ---------- | ---------- |
| Bright Black   | 90         | 100        |
| Bright Red     | 91         | 101        |
| Bright Green   | 92         | 102        |
| Bright Yellow  | 93         | 103        |
| Bright Blue    | 94         | 104        |
| Bright Magenta | 95         | 105        |
| Bright Cyan    | 96         | 106        |
| Bright White   | 97         | 107        |

#### 256 Colours

The following escape codes tells the terminal to use the given colour:

| Sequence         | Description           |
| --------         | -----------           |
| `ESC[38;5;{ID}m` | Set foreground colour |
| `ESC[48;5;{ID}m` | Set background colour |

Where `ID` should be replaced with the colour index from 0 to 255 of the following colour chart:

<img src="https://github.com/telehack-foundation/.github/raw/main/colour_chart.png" alt="ANSI Colour Chart">

_Generate this table with the following BASIC code:_

```
10  FOR I = 0 TO 255
20  S$ = TH_SPRINTF$( "%4S", I )
30  ? CHR$(27) "[38;5;" STR$(I) "m" S$ ;
40  IF NOT (I+1) MOD 16 THEN ?
50  NEXT
```

This table starts with the original 16 colours (0-15).

The proceeding 216 colours (16-231) are formed by a 3bpc RGB value offset by 16, packed into a single value.

The final 24 colours (232-255) are grayscale starting from a shade slighly lighter than black, ranging up to shade slightly darker than white.

Some emulators interpret these steps as linear increments (256 / 24) on all three channels, although some emulators may explicitly define these values.

#### RGB Colours

More modern terminals supports Truecolor (24-bit RGB), which allows you to set foreground and background colours using RGB values.

These escape sequences are usually documented poorly, if at all.

| Sequence                | Description                   |
| --------                | -----------                   |
| `ESC[38;2;{r};{g};{b}m` | Set foreground colour as RGB. |
| `ESC[48;2;{r};{g};{b}m` | Set background colour as RGB. |

_Note: `;38` and `;48` corresponds to the 16 colour sequence and is interpreted by the terminal to set the foreground and background colour respectively, whereas `;2` and `;5` sets the colour format._

### Common Private Modes

These are some examples of private modes, which are not defined by the specification, but are implemented in most terminals.

| Sequence     | Description                     |
| --------     | -----------                     |
| `ESC[?25l`   | Make cursor invisible           |
| `ESC[?25h`   | Make cursor visible             |
| `ESC[?47l`   | Restore screen                  |
| `ESC[?47h`   | Save screen                     |
| `ESC[?1049h` | Enables the alternative buffer  |
| `ESC[?1049l` | Disables the alternative buffer |

### DEC Special Graphics

DEC Special Graphics is a 7-bit character set developed by Digital Equipment Corporation.

This was used very often to draw boxes on the VT100 video terminal and the many emulators, and used by bulletin board software.

| Sequence  | Description                  |
| --------  | -----------                  |
| `ESC(0`   | Enable DEC special graphics  |
| `ESC(B`   | Disable DEC special graphics |


### Colour Examples (8-bit)

```
10  PRINT CHR$(27) + "[92mThe foreground is green" CHR$(27) "[m"
20  PRINT CHR$(27) + "[103mThe background is yellow" CHR$(27) "[m"
```

### Colour Examples (16-bit)

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
