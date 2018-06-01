
# COMMAND LINE EXERCISES WITH BASH
<hr>

### I. Math with Bash

**I.01)** Define two variables, var1=88 and var2=71. Print out (var1+var2), (var1*var2), (var1/var2), (var1%var2).<br>
(Hint: try echoing `$((var1+var2))`      )


```bash

```

**I.02)** Add 2 to var2 and echo var2.


```bash

```

**I.03)** Define two variables, var1=88.3 and var2=71. Print out var1+var2. What happened?


```bash

```

**I.04)** An easy way to do floating point arithmetic in bash is to use `bc` command. Explore the use of `bc` and calculate var1+var2 if var1=88.3 and var2=73. Investigate the use of `bc` on the web or man/help pages.


```bash

```

### II. File Manipulation and Finding Things

**II.01)** List the files with .so extension in "/lib64" folder to the libraries.txt file. Then, print out only the unique file names prior to ".so" to a file called "unique_libs.txt".


```bash

```

**II.02)** Split the unique_libs.txt to 4 files with more or less the same number of lines. The names of these split files should look like "splitlib_00", "splitlib_01", ... <br>
(Hint: Explore the use of `split` command but be careful to not to split an individual line between two files.)


```bash

```

**II.03)** Copy the file "splitlib_01" to "splitlib_01_1" but omit the first three lines of "splitlib_01". <br>
(Hint: You can do this with `tail` command.)


```bash

```

**II.04)** Combine "splitlib_00", "splitlib_01_1", "splitlib_02" and "splitlib_03" to create "unique_libs_defected.txt". "unique_libs.txt" and "unique_libs_defected.txt" should be same except the missing 3 lines.


```bash

```

**II.05)** Identify the names of the missing library names in "unique_libs_defected.txt" and their line numbers in "unique_libs.txt".<br>
(Hint: Explore `diff` command)



```bash

```

**II.06)** Combine "splitlib_00" and "splitlib_01" into "pasted_libs.txt" which will include 2 columns: the library names from "splitlib_00" in the first column and library names from "splitlib_01" in the second column. The columns should be separated by comma. Do you have two columns in every line? <br>
(Hint: Explore `paste` command.)


```bash

```

**II.07)** Print out "splitlib_00" file in reverse order (i.e. bottom to top). <br>
(Hint: You can use `cat` command to print a file from top to bottom to the screen. What command could do the reverse?)


```bash

```

**II.08)** List everything in your current working directory according to their modifictation time.


```bash

```

**II.09)** List only the files in your current directory and any directories within with respect to their sizes. <br>
(Hint: By combining `find` and `xargs` commands you can do this easily. Explore how to use  `xargs` command.)


```bash

```

**II.10)** Make four new folders ("slib_00", "slib_01", ...) and move "splitlib_00" to "slib_00" folder, move "splitlib_01" to "slib_01" folder, and so on.


```bash

```

**II.11)** Combining `find`, `xargs` and `grep` commands search for 'python' string in files with sizes greater than 1 kilobytes in the current working folder and all the folders within.


```bash

```

**II.12)** Find all the files in "/lib64" folder which are larger than 4 Megabytes and show their sizes. Do not let `find` to search files at deeper levels in "/lib64" folder hierarchy.


```bash

```

### III. Loop Exercises

**III.01)** Write a loop command to print out integers 1 to 20 (increasing order) to the screen where each number should be printed out on a separate line.


```bash

```

**III.02)** Write a loop command to print out integers 20 to 1 in (decreasing order) to the screen where each number should be printed out on a separate line.


```bash

```

**III.03)** In addition to `for`, loops can be created with `while` statement in bash scripts. Using `while` loop  repeat the last twp exercises i.e.:
- Write a loop command to print out integers 1 to 20 (increasing order) to the screen where each number should be printed out on a separate line.
- Write a loop command to print out integers 20 to 1 in (decreasing order) to the screen where each number should be printed out on a separate line.<br>
(Hint: When using  `while`, the loop continues until some condition is false. The argument of the condition should change during the loop operation. Otherwise you would end up with an infinite loop. Explore `while` loops on the web for further details.)


```bash

```

**III.04)** Write a loop command to print out integers 20 to 1 in (decreasing order) to the screen where all the numbers printed on the same line separated with a space.


```bash

```

**III.05)** Write a loop command to print out integers 1 to 20 (increasing order) to a file (called "integers.txt") where each number should be printed out on a separate line.


```bash

```

**III.06)** Write a command including a loop to add 1 to each integer in "integers.txt" file and write it to "plusone.txt". Assume you don't know the number of lines in "integer.txt".


```bash

```

**III.07)** Do the same as operation in the last question  but this time use sed function witin the loop to access each line in "integers.txt". Search for sed function on the web or read `man sed` or `sed --help` for its use. Again, assume you don't know the number of lines in "integer.txt".


```bash

```

**III.08)** Write a loop to create 100 folders with names "1","2","3",...,"100". Echo which folder is created each step. Use `seq` function to identify the values over which the loop iterates. Search for `seq` function on the web or read `man seq` or `seq --help`.


```bash

```

**III.09)** Delete the 100 folders using a similar loop as the last question.


```bash

```

**III.10)** Write a loop to create 100 folders with names "001", "002",...,"100". Echo which folder is created each step. Again, use `seq` function to identify the values over which the loop iterates. Search for `seq` function  on the web or read `man seq` or `seq --help`. <br>
(Hint: Read flags of `seq` function.)


```bash

```

**III.11)** Delete the 100 folders using created in the last question.


```bash

```

**III.12)** Write a loop to create 10 folders with names "1", "2",...,"10" but after a folder is created make the code to wait for 3 seconds before creating another folder. Echo which folder is created each step.


```bash

```

### IV. VIM Text Editor Exercises

**IV.01)** Print your name the one million times (each on one line) along with the line number to the file "ilikemyname.txt". Use VIM text editor to open "ilikemyname.txt" and delete 783219th line.


```bash

```

**IV.02)** While you are viewing ilikemyname.txt with VIM, set VIM to show line numbers.


```bash

```

**IV.03)** Undo your deletion.


```bash

```

**IV.04)** Only erase the number after your name on line 783219.


```bash

```

**IV.05)** While viewing ilikemyname.txt with VIM editor, go to the last line and enter the text "Last" before your name. Then go to the first line of the file and enter the text "First" after your name.


```bash

```

**IV.06)** Save the file, then save the file as "ilikemayname_bckp.txt" and quit to command line.


```bash

```

**IV.07)** Open "ilikemyname.txt" and "ilikemayname_bckp.txt" both in a single VIM window side-by-side. Delete the first 134000 lines in "ilikemyname.txt". Delete your name in all lines of "ilikemayname_bckp.txt"


```bash

```

**IV.08)** You can work with VIM without opening the editor window. This is called batch mode. Copy ilikemyname.txt" to "ilikemayname_bckp.txt". Now both files have your name. Delete your name in all lines of "ilikemayname_bckp.txt" and save the file with VIM without opening editor window.
(Hint: Explore `vim -c ...` i.e. -c flag)


```bash

```

### V. Writing Scripts

**V.01)** Write a script to find if a file exists in "/lib64". Input the filename as a parameter and if the file is in the folder, the script should print out "yourfilename file exists". Otherwise the script should print out "yourfilename file does not exits"


```bash

```

**V.02)** Write a bash script which outputs:<br>
 - "True" when you run it with 1 as the parameter (i.e. bash yourscript.sh 1) <br>
 - "False" when you run it with 0 as the parameter (i.e. bash yourscript.sh 0) <br>
 - "Enter 0 or 1" when you run it with any other integer (i.e. bash yourscript.sh 4) <br>
(Hint: Explore the use of conditionals if, elif, else in bash)


```bash

```

**V.03)** Write a bash script to generate 1000 random numbers between 1 and 1000 and write them to a file. Find out how many unique numbers are obtained. <br>
(Hint: Try issuing `echo $RANDOM`, what do you get?)


```bash

```

**V.04)** Write a script to run the script you have developed for unique random numbers n times. n is a variable parameter you will set as an input when you are starting your script.


```bash

```
