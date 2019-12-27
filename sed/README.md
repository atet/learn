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
* [5. `sed` and `grep`](#5-sed-and-grep)
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

* Each line starts with `$` below, _type everything after this_
* Let's start at your home directory (a.k.a. ~) and make a new empty directory to work from:

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

### Substitution

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

### Multiple Patterns

* We missed the last occurence of "hello" above, this is due to the lowercase "h"
* Let's try chaining together multiple `sed` commands using the "`-e`" flag:

```
$ sed -e "s/Hello/Goodbye/g" -e "s/hello/goodbye/g" hello.txt
Goodbye World! Goodbye, goodbye.
```

* Actually, let's substitute only the second and later occurrances of "Hello"; we can use the suffix with a number to signify this:

```
$ sed -e "s/Hello/Goodbye/2" -e "s/hello/goodbye/g" hello.txt
Hello World! Goodbye, goodbye.
```

### Syntax

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

### Print Control

* Let's download a file that has multi-line data:

```
$ wget https://raw.githubusercontent.com/atet/learn/master/sed/data/chuck.txt

<A BUNCH OF WGET STATUS TEXT>

$ cat chuck.txt
1. Chuck Norris can hear sign language.
2. Death once had a near-Chuck-Norris experience.
3. Chuck Norris can kill 2 stones with 1 bird.
4. Big foot claims he saw Chuck Norris.
5. Chuck Norris makes onions cry.
```

* With print control we can output only lines that have specific matches
* Let's output only lines that contain a match using the suffix "`p`" (print) combined with the `-n` flag (see what happens if you don't use this flag in conjuction with "`p`"):

```
$ sed -n "/hear/p" chuck.txt
1. Chuck Norris can hear sign language.
```


* Let's remove lines that don't contain a match using the suffix "`d`" (deletion):

```
$ sed "/hear/d" chuck.txt
2. Death once had a near-Chuck-Norris experience.
3. Chuck Norris can kill 2 stones with 1 bird.
4. Big foot claims he saw Chuck Norris.
5. Chuck Norris makes onions cry.
```


[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 5. `sed` and `grep`


[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 6. Tabular Data

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

1. chuck.html is adapted from: <a href="https://en.wikipedia.org/wiki/Chuck_Norris_filmography" target="_blank">https://en.wikipedia.org/wiki/Chuck_Norris_filmography</a>
2. chuck.txt is adapted from: <a href="https://chucknorrisfacts.net/top-100" target="_blank">https://chucknorrisfacts.net/top-100</a>

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2019-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>