# [atet](https://github.com/atet) / [learn](https://github.com/atet/learn) / [**_sed_**](https://github.com/atet/learn/tree/master/sed)

[![.img/logo_sed.png](.img/logo_sed.png)](#nolink)

# Introduction to Stream Editor

**This is part of a two-tutorial series on text editing in Bash: I recommend to first finish [Atet's 15 Minute Tutorial on Regular Expressions](https://github.com/atet/learn/blob/master/regex/README.md#atet--learn--regex) to put this content in better context**

* Estimated time to completion: 15 minutes.
* This quick introduction to stream editor (sed) is meant to cover only the absolute necessary material to get you up and running in a minimal amount of time.
* You are here because **you want to learn a few simple tricks to quickly process large amounts of text data**.
* We will be using <a href="https://en.wikipedia.org/wiki/Bash_(Unix_shell)" target="_blank">Bash Command Line Interface (CLI)</a> to perform basic operations; advanced material is not covered here.

--------------------------------------------------------------------------------------------------

## Table of Contents

### Introduction

* [0. Requirements](#0-requirements)
* [1. Installation](#1-installation)
* [2. Preface](#2-preface)
* [3. Example Files](#3-example-files)
* [4. Your First `sed`](#4-your-first-sed)
* [5. More `sed`](#5-more-sed)
* [6. Tabular Data](#6-tabular-data)
* [7. Bigger Data](#7-bigger-data)
* [8. Experiment](#8-experiment)
* [9. Next Steps](#9-next-steps)

### Supplemental

* [Other Resources](#other-resources)
* [Troubleshooting](#troubleshooting)
* [Acknowledgments](#acknowledgments)

--------------------------------------------------------------------------------------------------

## 0. Requirements

* This tutorial was developed on Microsoft Windows 10 with Windows Subsystem for Linux (WSL) using Ubuntu 18.04 LTS
* If you are using MacOS, [your Terminal program is Bash](https://en.wikipedia.org/wiki/Terminal_(macOS))
* Most Linux distributions use or can use Bash

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 1. Installation

### Windows 10

* Windows Subsystem for Linux (WSL) is a fully supported Microsoft product for Windows 10, learn how to install it here: [https://docs.microsoft.com/en-us/windows/wsl/install-win10](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* Please choose Ubuntu 18.04 LTS as the distribution you use with WSL
* WSL is only available for Windows 10

### MacOS

* You do not need to install anything, [your Terminal program is Bash](https://en.wikipedia.org/wiki/Terminal_(macOS))

### Linux

* I recommend using Ubuntu 18.04 LTS

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 2. Preface

### Stream Editor

> "`sed` is a stream editor. A stream editor is used to perform basic text transformations on an input stream (a file or input from a pipeline)."
>
> [gnu.org](https://www.gnu.org/software/sed/manual/sed.html#Introduction)

* Basically, `sed` can replace words with other words
* When used in combination with `grep`, you can make a powerful [pipelines (commands "piped" together using "`|`")](https://www.gnu.org/software/bash/manual/html_node/Pipelines.html) that can quickly manipulate huge amounts of data

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 3. Example Files

* Each line starts with "`$`" below, _type everything after this_
* Let's start at your home directory (a.k.a. "`~`") and make a new empty directory to work from:

```
$ cd ~
$ mkdir stream
$ cd stream
```

* Download the example file from my GitHub using `wget` and check the file's contents:

```
$ wget https://raw.githubusercontent.com/atet/learn/master/sed/data/hello.txt

<A BUNCH OF WGET STATUS TEXT>

$ ls
hello.txt
$ cat hello.txt
Hello World! Hello, hello.
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 4. Your First `sed`

### 4.1. Substitution

* Let's substitute ("`s`" prefix) "Hello" with "Goodbye":

```
$ sed "s/Hello/Goodbye/" hello.txt
Goodbye World! Hello, hello.
```

* Looks like we didn't substitute all the occurrences of "Hello", let's use the global prefix "`g`" to signify this

```
$ sed "s/Hello/Goodbye/g" hello.txt
Goodbye World! Goodbye, hello.
```

### 4.2. Multiple Patterns

* We missed the last occurence of "hello" above, this is due to the lowercase "h"
* Let's try chaining together multiple `sed` commands using the "`-e`" flag before each link:

```
$ sed -e "s/Hello/Goodbye/g" -e "s/hello/goodbye/g" hello.txt
Goodbye World! Goodbye, goodbye.
```

* Actually, let's substitute only the second and later occurrances of "Hello"; we can use the suffix with a number to signify this:

```
$ sed -e "s/Hello/Goodbye/2" -e "s/hello/goodbye/g" hello.txt
Hello World! Goodbye, goodbye.
```

### 4.3. Syntax

* Well that was easy, but what did the commands we just entered mean?
* Let's break down the above into parts:

Command | Description
--- | ---
`sed` | Calling the `sed` program
`"s/Hello/Goodbye/g"` | The processing to be done (in between quotes)
`hello.txt` | The file to be worked on

* Let's break down the processing syntax in between the quotes:

Command | Description
--- | ---
`s` | Prefix "`s`" means a substitution 
`/` | The slash character is a delimiter
`Hello` | The word to be replaced (case sensitive)
`Goodbye` | The word that is replacing the first word
`g` | Suffix "`g`" means globally change

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 5. More `sed`

### 5.1. Print Control

* Let's download a file that has multi-line data<sup>[[1]](#acknowledgments)</sup>:

```
$ wget https://raw.githubusercontent.com/atet/learn/master/sed/data/chuck.txt
```

* With print control we can output only lines that have specific matches
* Let's output only lines that contain a match using the suffix "`p`" (print) **combined with** the `-n` flag (see what happens if you don't use this flag in conjuction with "`p`"):

```
$ sed -n "/bird/p" chuck.txt
1. Chuck Norris can kill 2 stones with 1 bird.
```

* Let's remove lines that don't contain a match using the suffix "`d`" (deletion):

```
$ sed "/bird/d" chuck.txt
2. Death once had a near-Chuck-Norris experience.
3. Chuck Norris can hear sign language.
4. Big foot claims he saw Chuck Norris.
5. Chuck Norris makes onions cry.
```

### 5.2. Print Control with Patterns

* Adding a pattern to be searched for first before performing a replacement on that line:

```
$ sed -n "/1./ s/Chuck/Charles/p" chuck.txt
1. Charles Norris can kill 2 stones with 1 bird.
```

* Notice only the line that had a unique "`1.`" had `Chuck` substituted with `Charles`
* Additional commands can be chained together also:
   * Print control parameters should be on the last link in the chain

```
$ sed -e "/1./ s/Chuck/Charles/" -ne "s/2/two/p" chuck.txt
1. Charles Norris can kill two stones with 1 bird.
two. Death once had a near-Chuck-Norris experience.
```

* Oops, didn't mean to change "`2.`" to `two` on the second line, need to be more specific with that second chained command:

```
$ sed -e "/1./ s/Chuck/Charles/" -ne "/1./ s/2/two/p" chuck.txt
1. Charles Norris can kill two stones with 1 bird.
```

* Let's globally change all numerals to text, e.g. "`1`" will be substituted with "`one`":

```
$ sed -e "s/1/one/g" -ne "s/2/two/gp" chuck.txt
one. Chuck Norris can kill two stones with one bird.
two. Death once had a near-Chuck-Norris experience.
```

* Oops, didn't want to change the line numbers such as "`1.`" into text
* Let's add spaces before and after what we want to match to help make our pattern a bit more specific:
   * E.g. "`1.`" doesn't have a space before or after, so it shouldn't match

```
$ sed -e "s/ 1 /one/g" -ne "s/ 2 /two/gp" chuck.txt
1. Chuck Norris can killtwostones withonebird.
```

* Almost, just forgot to add spaces before and after the substitution:

```
$ $ sed -e "s/ 1 / one /g" -e "s/ 2 / two /g" chuck.txt
1. Chuck Norris can kill two stones with one bird.
2. Death once had a near-Chuck-Norris experience.
3. Chuck Norris can hear sign language.
4. Big foot claims he saw Chuck Norris.
5. Chuck Norris makes onions cry.
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 6. Tabular Data

* We can combine some regex syntax used in `grep` so that `sed` will recognize specific patterns to replace
* Let's download the raw HTML code for a webpage that contains a table of information<sup>[[2]](#acknowledgments)</sup>:

```
$ wget https://raw.githubusercontent.com/atet/learn/master/sed/data/chuck.html

<A BUNCH OF WGET STATUS TEXT>

$ head -n 10 chuck.html
<!DOCTYPE html>
<html>
   <head>
      <meta charset="UTF-8">
      <style>
         table {
            font-family: Arial, Helvetica, sans-serif;
            border-collapse: collapse;
            width: 100%;
         }
```

* If you haven't seen raw HTML code, it's basically a language of organized and nested elements that describe a webpage
* Though the code above could be all in one line, it's industry standard to make it look a bit nice with line breaks and tab spacing
* The HTML is ultimately instructions for your web browser to render a web page:

[![.img/step06a.png](.img/step06a.png)](#nolink)

### HTML format

* Looking back at the raw HTML, let's look at the meat of the HTML table:
   * The commands below first takes the first 35 lines of the file `chuck.html` with `head` then pipes it into `tail` to only output the last eight lines

```
$ head -n 35 chuck.html | tail -n 8
         <tr>
            <th>Title</th>
            <th>Year</th>
            <th>Actor</th>
            <th>Executive Producer</th>
            <th>Writer</th>
            <th>Role</th>
         </tr>
```

* The table will have an entry for each movie with six columns of information
* Let's look at another part of the table to see and example of a movie entry:
   * Instead of using `head` piped into `tail`, we will use `sed` to display a range of lines in the file
   * The commands below uses `sed` print control to output only lines 276 through 283

```
$ sed -n '276,283p' chuck.html
         <tr>
            <td>The Expendables 2</td>
            <td>2012</td>
            <td>Y</td>
            <td>N</td>
            <td>N</td>
            <td>Booker "The Lone Wolf"</td>
         </tr>
```

### Goal

* Let's try converting the nested HTML table into comma separated value (CSV) format:

```
Title,Year,Actor,Executive Producer,Writer,Role
.
.
.
The Expendables 2,2012,Y,N,N,Booker "The Lone Wolf"
```

* This will require a couple steps:
   * Getting rid of a lot of standard HTML tags (e.g. "`<tr>`")
   * Converting a multi-line, nested entry into a single line separated by commas

### Linearize

* You've seen that there is a specific structure that HTML tables must adhere to
* We are going to use `grep` to only extract the lines that have relevant HTML table information:
   * HTML tags that define a table are `table`, `tr`, `th`, and `td`
   * Tags come in pairs, so a beginning and end of a table would be `<table>...</table>`

```
$ grep -i -e "</*table\|</*tr\|</*th\|</*td" chuck.html > chuck2.html
```

* Let's breakdown the "`</*table\|...`" processing that is replaced by nothing (i.e. deletes this pattern)

`grep` Syntax | Definition
--- | ---
`<` | Literal left bracket
`/*` | Literal slash and quantifier of zero or more
`table` | Literal string "`table`", with "`grep -i`" makes it case insensitive
`\\|` | Regex "or" (must be escaped with backslash)

* Let's not modify the original source file; the HTML table-only code has been redirected to the new file `chuck2.html`
* Let's get rid of all the nested spacing; nesting is always a leading set of spaces or tabs before each line

```
$ sed "s/^[\ \t]*//g" chuck2.html > chuck3.html
```

* Let's breakdown the "`^[\ \t]*`" processing that is replaced by nothing (i.e. deletes this pattern)

`sed` Syntax | Definition
--- | ---
`^` | Anchor at the beginning of the line
`[` `]` | Anything between this can be matched
"`\ `" | Space
"`\t`" | Tab
`*` | Quantifier zero or more

* Let's remove all the newline-carriage returns (`\n\r`) and make all the text in a single line
* We have to use another program called `tr` (translate) to read in `chuck3.html` make the deletion and redirect the output into `chuck4.html`
   * Remember, that all these different programs were made by different people; so the way files are read in may be different

```
$ tr -d '\n\r' < chuck3.html > chuck4.html
```

* Replace `</tr>` with newline-carriage return:

```
$ sed "s/<\/tr[^>]*>/\n\r/Ig" chuck4.html > chuck5.html
```

* Remove `<table>` and `<tr>` tags:

```
$ sed "s/<\/*\(table\|tr\)[^>]*>//Ig" chuck5.html > chuck6.html
```

* Remove ^`<td>`, ^`<th>`, `</td>`$, `</th>`$:

```
$ sed "s/^<t[dh][^>]*>\|<\/*t[dh][^>]*>$//Ig" chuck6.html > chuck7.html
```

* Substitute `</td><td>` with comma:

```
$ sed "s/<\/t[dh][^>]*><t[dh][^>]*>/,/Ig" chuck7.html > chuck8.html
```

**Congratulations! You've just performed your very first "webscraping", a very useful skill to have in your toolbelt**

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 7. Bigger Data

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 8. Experiment

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 9. Next Steps

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Other Resources

Description | Link
--- | ---
`sed` Manual | https://www.gnu.org/software/sed/manual/sed.html
Bash Reference Manual | https://www.gnu.org/software/bash/manual/bash.pdf

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Troubleshooting

Issue | Solution
--- | ---
I need more delimiters | https://stackoverflow.com/questions/33914360/what-delimiters-can-you-use-in-sed

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Acknowledgments

1. chuck.txt is adapted from: <a href="https://chucknorrisfacts.net/top-100" target="_blank">https://chucknorrisfacts.net/top-100</a>
2. chuck.html is adapted from: <a href="https://en.wikipedia.org/wiki/Chuck_Norris_filmography" target="_blank">https://en.wikipedia.org/wiki/Chuck_Norris_filmography</a>

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2019-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>