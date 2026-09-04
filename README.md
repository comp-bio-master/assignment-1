# Assignment 1: Pipes, Filters, and Finding Things

## Reading for Discussion Next lecture

[Wilson_etal_2017_good_enough_practices](../literature/Wilson_etal_2017_good_enough_practices_in_scientific_computing.pdf)

[Complete these questions about the reading](https://forms.cloud.microsoft/r/deB63CDLgD)

---

## Computer Preparation

Complete the [Computer Setup Checklist](../resources/computer_setup_checklist.md) which should have already been completed in the first lecture.

---

## Description of Assignment

We are going to flip the classroom again next week. Flipping the classroom means that you work on the material to be covered before we address it in lecture. Then we can spend time in lecture going over the most challenging topics, as identified by you. Then we will continue together in lecture through new material that builds upon this assignment.  This material is covered in ch 1.6 of the CSB book.

In Assignment 0, you learned how to navigate directories and work with files from the command line.

In this assignment, you will build on those skills by learning how to:

* redirect command output,
* connect commands using pipes,
* search inside files with `grep`,
* find files with `find`,
* process tabular data with commands such as `cut`, `sort`, and `uniq`,
* combine several commands to solve larger problems, and
* submit your work using Git.

You will work **entirely inside a local clone of this Assignment 1 repository**.

Keep this `README.md` open in your web browser on GitHub while working through the assignment in your terminal.

---

<details><summary><strong>1. Clone Your Assignment Repository</strong></summary>

## Clone Your Assignment Repository

When you accepted this GitHub Classroom assignment, GitHub created your own Assignment 1 repository.

On the GitHub webpage for **your Assignment 1 repository**:

1. Click the green **Code** button.
2. Select **SSH**.
3. Copy the SSH address.

In your terminal, go to your home directory:

```bash
cd ~
```

Clone your repository, giving the local clone the name `assignment-1`:

```text
git clone YOUR-COPIED-SSH-ADDRESS assignment-1
```

Enter the repository:

```bash
cd assignment-1
```

Check your location:

```bash
pwd
```

Your path should end with:

```text
/assignment-1
```

List the contents:

```bash
ls
```

You should see at least:

```text
README.md
shell-lesson-data
CSB
```

From this point forward, all of your work will remain inside the `assignment-1` repository.

</details>

---

<details>
<summary><strong>2. Pipes and Filters</strong></summary>

## Pipes and Filters

One of the most powerful features of Bash is the ability to combine small commands.

Instead of using one large program to perform an entire task, we can connect commands that each perform one simple job.

Enter the `exercise-data` directory:

```bash
cd shell-lesson-data/exercise-data
```

Look at the directory contents:

```bash
ls
```

You should see directories including:

```text
alkanes
animal-counts
creatures
writing
```

### Count lines with `wc`

Enter the `alkanes` directory:

```bash
cd alkanes
```

The directory contains several `.pdb` files.

Count the number of lines in one file:

```bash
wc -l cubane.pdb
```

Now count the lines in every `.pdb` file:

```bash
wc -l *.pdb
```

The `*` is a wildcard that matches any sequence of characters.

Therefore:

```text
*.pdb
```

matches every filename ending in `.pdb`.

---

### Redirect output with `>`

Normally, output is printed to the terminal.

You can instead redirect the output to a file:

```bash
wc -l *.pdb > lengths.txt
```

Display the new file:

```bash
cat lengths.txt
```

The general form is:

```text
command > filename
```

> ⚠️ **CAUTION:** `>` replaces the contents of the output file if the file already exists.

To **append** output to an existing file instead, use:

```text
>>
```

For example:

```bash
echo "another line" >> lengths.txt
```

---

### Sort output

Run:

```bash
sort lengths.txt
```

By default, `sort` sorts alphabetically.

To sort numerically:

```bash
sort -n lengths.txt
```

You can also use `head` to show only the beginning of the output:

```bash
sort -n lengths.txt | head
```

The vertical bar:

```text
|
```

is called a **pipe**.

A pipe passes the output of the command on the left to the input of the command on the right.

You can therefore do everything above without creating `lengths.txt`:

```bash
wc -l *.pdb | sort -n | head
```

You can connect more than two commands in a pipeline.

For example, show the three `.pdb` files with the fewest lines:

```bash
wc -l *.pdb | sort -n | head -n 3
```

Remove the temporary file:

```bash
rm lengths.txt
```

### Key idea

Read pipelines from **left to right**.

For:

```bash
wc -l *.pdb | sort -n | head -n 3
```

Bash:

1. counts the lines,
2. sends those results to `sort`,
3. sorts them numerically,
4. sends the sorted results to `head`,
5. displays the first three lines.

</details>





























<details><summary>Software Carpentry</summary>
<p>

Complete the [Pipes & Filters](https://swcarpentry.github.io/shell-novice/04-pipefilter.html) tutorial on software carpentry

Complete the [Finding Things](https://swcarpentry.github.io/shell-novice/07-find.html) tutorial on software carpentry

> [!NOTE]
> In some of the "Challenge" boxes, scripts are discussed.  We have not yet covered scripts so you can skip over these parts.

> [!NOTE]
> We will have extra dirs and files from completing the previous lessons when compared to the example output given in Software carpentry

> [!NOTE]
> $() is a way of opening an invisible shell and running the command inside the parentheses. In this line from the Software Carpentry lesson, `grep "searching" $(find . -name "*.txt")`, `find` is run in a subshell to run `grep` for the pattern `searching` on all files ending in `.txt`.

</p>
</details>

---

<details><summary>Advanced `bash` Commands</summary>
<p>

Work through the following tutorial. Note the instructions to clone the CSB repo in the Computer Preparation instructions above


---

### Move the the `CSB/unix/sandbox` directory

```bash
# let’s start by moving to our sandbox in the unix dir of the CSB repo
# you must have cloned the CSB repo to your home dir for this path to work
$ cd ~/CSB/unix/sandbox
$ pwd
```

After running `cd ~/CSB/unix/sandbox`, your present working directory (`pwd`) is `sandbox`.  If the `cd ~/CSB/unix/sandbox` failed, then you should consult the [Computer Preparation Section](#computer-preparation) above

```
CSB/unix
├── data
│   ├── Saavedra2013
│   └── miRNA
├── installation
├── **sandbox**  #YOU SHOULD BE HERE!
└── solutions
```

---

### Redirection of output ([stdout](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_(stdout))) to file `[command] > filename`, Append [stdout](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_(stdout)) to file `[command] >> filename`, Redirect contents of file to [stdin](https://en.wikipedia.org/wiki/Standard_streams#Standard_input_(stdin)) `[command] < filename` 

```
# print text to screen, then print to file, then print file to screen
$ echo "My first line" 
My first line

$ echo "My first line" > test.txt
$ cat test.txt
My first line

# append file with additional text, then print file to screen
$ echo "My second line" >> test.txt
$ cat test.txt
My first line
My second line
```

&#x1F4A1; TIP! _use `Tab` key to autocomplete names, prevent spelling mistakes_

---


### Problem Solving Scenario

A machine provides you with thousands of data files. There’s so many, it is freezing your Win/Mac GUI file browser. How can you determine the number of files?

We will use the dir `unix/data/Saavedra2013` as an example of a directory with many files

```
CSB/unix
├── data
│   ├── Saavedra2013
│   └── miRNA
├── installation
├── **sandbox**  #YOU ARE HERE!
└── solutions
```

&#x1F4A1; TIP! _To specify `unix/data/Saavedra2013` from `unix/sandbox` you can use the relative path `../data/Saavedra2013`_

```bash
# save file names to file in pwd
$ ls ../data/Saavedra2013 > filelist.txt

# look at the file
$ cat filelist.txt

# count lines in the file
$ wc -l filelist.txt

# remove the file
$ rm filelist.txt
```

---

### Piping Text Streams From One Command to the Next with `|`

![Common Operating Systems](../lectures/Week01_files/pipeline.png)

![Common Operating Systems](../lectures/Week01_files/pipeline2.png)

A pipe `|` passes the [stdout](https://en.wikipedia.org/wiki/Standard_streams#Standard_output_(stdout)) from one command to the [stdin](https://en.wikipedia.org/wiki/Standard_streams#Standard_input_(stdin)) of another

&#x2753; QUESTION _How many files are there in `CSB/unix/data/Saavedra2013`?_

```
CSB/unix
├── data
│   ├── Saavedra2013
│   └── miRNA
├── installation
├── **sandbox**  #YOU ARE HERE!
└── solutions
```

```bash
# list file names
$ ls ../data/Saavedra2013

# list file names and pipe into wc to return the number of files
$ ls ../data/Saavedra2013 | wc –l
59

```

---

### [TSV](https://en.wikipedia.org/wiki/Tab-separated_values) & [CSV](https://en.wikipedia.org/wiki/Comma-separated_values) Data Files

In the tidy table below, columns are _*delimited*_ by tabs.  The first column has no column header but is the sample ID.  Ozone, Solar.R, Wind, Temp, Month, and Day are all pieces of data (dimensions) describing each of the 10 samples.

![Common Operating Systems](../lectures/Week01_files/tsv.png)

* Tab Separated Values (TSV)

  * Tabs denote columns

* Comma Separated Values (CSV)

  * Commas denote columns
  
* [Tidy data](https://en.wikipedia.org/wiki/Tidy_data)

  * Each [row](https://en.wikipedia.org/wiki/Row_(database)) is one [unit of observation](https://en.wikipedia.org/wiki/Unit_of_observation)
  
  * Each [column](https://en.wikipedia.org/wiki/Column_(database)) is one dimension or aspect of the units of observation
  
* File extensions are not always accurate, so it is important to view a file to be sure of the delimiter.


Tidy Table:
| Column 1 Header | Column 2 Header | Column 3 Header |
| --------------- | --------------- | --------------- |
| Row 1 Column 1 | Row 1 Column 2 | Row 1 Column 3 |
| Row 2 Column 1 | Row 2 Column 2 | Row 2 Column 3 |
| Row 3 Column 1 | Row 3 Column 2 | Row 3 Column 3 |
| Row 4 Column 1 | Row 4 Column 2 | Row 4 Column 3 |

TSV
```
Column 1 Header	Column 2 Header	Column 3 Header
Row 1 Column 1	Row 1 Column 2	Row 1 Column 3
Row 2 Column 1	Row 2 Column 2	Row 2 Column 3
Row 3 Column 1	Row 3 Column 2	Row 3 Column 3
Row 4 Column 1	Row 4 Column 2	Row 4 Column 3
```

&#x26A0; CAUTION! _Do not type in these code blocks.  They are here to show you TSV and CSV formatting_

TSV File with tabs denoted by `\t`.  Note your text files will not contain `\t`.  I did this show where tabs were, versus spaces. This is also the first use of a regular expression in this course.  The `\` is the escape character, which changes the meaning of the character that follows.  `\t` is the regular expression for a tab. Regular expressions are recognized by almost all commands across all computer languages that use a pattern (`\t`) to find matching text (tab character).

```
Column 1 Header\tColumn 2 Header\tColumn 3 Header
Row 1 Column 1\tRow 1 Column 2\tRow 1 Column 3
Row 2 Column 1\tRow 2 Column 2\tRow 2 Column 3
Row 3 Column 1\tRow 3 Column 2\tRow 3 Column 3
Row 4 Column 1\tRow 4 Column 2\tRow 4 Column 3
```

CSV
```
Column 1 Header, Column 2 Header, Column 3 Header
Row 1 Column 1, Row 1 Column 2, Row 1 Column 3
Row 2 Column 1, Row 2 Column 2, Row 2 Column 3
Row 3 Column 1, Row 3 Column 2, Row 3 Column 3
Row 4 Column 1, Row 4 Column 2, Row 4 Column 3
```

---


### Convert Among Formats Using `tr "<old delimiter>" "<new delimiter>"`

```bash
# view contents of csv
$ less -S ../data/Pacifici2013_data.csv 

# replace semicolons with commas using tr [find] [replace]
$ cat ../data/Pacifici2013_data.csv | tr “;” “,” | less –S

# view as tsv
# \t is the nearly universal symbol for tab
$ cat ../data/Pacifici2013_data.csv | tr ";" "\t" | less -S

```

&#x1F4A1; _`tr` is an abbreviation for translate_

---


### Using `cut` to retrieve/isolate/select columns and `head` to retrieve rows

```bash
# change directory
$ cd ~/CSB/unix/data

# display first line of file (i.e., header of CSV file)
$ head -n 1 Pacifici2013_data.csv

# display first column of file
$ cut -d ";" –f 1 Pacifici2013_data.csv

# display second through fourth columns
$ cut -d ";" -f 2-4 Pacifici2013_data.csv

# display first “cell” of data
$ head -n 1 Pacifici2013_data.csv | cut -d ";" -f 1

```

&#x1F4A1; _`cut` assumes tab delimited files.  If a different delimiter is used in the file, the `-d` option is used to specify the delimiter.  It is very easy to mistake spaces for tabs, and that will make `cut` do odd things with your data if you do not set `-d " "`_

---


### Connecting `cut` `head` `tail` `sort` `uniq`

```bash
# select 2nd column, display first 5 elements
$ cut -d ";" -f 2 Pacifici2013_data.csv | head -n 5

# select 2nd and 8th columns, display first 3 elements
$ cut -d ";" -f 2,8 Pacifici2013_data.csv | head -n 3

# select 2nd column without header, show 5 first elements
$ cut -d ";" -f 2 Pacifici2013_data.csv | tail -n +2 | head -n 5

# identify the orders in csv
# select 2nd column without header, unique sorted elements
$ cut -d ";" -f 2 Pacifici2013_data.csv | tail -n +2 | sort | uniq

# count how many records per order in csv
$ cut -d ";" -f 2 Pacifici2013_data.csv | tail -n +2 | sort | uniq -c

# output the order with the most records, including the number of records in csv
$ cut -d";" -f2 ../data/Pacifici2013_data.csv |  tail -n +2 | sort | uniq -c | tr -s " " "\t" | cut -f2-3 | sort -n | tail -n1

```

&#x1F4A1; _`uniq` is a command that that removes consecutive duplicate lines (rows). For this reason, the input to `uniq` is almost always sorted beforehand.  Use `man uniq` to see the description of the `-c` option.  I use `uniq -c` all the time._

&#x1F4A1; _`sort -t";"` specifies the delimiter character, also known as a field separator.  Try `man sort` and search `/field` to see the manual entry for this._

&#x1F4A1; _`tr -s` can be used to easily convert files or text streams that have multiple spaces in between columns (such as the output of `uniq -c` into a tab separated format.  The `-s` means squish consecutive charcters to one character_

---

### Advanced Pipelining

When constructing long pipelines like the last one in the code block above, you should build it step by step, testing the output as you go.  This strategy reduces the possibility of making a mistake.

I like to use `less -S` or `head` to capture and view the output when it takes up many lines.  The `q` key closes the `less` viewer.

```
# here is an example of how to build the really long pipe above, from scratch
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | less -S
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | tail -n +2 | head
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | tail -n +2 | sort | head
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | tail -n +2 | sort | uniq -c | less -S
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | tail -n +2 | sort | uniq -c | tr -s " " "\t" | head
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | tail -n +2 | sort | uniq -c | tr -s " " "\t" | cut -f2-3 | head
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | tail -n +2 | sort | uniq -c | tr -s " " "\t" | cut -f2-3 | sort -n | less -S
$ cut -d";" -f2 ../data/Pacifici2013_data.csv | tail -n +2 | sort | uniq -c | tr -s " " "\t" | cut -f2-3 | sort -n | tail -n1
```

</p>
</details>

---

<details><summary>Mind Expander 1.3</summary>
<p>

[Mind Expander 1.3 Form](https://forms.office.com/Pages/ResponsePage.aspx?id=8frLNKZngUepylFOslULZlFZdbyVx8RLiPt1GobhHnlUOThBNjZNVzlGQUtJUzhYREZVSE5UVVJMNS4u)

</p>
</details>

---

<details><summary>Exercise 1.10.1</summary>
<p>

Complete [Exercise 1.10.1 Next Generation Sequencing Data](https://forms.office.com/Pages/ResponsePage.aspx?id=8frLNKZngUepylFOslULZlFZdbyVx8RLiPt1GobhHnlUMTVENFg0UjhFTzc3Wkc0NExRTjdLSjdGNi4u) using the commands you've learned and the `grep` command. Please consult the [Unix/Linux Cheat Sheet](../resources/CheatSheetLinux_2022-09-02.pdf). Make sure that you document your work by saving your answers for each question in a text document (use notepad++  or bbedit).  Then when done, copy and paste your answers into the form and submit.  We will review this in class

</p>
</details>

---


## CSB Book Versus Online Materials

While the CSB book is not required, I include this to help those that do use it.

The _*New Material*_ closely follows the book but there is some additional information that is not provided in the book (and vice versa). In the lecture slides, the `code blocks` are represented by green text on a black background, mimicking the terminal.

The material below closely follow the book but there is some additional information that is not provided in the book (and vice versa). If you choose to follow the lecture slides, the `code blocks` are represented by green text on a black background, mimicking the terminal.

* Page 35 **Use _BodyMass.csv_ (slides) rather than _BodyM.csv_ (book)**

* Page 46, the script on the bottom half of the page is poor form. Making a bunch of tmp files is a bad idea.  Do this instead:

```
#!/bin/bash

# to run do this:
# ./ExtractBodyM.sh [infile] [outfile]

# isolate columns 2-6 of csv (first argument) using cut
# translate the ; to “ “ using tr
# remove the header row using tail
# sort by sixth column, descending order
# save to file (second argument)

# isolate columns 2-6 of csv (first argument) using cut
cut -d ";" -f 2-6 $1 | \
 # translate the ; to “ “ using tr
	tr ";" " " | \
 # remove the header row using tail
	tail -n+2 | \
 # sort by sixth column, descending order
 # save to file (second argument)
	sort -nrk6 > $2
```

