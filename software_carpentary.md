# PIPES and FILTERS
<hr>


### I. Wildcards

Let's look at what is inside molecules folder and enter into it.

```bash
ls molecules
cd molecules
```

We see *Protein Data Bank* (.pdb) files for several molecules. We want to obtain more 
information about these files. `wc` (word count) command will give 
information about how many lines, words and characters are there
in files. 

```bash
wc cubane.pdb
```

If you only need information about how many lines are there in a file,
you can use a flag with `wc`

```bash
wc -l cubane.pdb
wc --help
```

Instead of issuing the command for each file one by one, or
using a loop to go though each file we can use **wildcards**. 

```bash
wc *.pdb
```


Think `*` wildcard as an internal loop running over everything and picking the 
files which have matching strings in their name.

Another wildcard you can use is `?`. In contrast to `*` wildcard `?` matches only 
one character

```bash
wc p?tane.pdb
wc p??tane.pdb
wc p*tane.pbd
```

Let's move to folder *north-pacific-gyre/2012-07-03*

```bash
cd ../north-pacific-gyre/2012-07-03
ls -al
```

There are files ending with A, B and Z and we want to select the ones
ending with A or B

```bash
cd ../north-pacific-gyre/2012-07-03
ls -al
ls *[AB].txt
ls *[ABZ].txt
```

The square brackets gives us the *or* option.

### II. Sorting and Redirecting
Let's gather information about the number of lines in all files in this folder and 
store the data

```bash
pwd
wc -l *.pdb
wc -l *.pdb > lengths.txt
```

Did we create a file?

```bash
ls lengths.txt
ls --help
ls -al lenghts.txt
```

What is is the "lengths.txt" file? We can use `cat` (concatenate) command to
print the contents of the file. `cat` prints out all the file to screen but
if we want to see the data page by page, we can use `less`. You can move screen
by screen with spacebar, or go back by `b` and quit by `q`

```bash
cat lengths.txt
less lengths.txt
```

How an `wc` works differently with file input and redirecting 

```bash
wc -l lengths.txt
wc -l < lengths.txt

wc -l #hit enter#
a #hit enter#
b #hit enter#
c #hit enter#
d #hit enter#
e #hit enter#
#hit Ctrl+D#
```

One other type of redirecting is appending with `>>`

```bash
wc -l *.pdb >> lengths.txt
```

We want to see the which molecule file has the most lines.
We can use `sort` command.

```bash
sort -n lengths.txt
```

Let's redirect the result to another file and look at the shortest and
longest files. 

```bash
sort -n lengths.txt > sorted-lenghts.txt
head -n 1 sorted-lenghts.txt
tail -n 1 sorted-lenghts.txt
```

Redirecting a file to the same file is a bad practice, don't do
`sort -n lengths.txt > lenghts.txt`

We can reverse the order of `sort` or the column that the sorting
is done.

```bash
sort -n -r lengths.txt
sort -k 2 sorted-lenghts.txt
```

In sort `-n` identifies numeric sorting. If not set, the 
default is to sort alphabetical.

### III. Pipes

We have used `wc`, `head`, `sort` commands step by step to accomplish tasks.
There is another approach called **Pipes** with which we can execute our 
tasks in one step.

```bash
sort -n lengths.txt | head -n 1
sort -n -r lengths.txt | tail -n 1
```

The vertical bar `|` between to commands is called a **pipe**. It takes the 
output from the command on the left and feeds as input to the command on the
right. 

```bash
sort -n lengths.txt | head -n 3 | tail -n 1
wc -l *.pdb | sort -n | head -n 3 | tail -n 1
```

As you see, we can create a pipeline by stacking many pipes one after 
another. Each time the data is filtered and modified in some manner.

Now we will look at 2 other useful command we can use when filtering data.
These are `uniq` and `cut`

```bash
cp ../data/salmon.txt ./
cat salmon.txt
uniq salmon.txt; cat salmon.txt | uniq ; uniq<salmon.txt
sort salmon.txt | uniq
```

`uniq` removes duplicate lines only if they are adjacent. Combining with `sort`
you can eliminate all duplicates.

```bash
cp ../data/animals.txt ./
cut -d , -f 2 animals | sort | uniq
```

For `cut` the flags `-d` and `-f` indicate the delimiter and field

# CONDITIONAL STATEMENTS

The basic conditional statement is `if`. Apart from syntax differences, the
usage of the conditional construct is same as other languages.

```bash
myfavnumber=34

if [ $myfavnumber -eq 34 ];then echo "My favorite number is $myfavnumber";fi
```

`if/then` statement can be extended to `if/then/else` or `if/then/elif/else`
to test more conditions. Let's move to *data* folder.

```bash
cd data

nrabbits=`cat animals.txt | grep rabbit | wc -l`
# nrabbits=$(cat animals.txt | grep rabbit | wc -l)

if [ $nrabbits -le 2 ]; then
    echo 'Less than 3 rabbits'
elif [ $nrabbits -gt 2 ] && [ $nrabbits -le 10 ]  ; then
    echo '3 to 10 rabbits'
else
    echo 'More than 10 rabbits'
fi

echo "$nrabbits"
```


# LOOPS

Loops will make your life very easy for repetitive tasks and automation. 
Let's move to 'creatures' folder. We will work with the two files but let's 
first create backup copies.

```bash
cd ../creautures
pwd
ls -al
cp *.dat original-*.dat
```

When `cp` receives more than two inputs the last should be a directory for
`cp` to be able to copy all files prior to this directory. We can use 
a loop to accomplish this task

```bash
for filename in basilisk.dat unicorn.dat #hit enter#
> do
>     cp $filename original-$filename
> done

#OR

for filename in basilisk.dat unicorn.dat; do cp $filename original-$filename; done

#OR

for x in basilisk.dat unicorn.dat; do cp $x original-$x; done

for color in basilisk.dat unicorn.dat; do cp $color original-$color; done
```

`$` symbol tells the shell interpreter to treat *filename* as a **variable** and 
`$filename` returns the value of the variable which becomes *basilisk.dat* and
*unicorn.dat* within the loop. In some code, you may see `${filename}` which
is equivalent to `$filename`

```bash
echo *.dat

for filename in *.dat #hit enter#
> do
>     echo $filename
>     head -n 100 $filename | tail -n 5  #this selects the lines 96-100
> done
 ```

Say you have white spaces in your file names:

```bash
cp basilisk.dat 'green snake.dat'
cp unicorn.dat 'brown horse.dat'
for filename in green snake.dat brown horse.dat #hit enter#
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20  #this selects the lines 81-100 
> done

#This should be

for filename in 'green snake.dat' 'brown horse.dat' #hit enter#
> do
>     echo $filename
>     head -n 100 $filename | tail -n 20  #this selects the lines 81-100 
> done
 ```

Let's go back to our molecules folder do more looping

```bash
cd ../molecules
```

Say we want to write all molecules in one file:

```bash
for molecule in *.pdb; do echo $molecule; cat $molecule > all_molecules.dat; done
cat all_molecules.dat
```

We could not write all molecules in a single file because each iteration
of the loop we overwrite the previous file. Instead we should have used 
append `>>`

```bash
rm all_molecules.dat
for molecule in *.pdb; do echo $molecule; cat $molecule >> all_molecules.dat; done
```

What if we only want to write molecules if their names start with p

```bash
for molecule in p*; do echo $molecule; cat $molecule >> p_molecules.dat; done
```

What if we only want to write molecules if their names include c

```bash
for molecule in *c*; do echo $molecule; cat $molecule >> c_molecules.dat; done
```

We can construct nested loops for instance creating a grid of folders
for organizing our data

```bash
for temperature in 10 20 ; do 
> for molecule in propane pentane; do mkdir $molecule-$temperature; done
> done

#OR 

for temperature in 10 20 ; do 
> for molecule in propane pentane; do mkdir "$molecule-$temperature"; done
> done

#BUT NOT SAME

for temperature in 10 20 ; do 
> for molecule in propane pentane; do mkdir '$molecule-$temperature'; done
> done
```

There are other loop constructions such as `while` and `until`.

```bash
counter=0
while [ $counter -lt 10 ]; do echo $counter; let counter=counter+1; done
 ```

`while` iterates as long as the condition is true where as `until` stops
the loop when the condition is true
 
```bash
counter=0
until [ $counter -ge 10 ]; do echo $counter; let counter=counter-1; done
echo $counter
```

# FINDING THINGS

To find things in your system, the two commands that
you will most use are `grep` (global/regular expression/print) 
and `find`.

`grep` finds and prints lines in files that match a pattern. 

Let's move to 'writing' folder

```bash
cd ../writing
pwd
ls -al
```

What is in haiku.txt?

```bash
cat haiku.txt
```

Let's find lines that contain the word "not" and "The" :

```bash
grep not haiku.txt
grep The haikue.txt
```

When we searched for "The" two lines came up. In one the 
letters are actually included in "Thesis". To restrict our
search to the word "The" we could use `-w` flag. This flag
forces the pattern to match only whole words.

```bash
grep -w The haiku.txt
```

What is the line number of the line with matching the pattern? 
`-n` flag prints out the line number

```bash
grep -n -w The haiku.txt
grep -n The haiku.txt
```

How do we find all "The" and "the" together? `-i` makes the search
case-insensitive

```bash
grep -n -w the haiku.txt
grep -n -w -i The haiku.txt
```

How do we find all lines that do not contain "the" or
"The"? `-v` flag inverts the selection

```bash
grep -v -n -w -i The haiku.txt
``` 

There are other flags you can explore, just type:

```bash
grep --help
``` 

We could also search for patterns including spaces.

```bash
grep "is not" haiku.txt
```

We searched within files using `grep`. `find` command 
on the other searches for files. Let's see what `find`
finds in the current folder

```bash
find . # '.' means current directory
find ../ # '../' means one directoy above
```
`find`s output is the names of every file and directory 
under the current working directory. Using `-type d` and
`-type f` flag/argument couples we can determine directories
or files respectively 

```bash
find . -type d
find . -type f
```

`-name <pattern>` flag can be used to find files with
matching pattern in their name

```bash
find . -name *.txt
```

We expected it to find all the text files, but it 
only prints out "haiku.txt". The problem is that 
the shell expands wildcard characters like * before 
commands run. Since *.txt in the current directory 
expands to "haiku.txt", the command we actually ran was:

```bash
find . -name haiku.txt
```

To find all '.txt' files:

```bash
find . -name '*.txt'
```

Putting *.txt in single quotes to prevent the shell from 
expanding the * wildcard. This way, find actually gets 
the pattern *.txt, not the expanded filename haiku.txt

Can we find out the number of lines for all '.txt' files

```bash
wc -l $(find . -name '*.txt')

#OR

wc -l `find . -name '*.txt'`
```

Here the commands in '$()' and '``' are evaluated and 
then `wc -l` operates the output. We can further
`sort` the result

```bash
wc -l `find . -name '*.txt'` | sort -n
```

We can also use `find` and `grep` in sequence to search
for a pattern in certain files
 
```bash
grep 'FE' $(find .. -name '*.pdb')
```

# SHELL SCRIPTS

We were issuing the commands on the command line and
finding them again using the arrow key or `history` 
command.

When we need to accomplish many tasks, and repeat these
tasks form time to time, it is better to save your
commands to a file. Instead of executing the commands
one by one on the command line, we can execute the 
file. This file is called a shell script.

Let's go to molecules folder and start writing a 
script
 
```bash
cd ../molecules
vim middle.sh
```

When we start vim, to write characters we first hit
**i** (entering inset mode) and then we write the following

```bash
#!/usr/bin/env bash     # you may not need this line
head -n 15 octane.pdb | tail -n 5
```

Then we hit **Esc**, then we hit **:** (entering  command mode) 
and type **wq** (save and quit) and hit **Enter**.

```bash
bash middle.sh
```

Your input in the `head` command was octane.pdb.
Instead of hardcoding the file name in the script
we can make it a variable. Let's edit our script
with vim again

```bash
vim middle.sh
```

hit **i** (inset mode) and then we write the 
following

```bash
# head -n 15 octane.pdb | tail -n 5
head -n 15 "$1" | tail -n 5
```

A comment starts with a `#` character and runs to 
the end of the line. The computer ignores comments. 

In case the filename happens to contain any spaces, 
we surround $1 with double-quotes.

Then we hit **Esc**, then we hit **:** and type
**wq** and hit **Enter**. Now we can identify 
our file as an input to the script on the command line

```bash
bash middle.sh octane.pdb
bash middle.sh pentane.pdb
```

Let's make the number of lines printed by `head` and
`tail` also variables

```bash
vim middle.sh
```

hit **i** (inset mode) and then we write the 
following

```bash
# head -n 15 octane.pdb | tail -n 5
head -n "$2" "$1" | tail -n "$3"
```

Then we hit **Esc**, then we hit **:** and type
**wq** and hit **Enter**. Now let's change the 
number of lines on the command line.

```bash
bash middle.sh pentane.pdb 15 5
bash middle.sh pentane.pdb 20 5
```

It is a good coding practice to add comments 
in your script to explain what is being done
to another user of your script.

```bash
vim middle.sh
```

We will repeat the routine to insert save and
quit in vim.

```bash
# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
# head -n 15 octane.pdb | tail -n 5
head -n "$2" "$1" | tail -n "$3"
```

Comments are invaluable for helping people (including 
your future self) understand and use scripts. However 
each time you modify the script, you should check that 
the comment is still accurate.

Let's write another script to find the number of lines
for each file and sort them according to these
numbers. 

```bash
vim sorted.sh
```

Repeat the routine to insert save and
quit in vim.

```bash
wc -l "$1" "$2" | sort -n
```

Let's execute the script

```bash
bash sorted.sh *.pdb
```

As you see we did not get all the files. Only two files
reported because we entered two variables in the script.
If we want to enter any number of input arguments,
instead of using `"$1"`, `"$2"` etc., we could use 
`"$@"`

```bash
vim sorted.sh
```

Repeat the routine to insert save and
quit in vim.

```bash
wc -l "$@" | sort -n
```

Let's execute the script

```bash
bash sorted.sh *.pdb ../creatures/*.dat
```

If you forget to provide input as show below, the script
will start but not do anything. To exit from this state
hit Ctrl+C

```bash
bash sorted.sh
```

A short cut to save some useful commands is to redirect 
the current history to a file which becomes a script

```bash
history | tail -n 5 > redo-commands.sh
```

As you see it is natural to stack more than one command
in a script. So let's write a script that takes all
*.pdb* files as input and
<br>
1. Prints the file names that are provided 
2. Prints out 4<sup>th</sup> line from each 
file 
3. Combines all files in "all_molecules.txt"
4. Create copies with names "bckp-<file_name>"

```bash
vi myscript 
```

Repeat the routine to insert save and
quit in vim.

```bash
for filename in "$@"
    do
        echo $filename
        head -n 4 $filename | tail -n 1
        cat $filename >> all_molecules.txt
        cp $filename bckp-$filename
    done
```

Let's do some scripting with random numbers. 
Write a bash script to generate 1000 random numbers 
between 1 and 1000 and write them to a file. Find 
out how many unique numbers are obtained. <br>
(Hint: Try issuing \``echo $RANDOM`\, what do you get?)


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

Write a script that creates a folder at every 2 seconds with names
folder_01, ... folder_10 and let's you know when each folder is created
and the operation is ended. Finally, the script should show the created
folders and then delete them.

```bash
#!/usr/bin/env bash
counter=1

while [ $counter -le 10 ]; do
    sleep 2 #wait for 2 seconds
    mkdir folder_$(printf "%02d" $counter)

    if [ $counter -eq 10 ]; then
        echo "Folder ${counter} has been created"
        echo 'All folders are created'
    else
        echo "Folder ${counter} has been created"
    fi

    let counter=counter+1
done

ls -al | grep folder_
rm -Rf folder_*
```