# TeleBASIC Reference Guide
##

[Back to main](basic.md)
##

## How to Use `COMM.EXE` via BASIC
_By archer, 2018_

### `Q:` How do I write a program for use with `COMM.EXE`?

 `A:` See the example below:

Your program has to run in an infinite Loop.  Make sure `COMM.EXE` is running in another shell, and open a new session and run the BASIC program.

#### Simple Template:

```
 10  SLEEP 0.1
 20  TMO = 600
 25  CT = 0
100  OPEN "COM1:9600", AS #1
110  SLEEP 0.1
```
##

### `Q:` How do I accept an incoming call via `COMM.EXE`?

 `A:` You have to read the buffer and watch for `"RING"`. <span style="color: #ff6;">_Note: you have to strip the trailing `\n` at the end of the buffer._</span>

You should then send `"ATA"`. You are now connected.

<span style="color: #ff6;">_Assuming you have the previous template as a starting point..._</span>
```
115 REM If Buffer empty, go back to 110
120 IF EOF(1) < 0 THEN GOTO 110
125 REM Store Buffer in BUF Variable
130 INPUT# 1, BUF
135 REM If theres a "RING" in BUF we got a call. GoTo Line 160
140 IF LEFT$(BUF, 4) = "RING" THEN GOTO 160
145 REM Otherwise go back to 110
150 GOTO 110
155 REM Send ATA and initiate a connection
160 PRINT# 1, "ATA"
170 REM You are now connected, put Program Logic here
```
##

### `Q:` How do I read input and disconnect if the user is idle for more than `n` seconds?

 `A:` We have the timeout value set in the `TMO` variable. The `CT` variable will hold our current timer value.

<span style="color: #ff6;">_Assuming you have the template & the incoming call parts above..._</span>
```
195 REM Show an Prompt
200 PRINT# 1, "Enter something:";
205 REM If theres crap in the Buffer, empty it
210 IF EOF(1) = 0 THEN INPUT# 1, DUMP$ : GOTO 210
215 REM If theres actual Input, store it in INP Variable
220 IF EOF(1) = 0 THEN INPUT# 1, INP$ : SLEEP 0.1 : GOTO 310
225 REM Strip the \n
230 INP$ = LEFT$(INP$, LEN(INP$)-1)
235 REM Check if CT > TMO. If True the timeout has been passed. Disconnect the user
240 IF CT > TMO THEN PRINT# 1, "INPUT TIMEOUT, BYE" : PRINT# 1, "MODEM HANGUP" : SLEEP 1 : PRINT# 1, "+++" : PRINT# 1, "ATH0" : GOTO 20
245 REM Increment the Current Timer (CT) by 0.1
250 CT = CT + 0.1
255 REM Sleep a little bit...
260 SLEEP 0.1
270 GOTO 220
295 REM Strip the \n
300 INP$ = LEFT$(INP$, LEN(INP$)-1)
305 REM Reset the Current Timer (CT)
310 CT = 0
315 REM The entered User Value is now in INP
```
##
