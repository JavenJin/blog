---
title: Windows batch scripts(.bat)
description: Windows批处理脚本（.bat）
date: '2022-05-17'
categories:
    - Tools
tags:
    - Tools
---

# Windows batch scripts(.bat)

## Common file manipulation DOS commands

- dir (List file names)
- cd (Change current directory)
- ren (Change the file name)
- copy (Copy a file)
- del (Delete a file)
- md (Create subdirectory)
- rd (Deletes a directory)
- deltree (Deletes a directory tree)
- format (format the disk)
- edit (Text editor)
- type (Show file contents)
- mem (View memory status)
- help (Show help tips)
- cls (clear screen)
- move (Move files, change directory names)
- more (split screen display)
- xcopy (copies directories and files)
- echo (Show input)
- echo on (Turns on the command echo)
- echo off (Turn off the command display)
- @ (@ commands with @ are not displayed)
- pause (suspends the program, press any key to continue)
- \> (Output the displayed content to somewhere)
- \>\> (Append the display to somewhere)
- \>nul (command followed by \>nul means output to empty device)
- mode (Sets the window size: mode con cols=32 lines=8)
- color (Set the background color: color 3a (background (dark indigo) and text (bright green)))
- title (change the title name of the current command prompt)
- rem (comment (belongs to the command will be displayed))
- :: (comment (will not be shown))
- prompt (change the current path to the root path and rename it)
- goto (command followed by a label to jump)
- : (Write the tag name after the command (not case sensitive), special tags :EOF or :eof do not need to be defined)
- call (call batch or label)
- start (starts the application)

## Variables

| Command                         | Explanation                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| set var=1                       | Define the variable var and copy 1 to a                                      |
| set var                         | View the value of the variable var                                              |
| set v                           | View the values of all variables starting with v                                        |
| set                             | View the values of all variables                                             |
| %var%                           | Value (content) of var variable                                          |
| set /a var=48                   | Assign the number 48 to the variable var, a 32-bit integer value, occupying 4 bytes           |
| set /p var                      | The user manually enters a value for var                                          |
| set /p var=Please enter some text       | The user manually enters the value for var and displays the prompt text: "Please enter some text"        |
| set var=Hello world!            |                                                              |
| echo %var:o=z%                  | Output Hello world! without changing the var value                                  |
| set var2=%var:ld=ms and bugs%   | Assign Hello worms and bugs! to var2 without changing the var value                 |
| %var:~m%                        | A positive number m means that the variable var is taken from the left side after the mth character. A negative number m means that the variable var is taken from the right side after the -mth character and all characters to the right of it. |
| %var:~m,n%                      | Starting from m, n characters are taken for positive numbers, and n characters are taken for negative numbers until -n characters are left         |
| set /a num=48                   | Assign the value 48 to the variable num                                        |
| set /a result=%num%+12          | The result of adding the variables num and 12 is assigned to the variable result                          |
| echo %result%                   | Display the value of the variable result                                           |
| setlocal EnableDelayedExpansion | Delayed variable expansion makes sense of !var!                                    |

## Passing parameters

Use % to receive arguments Pass arguments directly after call or start or when running a batch file in cmd

```bat
Receiving parameters:
echo The 1st parameter you entered is %1
echo The 2nd parameter you entered is %2

Transfer parameters:
call Called.bat hello world!
start Called.bat hello world!
./Called.bat hello world!
```

## Condition IF

| Symbols | Meaning |
| ---- | -------- |
| EQU | equal |
| NEQ | unequal |
| LSS | less than |
| LEQ | less than or equal to |
| GTR | Greater than |
| GEQ | greater than or equal to |
| NOT | NOT |

- if exist	(Determine if a file exists)
- if defined	(Determine if environment variables are defined)

## Loop FOR

General format of for loop usage: for %i in (\*.\*) do @echo %i

```bat
:::::::Batch file name modification.bat:::::::
@echo off
setlocal EnableDelayedExpansion
set /a num=1
for %%i in (D:\test\*.txt) do (
ren "%%i" !num!.txt
set /a num+=1
)
::::::::::::::::::::::::::::::::::::::::::::::
```

The for loop uses the general format of a numeric loop: for /l %i in (5,3,16) do echo %i

The numeric variable i becomes, in order: 5, 8, 11, 14, starting from 5 and increasing by 3 until 16.

```bat
::::::::::Circle Square.bat::::::::::
@echo off
setlocal EnableDelayedExpansion

set var=○
for /l %%i in (1,1,7) do set var=%var%!var!
:: At this point the variable var has become a row of 8 consecutive circles

for /l %%i in (1,1,8) do (
echo This is the first %%i copies> output-results-%%i.txt
for /l %%j in (1,1,8) do echo %var%>>output-results-%%i.txt
)

echo The 8 X 8 ○ matrix has been drawn and saved in 8 text files
pause
::::::::::::::::::::::::::::::::s:::::
```

## Combination commands

1. &

   ```bat
   echo Checking what executable files we have in WINDOWS... & dir C:\WINDOWS\*.exe & echo And we got lots of stuff here.
   ```

   & acts as a link between multiple commands.

   Regardless of the result of each of the three commands, the later one will always be executed.

2. &&

   Similar to &, multiple commands are juxtaposed and executed in order.

   If there is an error in the execution of one of the multiple commands, the subsequent commands will not be executed; if there has been no error, all the concurrent commands will be executed all the time.

3. ||

   || has the opposite purpose of &&.

   When the correct command is encountered, no further commands will be executed.

   If no correct command is encountered, all commands will be executed.

## Pipeline commands

1. \> and \>\>

   Enter the redirect command. Redirects a command or the output of a program to a specific file.

   \> will erase the content of the original file and write it to the specified file, while \>\> will only append the content to the specified file.

2. |

   It can put the output of the command on its left into the command on its right as an argument.

3. The pipeline command also has \<, \<& and \>&, which are not common and will not be discussed for now.

## Learning Address

[Windows Batch Scripting Tutorial](http://docs.30c.org/dosbat/index.html)