
# COMMAND LINE EXERCISES WITH BASH
<hr>

### I. Math with Bash

**I.01)** Define two variables, var1=88 and var2=71. Print out (var1+var2), (var1*var2), (var1/var2), (var1%var2).<br>
(Hint: try echoing \``$((var1+var2))`\`      )


```bash
var1=88;var2=71;echo $((var1+var2))
var1=88;var2=71;echo $((var1*var2))
var1=88;var2=71;echo $((var1/var2))
var1=88;var2=71;echo $((var1%var2))
```

**I.02)** Add 2 to var2 and echo var2.


```bash
let var2+=2; echo $var2
```

**I.03)** Define two variables, var1=88.3 and var2=71. Print out var1+var2. What happened?


```bash
var1=88.3;var2=71;echo $((var1+var2))
-bash: 88.3: syntax error: invalid arithmetic operator (error token is ".3")
```

**I.04)** An easy way to do floating point arithmetic in bash is to use \``bc`\` command. Explore the use of \``bc`\` and calculate var1+var2 if var1=88.3 and var2=73. Investigate the use of \``bc`\` on the web or man/help pages.


```bash
echo "$var1+$var2" | bc
```

### II. File Manipulation and Finding Things

**II.01)** List the files with .so extension in "/lib64" folder to the libraries.txt file. Then, print out only the unique file names prior to ".so" to a file called "unique_libs.txt".


```bash
ls /lib64 | grep -F .so > libraries.txt
cut -d. -f 1 libraries.txt | sort | uniq > unique_libs.txt
```

**II.02)** Split the unique_libs.txt to 4 files with more or less the same number of lines. The names of these split files should look like "splitlib_00", "splitlib_01", ... <br>
(Hint: Explore the use of \``split`\` command but be careful to not to split an individual line between two files.)


```bash
split -d --number=l/4 unique_libs.txt splitlib_
```

**II.03)** Copy the file "splitlib_01" to "splitlib_01_1" but omit the first three lines of "splitlib_01". <br>
(Hint: You can do this with \``tail`\` command.)


```bash
tail -n +4 splitlib_01 > splitlib_01_1
```

**II.04)** Combine "splitlib_00", "splitlib_01_1", "splitlib_02" and "splitlib_03" to create "unique_libs_defected.txt". "unique_libs.txt" and "unique_libs_defected.txt" should be same except the missing 3 lines.


```bash
cat splitlib_00 splitlib_01_1 splitlib_02 splitlib_03 > unique_libs_defected.txt
#or
cat splitlib_0* > unique_libs_defected.txt
```

**II.05)** Identify the names of the missing library names in "unique_libs_defected.txt" and their line numbers in "unique_libs.txt".<br>
(Hint: Explore \``diff`\` command)



```bash
diff unique_libs.txt unique_libs_defected.txt
```

**II.06)** Combine "splitlib_00" and "splitlib_01" into "pasted_libs.txt" which will include 2 columns: the library names from "splitlib_00" in the first column and library names from "splitlib_01" in the second column. The columns should be separated by comma. Do you have two columns in every line? <br>
(Hint: Explore \``paste`\` command.)


```bash
paste -d, splitlib_00 splitlib_01 > pasted_libs.txt
```

**II.07)** Print out "splitlib_00" file in reverse order (i.e. bottom to top). <br>
(Hint: You can use \``cat`\` command to print a file from top to bottom to the screen. What command could do the reverse?)


```bash
tac splitlib_00
```

**II.08)** List everything in your current working directory according to their modifictation time.


```bash
ls -t
```

**II.09)** List only the files in your current directory and any directories within with respect to their sizes. <br>
(Hint: By combining \``find`\` and \``xargs`\` commands you can do this easily. Explore how to use  \``xargs`\` command.)


```bash
find . -type f | xargs ls -lS
```

**II.10)** Make four new folders ("slib_00", "slib_01", ...) and move "splitlib_00" to "slib_00" folder, move "splitlib_01" to "slib_01" folder, and so on.


```bash
echo slib_00 slib_01 slib_02 slib_03 | xargs mkdir

#or

for i in 00 01 02 03; do mv splitlib_$i ./slib_$i; done
```

**II.11)** Combining \``find`\`, \``xargs`\` and \``grep`\` commands search for 'python' string in files with sizes greater than 1 kilobytes in the current working folder and all the folders within.


```bash
find . -size +1k -type f | xargs grep 'python'
```

**II.11)** Find all the files in "/lib64" folder which are larger than 4 Megabytes and show their sizes.  Do not let find to search files at deeper levels in "/lib64" folder hierarchy.


```bash
find /lib64/ -maxdepth 1 -size +2M -type f -ls
```

### III. Loop Exercises

**III.01)** Write a loop command to print out integers 1 to 20 (increasing order) to the screen where each number should be printed out on a separate line.


```bash
for ((i=1;i<=20;i+=1)); do echo $i; done

#or

for i in `seq 20`; do  echo $i; done
```

**III.02)** Write a loop command to print out integers 20 to 1 in (decreasing order) to the screen where each number should be printed out on a separate line.


```bash
for ((i=20;i>0;i-=1)); do echo $i; done
```

**III.03)** In addition to \``for`\`, loops can be created with \``while`\` statement in bash scripts. Using \``while`\` loop  repeat the last twp exercises i.e.:
- Write a loop command to print out integers 1 to 20 (increasing order) to the screen where each number should be printed out on a separate line.
- Write a loop command to print out integers 20 to 1 in (decreasing order) to the screen where each number should be printed out on a separate line.<br>
(Hint: When using  \``while`\`, the loop continues until some condition is false. The argument of the condition should change during the loop operation. Otherwise you would end up with an infinite loop. Explore \``while`\` loops on the web for further details.)


```bash
i=1; while [ $i -lt 21 ]; do echo $i; i=$((i+1)); done
```


```bash
i=20; while [ $i -gt 0 ]; do echo $i; i=$((i-1)); done
```

**III.04)** Write a loop command to print out integers 20 to 1 in (decreasing order) to the screen where all the numbers printed on the same line separated with a space.


```bash
for ((i=20;i>0;i-=1)); do echo -n "$i "; done; echo " "
```

**III.05)** Write a loop command to print out integers 1 to 20 (increasing order) to a file (called "integers.txt") where each number should be printed out on a separate line.


```bash
rm integers.txt; touch integers.txt; for ((i=1;i<=20;i+=1)); do echo $i>> integers.txt; done
```

**III.06)** Write a command including a loop to add 1 to each integer in "integers.txt" file and write it to "plusone.txt". Assume you don't know the number of lines in "integer.txt".


```bash
rm plusone.txt 
i=`cat integers.txt | wc -l` 
touch plusone.txt 
for j in `seq $i`; do l=`head -n $j integers.txt | tail -1`; echo $((l+1))>>plusone.txt; done
```

**III.07)** Do the same as operation in the last question  but this time use sed function witin the loop to access each line in "integers.txt". Search for sed function on the web or read \``man sed`\` or \``sed --help`\` for its use. Again, assume you don't know the number of lines in "integer.txt".


```bash
rm plusone.txt 
i=`cat integers.txt | wc -l`
touch plusone.txt
for j in `seq $i`; do l=`sed -n "$j"p integers.txt`; echo $((l+1))>>plusone.txt; done
```

**III.08)** Write a loop to create 100 folders with names "1","2","3",...,"100". Echo which folder is created each step. Use \``seq`\` function to identify the values over which the loop iterates. Search for \``seq`\` function on the web or read \``man seq`\` or \``seq --help`\`.


```bash
for i in `seq 100`; do mkdir $i; echo $i; done
```

**III.09)** Delete the 100 folders using a similar loop as the last question.


```bash
for i in `seq 100`; do rm -Rf $i; done
```

**III.10)** Write a loop to create 100 folders with names "001", "002",...,"100". Echo which folder is created each step. Again, use \``seq`\` function to identify the values over which the loop iterates. Search for \``seq`\` function  on the web or read \``man seq`\` or \``seq --help`\`. <br>
(Hint: Read flags of \``seq`\` function.)


```bash
for i in `seq -w 100`; do mkdir $i; done
```

**III.11)** Delete the 100 folders using created in the last question.


```bash
for i in `seq -w 100`; do rm -Rf $i; done
```

**III.12)** Write a loop to create 10 folders with names "1", "2",...,"10" but after a folder is created make the code to wait for 3 seconds before creating another folder. Echo which folder is created each step.


```bash
for i in `seq 10`; do mkdir $i; echo $i; sleep 3; done
```

### IV. VIM Text Editor Exercises

**IV.01)** Print your name the one million times (each on one line) along with the line number to the file "ilikemyname.txt". Use VIM text editor to open "ilikemyname.txt" and delete the line 783219th line.


```bash
rm ilikemyname.txt
touch ilikemyname.txt 
for i in `seq 1000000`; do echo "Alper Kinaci" $i >> ilikemyname.txt; done
vim ilikemyname.txt

-- Go to the command-line mode (hit "esc" then ":"), two alternatives after that: 
1- write 783219 and hit enter/return, 
2- write ?783219 and hit enter/return. Hit d two times

```

**IV.02)** While you are viewing ilikemyname.txt with VIM, set VIM to show line numbers.


```bash
-- Go to the command-line mode (hit "esc" then ":") and write set nu, hit enter/return
```

**IV.03)** Undo your deletion.


```bash
-- Hit "esc" to go to the normal mode and hit "u"
```

**IV.04)** Only erase the number after your name on line 783219.


```bash
-- Again you have many options here:

1- Hit "esc" to switch to the normal mode, move the cursor to the beginning of the number and 
hit "x" 6 times to erase the number on that line on character at a time

OR

2- Hit "esc" and "6" and then "x" to erase 6 characters. There are several more ways.
```

**IV.05)** While viewing ilikemyname.txt with VIM editor, go to the last line and enter the text "Last" before your name. Then go to the first line of the file and enter the text "First" after your name.


```bash
-- Follow the steps below

1- Hit "esc" and ":" to go to the command-line mode
2- Write "$", hit enter/return
3- Hit "i" to enter insert mode and type "Last" before your name
4- Hit "esc" and ":" to go to the command-line mode
5- Write "0", hit enter/return
6- Hit "i" to enter insert mode, move the cursor after your name and type "First"
```

**IV.06)** Save the file, then save the file as "ilikemayname_bckp.txt" and quit to command line.


```bash
-- Follow the steps below:

1- Hit "esc" and ":" to go to the command-line mode
2- Write "w", hit enter/return. The file is saved
3- Hit "esc" and ":" to go to the command-line mode
4- Write "w ilikemayname_bckp.txt", hit enter/return. You created ilikemayname_bckp.txt
5- Hit "esc" and ":" to go to the command-line mode
6- Write "wq", hit enter/return to save and quit
```

**IV.07)** Open "ilikemyname.txt" and "ilikemayname_bckp.txt" both in a single VIM window side-by-side. Delete the first 134000 lines in "ilikemyname.txt". Delete your name in all lines of "ilikemayname_bckp.txt"


```bash
vim -O ilikemyname.txt ilikemayname_bckp.txt

-- The command above will open 2 files in one VIM editor window. Now, follow the step below:

1- Make sure the cursor is on ilikemyname.txt tab
2- Hit "esc" to go to normal mode
3- Write 134000 and hit "d" 2 times. 134K lines deleted
4- To move the cursor to ilikemayname_bckp.txt tab hit "esc" (normal mode) and do "Ctrl+w" and hit "w" again.
5- Hit "esc" and ":" to go to the command-line mode
6- Write %s/Your Name//g, hit enter/return. All your names are deleted from ilikemayname_bckp.txt tab
7- Hit "esc" and ":" to go to the command-line mode
8- Write "wq", hit enter/return to save and quit rom ilikemayname_bckp.txt tab
9- Hit "esc" and ":" to go to the command-line mode
10- Write "wq", hit enter/return to save and quit

```

**IV.08)** You can work with VIM without opening the editor window. This is called batch mode. Copy ilikemyname.txt" to "ilikemayname_bckp.txt". Now both files have your name. Delete your name in all lines of "ilikemayname_bckp.txt" and save the file with VIM without opening editor window.
(Hint: Explore `vim -c ...` i.e. -c flag)


```bash
cp ilikemyname.txt ilikemayname_bckp.txt
vim -c ":%s/Your Name//g" -c ":wq" ilikemayname_bckp.txt
```

### V. Writing Scripts

**V.01)** Write a script to find if a file exists in "/lib64". Input the filename as a parameter and if the file is in the folder, the script should print out "yourfilename file exists". Otherwise the script should print out "yourfilename file does not exits"


```bash
#!/usr/bin/env bash

filename=$1

if [ -f /lib64/$filename ]; then
    echo "$filename"  'file exits'
else
    echo  "$filename"  'file does not exist'
```

**V.02)** Write a bash script which outputs:<br>
 - "True" when you run it with 1 as the parameter (i.e. bash yourscript.sh 1) <br>
 - "False" when you run it with 0 as the parameter (i.e. bash yourscript.sh 0) <br>
 - "Enter 0 or 1" when you run it with any other integer (i.e. bash yourscript.sh 4) <br>
(Hint: Explore the use of conditionals if, elif, else in bash)


```bash
#!/usr/bin/env bash

myflag="$1"

if [ $myflag -eq 1 ]; then
    echo 'True'
elif [ $myflag -eq 0 ]; then
    echo 'False'
else
    echo 'Enter 0 or 1'
fi
```

**V.03)** Write a bash script to generate 1000 random numbers between 1 and 1000 and write them to a file. Find out how many unique numbers are obtained. <br>
(Hint: Try issuing \``echo $RANDOM`\`, what do you get?)


```bash
#!/usr/bin/env bash

rm randomnumbers.txt
touch randomnumbers.txt

for i in `seq 1000`
    do
        echo $(((RANDOM%1000)+1)) >> randomnumbers.txt
    done

sort -n randomnumbers.txt | uniq | wc -l
```

**V.04)** Write a script to run the script you have developed for unique random numbers n times. n is a variable parameter you will set as an input when you are starting your script.


```bash
#!/usr/bin/env bash

for j in `seq $1`; do
    rm randomnumbers.txt
    touch randomnumbers.txt

    for i in `seq 1000`; do
        echo $(((RANDOM%1000)+1)) >> randomnumbers.txt
    done

    sort -n randomnumbers.txt | uniq | wc -l
done
```
