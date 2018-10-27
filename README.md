TinyBasic Plus
==============

# Full list of supported statements and functions

## System
- BYE		- *exits Basic, soft reboot on Arduino*
- END 		- *stops execution from the program, also "STOP"*
- MEM		- *displays memory usage statistics*
- NEW		- *clears the current program*
- RUN		- *executes the current program*
- LIST		- *print out the current program*

## File IO/SD Card
- FILES		- 	*lists the files on the SD card*
- LOAD filename.bas	- *loads a file from the SD card*
- CHAIN filename.bas - *equivalent of: new, load filename.bas, run*
- SAVE filename.bas	- *saves the current program to the SD card, overwriting*

## IO, Documentation
- INPUT variable	- *let the user input an expression (number or variable name)*
- PRINT expression	- *print out the expression, also "?"*
- REM stuff		- *remark/comment, also "'"*

## Expressions, Math
- A=V, LET A=V	- *assign value to a variable*
- +, -, \*, / - *Math*
- <,<=,=,<>,!=,>=,> - *Comparisons*
- ABS( expression )  - *returns the absolute value of the expression*
- RSEED( v ) - *sets the random seed to v*
- RND( m ) - *returns a random number from 0 to m-1*

## Control
- IF expression statement - *perform statement if expression is true*
- FOR variable = start TO end	- *start for block*
- FOR variable = start TO end STEP value - *start for block with step*
- NEXT - *end of for block*
- GOTO linenumber - *continue execution at this line number*
- GOSUB linenumber - *call a subroutine at this line number*
- RETURN	- *return from a subroutine*

## Pin IO 
- DELAY	timems*- wait (in milliseconds)*
- DWRITE pin,value - *set pin with a value (HIGH,HI,LOW,LO)*
- AWRITE pin,value - *set pin with analog value (pwm) 0..255*
- DREAD( pin ) - *get the value of the pin* 
- AREAD( analogPin ) - *get the value of the analog pin*

## Sound - Piezo wired with red/+ on pin 5 and black/- to ground
- TONE freq,timems - play "freq" for "timems" milleseconds (1000 = 1 second)
- TONEW freq,timems - same as above, but also waits for it to finish
- NOTONE - stop playback of all playing tones

# Example programs

Here are a few example programs to get you started...

## User Input

Let a user enter a new value for a variable, enter a number like '33' or '42',
or a varaible like 'b'.

	10 A=0
	15 B=999
	20 PRINT "A is ", A
	30 PRINT "Enter a new value ";
	40 INPUT A
	50 PRINT "A is now ", A

## Blink

hook up an LED between pin 3 and ground

	10 FOR A=0 TO 10
	20 DWRITE 3, HIGH
	30 DELAY 250
	40 DWRITE 3, LOW
	50 DELAY 250
	60 NEXT A

## Fade

hook up an LED between pin 3 and ground

	10 FOR A=0 TO 10
	20 FOR B=0 TO 255
	30 AWRITE 3, B
	40 DELAY 10
	50 NEXT B
	60 FOR B=255 TO 0 STEP -1
	70 AWRITE 3, B
	80 DELAY 10
	90 NEXT B
	100 NEXT A

## LED KNOB

hook up a potentiometeter between analog 2 and ground, led from digital 3 and ground.  If knob is at 0, it stops

	10 A = AREAD( 2 )
	20 PRINT A
	30 B = A / 4
	40 AWRITE 3, B
	50 IF A == 0 GOTO 100
	60 GOTO 10
	100 PRINT "Done."

# Known Quirks and Limitations
- If LOAD or SAVE are called, FILES fails subsequent listings
- SD cards are not hot-swappable. A reset is required between swaps.
