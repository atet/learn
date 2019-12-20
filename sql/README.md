# [atet](https://github.com/atet) / [learn](https://github.com/atet/learn) / [**_sql_**](https://github.com/atet/learn/tree/master/sql)

[![.img/logo_sqlite.png](.img/logo_sqlite.png)](#nolink)

# Introduction to SQL

* Estimated time to completion: 15 minutes.
* This quick introduction to [Structured Query Language (SQL)](https://en.wikipedia.org/wiki/SQL) is meant to cover only the absolute necessary material to get you up and running in a minimal amount of time.
* You are here because you want to use SQL to manage (view, extract, and/or manipulate) data in a [Relational Database Management System (RDMS)](https://en.wikipedia.org/wiki/Relational_database#RDBMS).
* We will be using [SQLite](https://www.sqlite.org/index.html) to perform basic operations; advanced material is not covered here.

--------------------------------------------------------------------------------------------------

## Table of Contents

### Introduction

* [0. Requirements](#0-requirements)
* [1. Installation](#1-installation)
* [2. Example Data](#2-example-data)
* [3. Loading Data](#3-loading-data)
* [4. Navigation](#4-navigation)
* [5. Your First Query](#5-your-first-query)
* [6. Data Manipulation Concept](#6-data-manipulation-concept)
* [7. Data Manipulation Queries](#7-data-manipulation-queries)
* [8. Experiment](#8-experiment)

### Supplemental

* [Epilogue](#Epilogue)
* [Troubleshooting](#troubleshooting)
* [SQLite vs. other SQL implementations](#sqlite-vs-other-sql-implementations)
* [Acknowledgments](#acknowledgments)

--------------------------------------------------------------------------------------------------

## 0. Requirements

* This tutorial was developed on Microsoft Windows 10.
* SQLite and SQLiteStudio is also available for MacOS and Linux.

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 1. Installation

* We will use SQLiteStudio, which is a Graphical User Interface (GUI) created for SQLite: [https://sqlitestudio.pl/index.rvt?act=download](https://sqlitestudio.pl/index.rvt?act=download)
* Download the "Windows (portable), 32-bit" version: [https://sqlitestudio.pl/files/sqlitestudio3/complete/win32/SQLiteStudio-3.2.1.zip](https://sqlitestudio.pl/files/sqlitestudio3/complete/win32/SQLiteStudio-3.2.1.zip)
   * Note: This link may break as new versions are released.

[![.img/step01a.png](.img/step01a.png)](#nolink)

* Unzip the file find and run "SQLiteStudio.exe".
* After choosing your language setting and you will be presented with your working environment.

[![.img/step01b.png](.img/step01b.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 2. Example Data

* We will use a small dataset of vehicles as an example<sup>[[1]](#acknowledgments)</sup>.
* Click here for the dataset (right-click and "Save as..." then save as _mtcars.csv_): <a href="https://raw.githubusercontent.com/atet/learn/master/sql/data/mtcars.csv" target="_blank">https://raw.githubusercontent.com/atet/learn/master/sql/data/mtcars.csv</a>
* This Comma Separated Values (CSV) file contains 32 records of vehicles and 12 attributes describing them (e.g. "id" = name, "mpg" = miles per gallon, etc.):

[![.img/step02.png](.img/step02.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 3. Loading Data

* First, create a new _database_:
   * Click on "Add a database" or CTRL+O
   * Leave Database type as default SQLite 3
   * Give your File a name, e.g. "testdb" (this will also be the database name)
   * Click on OK
   * **IMPORTANT: You must connect to this newly created _database_ to work on it**

[![.img/step03a.png](.img/step03a.png)](#nolink)

* Second, load the _mtcars.csv_ file as a new _table_ in the database:
   * Note: A database can have multiple tables in it, analogous to an Excel workbook having multiple worksheets
   * Select "Import"
   * Give the incoming data a table name, (e.g. "mtcars")
   * **IMPORTANT: Make sure you select "First line represents CSV column names"**
   * Click Next
   * Navigate to where you downloaded the _mtcars.csv_
   * Click Finish

[![.img/step03b.png](.img/step03b.png)](#nolink)

* You will get a console message that "_Imported data to the table 'mtcars' successfully._" and _mtcars_ is now seen in the hierarchy of the database you created.

[![.img/step03c.png](.img/step03c.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 4. Navigation

* You can view the imported _mtcars_ data in tabular format by selecting the table on the left-hand side, Data tab, and Grid view tab.
* You will execute SQL queries when you select "Create a view".

[![.img/step04a.png](.img/step04a.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 5. Your First Query

* Once you select "Create a view", a new bottom tab will appear for the new view.
* We are going to make a view that basically selects all the data from the _mtcars_ table.
   * Name the view "all"
   * In the text box, type out `SELECT * FROM mtcars;` (make sure you have the semicolon at the end)
   * Press the green "Commit the view changes" button
   * A confirmation window "Queries to be executed" will pop up, select OK

[![.img/step05a.png](.img/step05a.png)](#nolink)

* You will get a console message that "_Committed changes for view 'all' (named before '') successfully._" and the _all_ view is now seen in the hierarchy of the database you created.
* You can navigate this view as you would a regular table.

[![.img/step05b.png](.img/step05b.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 6. Data Manipulation Concept

* The general concept is that you have data in your database **tables**, and you are generating a customized **view** that was manipulated by your queries.

**What did "`SELECT * FROM mtcars;`" mean?**

* This query means that you want to `SELECT` all rows (and columns), this is represented by the wildcard `*` (asterisk), `FROM` table `mtcars`.

```{sql}
SELECT * FROM mtcars;
```

* We are basically viewing everything from the _mtcars_ **table** in the _all_ **view**.

[![.img/step06.png](.img/step06.png)](#nolink)

_**Figure 6.** Concept of `SELECT`ing everything. Basically, viewing the entire table._

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 7. Data Manipulation Queries

* We will go through four common data manipulation queries here.

### 7.a. Subsetting rows

* You can subset rows (a.k.a. observations) by their values.

```{sql}
SELECT * FROM mtcars WHERE cyl >= "6";
```

* E.g. Select vehicles that have six or more engine cylinders (column "cyl").

[![.img/step07a.png](.img/step07a.png)](#nolink)

_**Figure 7.a.** Only returning rows that meet some criteria._

### 7.b. Subsetting columns

* You can subset only the columns (a.k.a. variables) that you need.

```{sql}
SELECT id, mpg FROM mtcars;
```

* E.g. Select only vehicle name (column "id") and fuel efficiency (column "mpg"), we don't need the rest of the columns.

[![.img/step07b.png](.img/step07b.png)](#nolink)

_**Figure 7.b.** Only returning required columns._

### 7.c. Make new columns

* You can make new columns (a.k.a. variables) based on calculations.

```{sql}
SELECT id, disp, (disp * 0.0164) AS disp2 FROM mtcars;
```

* E.g. Add a new column _disp2_ that multiplies the _disp_ column (cubic inches) by 0.0164 to give displacement in liters. Show only columns _id_, _disp_, and new displacement in liters `AS` column _disp2_.

[![.img/step07c.png](.img/step07c.png)](#nolink)

_**Figure 7.c.** Add new columns with values calculated from other variables._

### 7.d. Summarize data

* You can summarize many observations into fewer values while making new columns based on calculations.

```{sql}
SELECT cyl, AVG(disp) AS meandisp FROM mtcars GROUP BY cyl;
```

* E.g. Mean (average) displacement for vehicles grouped by cylinder count.
   * Fewer observations: Individual vehicles will be summarized by grouping them by cylinder count.
   * New columns: Mean displacement.

[![.img/step07d.png](.img/step07d.png)](#nolink)

_**Figure 7.d.** Summarizing groups into fewer values and variables._

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 8. Experiment

* Play around with the software, make new views.
* Find new data on the internet and learn new ways to use SQL for your workflow.
* If you are an Excel and/or R user, think about how your analysis workflow would be different using SQL.
* Resources:

Description | Link
--- | ---
Sample Data | <a href="https://public.tableau.com/en-us/s/resources?qt-overview_resources=1#qt-overview_resources" target="_blank">https://public.tableau.com/en-us/s/resources?qt-overview_resources=1#qt-overview_resources</a>
Comprehensive Tutorial | <a href="https://www.w3schools.com/sql/" target="_blank">https://www.w3schools.com/sql/</a>
Best Practices | [http://www.dpriver.com/blog/2011/09/27/a-list-of-sql-best-practices/](http://www.dpriver.com/blog/2011/09/27/a-list-of-sql-best-practices/)
More Concepts | [https://javajee.com/basic-sql-concepts](https://javajee.com/basic-sql-concepts)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Epilogue

* Don't be discouraged: Professionals that work with data often spend more time munging/wrangling data than they do performing statistical analyses.
   * You can read about organizing, cleaning, and manipulating data (a.k.a. "munging" or "wrangling") here: [https://en.wikipedia.org/wiki/Data_wrangling](https://en.wikipedia.org/wiki/Data_wrangling)
* _Really, don't be discouraged_: If you are just using SQL as a means to an end, know that there are highly-paid professionals that their primary responsibility is optimizing SQL queries.
   * Check out: [https://www.google.com/search?q=SQL+Query+Optimization+Engineer+Jobs](https://www.google.com/search?q=SQL+Query+Optimization+Engineer+Jobs)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Troubleshooting

* By downloading the "portable" version of SQLite in this tutorial, nothing gets installed on your system.

Task | Link
--- | ---
Installation SQLite Tools for Command Line | [https://www.sqlitetutorial.net/download-install-sqlite/](https://www.sqlitetutorial.net/download-install-sqlite/)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## SQLite vs. other SQL implementations

* The SQL language has multiple implementations (e.g. SQLite, MySQL, MariaDB, etc.)
* There can be many differences between these implementations ranging from capabilities to performance.
* You can read more about the details here: [https://stackoverflow.com/q/1326318](https://stackoverflow.com/q/1326318)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Acknowledgments

1. mtcars data set from R: <a href="https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/mtcars.html" target="_blank">Henderson and Velleman (1981), Building multiple regression models interactively. Biometrics, 37, 391–411.</a>

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2019-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>