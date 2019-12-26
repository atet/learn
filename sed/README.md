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
* [3. Basic Use](#3-basic-use)
* [4. Example Files](#4-example-files)
* [5. Your First `sed`](#5-your-first-sed)
* [6. `sed` and `grep`](#6-sed-and-grep)
* [7. Tabular Data](#7-tabular-data)
* [8. Bigger Data](#8-bigger-data)
* [9. Experiment](#9-experiment)
* [10. Next Steps](#10-next-steps)

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

## 3. Basic Use

### Prepare Environment

* Let's make a new directory named `stream` to work in then download an example text file:

```
$ cd ~
$ mkdir stream
$ cd stream
$ wget https://raw.githubusercontent.com/atet/learn/master/sed/data/hello.txt

<A BUNCH OF WGET STATUS TEXT>

$ ls
hello.txt
```

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 4. Example Files

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 5. Your First `sed`

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 6. `sed` and `grep`

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 7. Tabular Data

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 8. Bigger Data

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 9. Experiment

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 10. Next Steps

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