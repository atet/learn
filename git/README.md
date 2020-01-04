# [atet](https://github.com/atet) / [learn](https://github.com/atet/learn) / [**_git_**](https://github.com/atet/learn/tree/master/git)

[![.img/logo_git.png](.img/logo_git.png)](#nolink)

# Introduction to Git

**_Git and run_ in 15 minutes**

* This introduction to Git only covers what's absolutely necessary to get you up and running
* You are here because you want to use a [version control system (VCS)](https://git-scm.com/book/en/v2/Getting-Started-About-Version-Control) to help manage your solo and/or team-based projects
* We will use Git graphical user interface (GUI) and GitHub to perform basic operations; advanced material is not covered here

--------------------------------------------------------------------------------------------------

## Table of Contents

### Introduction

* [0. Requirements](#0-requirements)
* [1. Installation](#1-installation)
* [2. New Repository](#2-new-repository)
* [3. Clone Repository](#3-clone-repository)
* [4. Setup Connection](#4-setup-connection)
* [5. Adding Changes](#5-adding-changes)
* [6. Committing Changes](#6-committing-changes)
* [7. Pushing Changes](#7-pushing-changes)
* [8. Typical Workflow](#8-typical-workflow)
* [9. Epilogue](#9-epilogue)

### Supplemental

* [Troubleshooting](#troubleshooting)
* [Additional Tutorials](#additional-tutorials)
* [GitHub vs. Other Git Platforms](#gitHub-vs-other-git-platforms)

--------------------------------------------------------------------------------------------------

## 0. Requirements

* This tutorial was developed on Microsoft Windows 10
* You are using two platforms hand-in-hand:
   * **Git graphical user interface** (GUI) downloaded on your computer
   * **GitHub** website accessed through web browser
* You can also perform this tutorial on MacOS or Linux

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 1. Installation

### 1.1. Git GUI

* We will use Git GUI to interface with GitHub's Website
* Download the "64-bit Git for Windows Portable" version here: [https://github.com/git-for-windows/git/releases/download/v2.23.0.windows.1/PortableGit-2.23.0-64-bit.7z.exe](https://github.com/git-for-windows/git/releases/download/v2.23.0.windows.1/PortableGit-2.23.0-64-bit.7z.exe)
   * Note: This link may break as new versions are released, if so go to: [https://git-scm.com/download/](https://git-scm.com/download/)

[![.img/step01a.png](.img/step01a.png)](#nolink)

* Run the downloaded file and have it extract to your desktop

[![.img/step01b.png](.img/step01b.png)](#nolink)

* Open Windows File Explorer and navigate to where you extracted PortableGit, navigate to "`..\PortableGit\cmd\git-gui.exe`" and run it
* Keep this program up while you move on to the GitHub website

[![.img/step01c.png](.img/step01c.png)](#nolink)

### 1.2. GitHub Website

* You must sign up for a free account with GitHub at [www.github.com](www.github.com) and sign in.

[![.img/step01d.png](.img/step01d.png)](#nolink)

**After downloading and installing Git GUI and registering for a GitHub account, you should be able to setup your Git credentials within the next 5 minutes.**

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------


## 2. New Repository

### 2.1. Create a New Repository on GitHub

* We will create a new **repository** and **initialize** it to begin using the _repos_ (short for repository)
* After you log in, click on the green "New" button:

[![.img/step02a.png](.img/step02a.png)](#nolink)

* Give your repos a name (e.g. "TEST"), click on "Initialize this repository with a README" (this is important), and then click the green "Create repository" button.

[![.img/step02b.png](.img/step02b.png)](#nolink)

### 2.2. Copy Repository Address

* After your new repos is created, click on the green "Clone or download" button on the top right and **copy the information you see here under "Clone with SSH"**, e.g. `git@github.com:atet/TEST.git`

[![.img/step02c.png](.img/step02c.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 3. Clone Repository

* We just created the repository on GitHub's website, let's **clone** that repository so it also exists on your local computer
* Go back to the Git GUI program and select "Clone Existing Repository"

[![.img/step03a.png](.img/step03a.png)](#nolink)

* Paste the information from GitHub to "Source Location", e.g. `git@github.com:atet/TEST.git`
* Choose a "Target Directory" for where the files will go locally, e.g. filepath to your desktop, then **manually add the name of the new folder to be created but does not yet exist**, e.g. "`/TEST`"
   * Git GUI will not let you use a directory that already exists, a new directory must be created here

[![.img/step03b.png](.img/step03b.png)](#nolink)

* Once you click "Clone" button, Git GUI will download the repos you just made on GitHub to your local target directory

[![.img/step03c.png](.img/step03c.png)](#nolink)

* Once the repos is cloned, a copy of your GitHub repos exists locally on your computer
* Below is what your working environment on Git GUI will look like

[![.img/step03d.png](.img/step03d.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 4. Setup Connection

**After cloning your repository, you must set up your Git GUI and GitHub website account to securely communicate with each other**

### 4.1. Setup GitHub Account Credentials in Git GUI

* Go to `Edit` → `Options...`
* On the left-hand side, enter your **GitHub website username and email address** associated with your account
* Click `Save`

[![.img/step04a.png](.img/step04a.png)](#nolink)

### 4.2. Generate Git GUI SSH Key

* Go to `Help` → `Show SSH Key`
* Click on `Generate Key` then `Copy To Clipboard`
   * NOTE: Your key will be a difference sequence of characters than below

[![.img/step04b.png](.img/step04b.png)](#nolink)

### 4.3. Register Git GUI SSH Key with GitHub Account

* Click on the top-right profile picture and select `Settings`
* Click on `SSH and GPG keys` on left-hand side
* Click on green `New SSH key` button on top-right
* Give this new key a `Title`
* Paste your public Git GUI key into the text box
* Click on `Add SSH key`

[![.img/step04c.png](.img/step04c.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 5. `Add`ing changes

**`Add`ing will list out all the changes (new/deleted/modified files) that were made to the local repository**

* Here, we will just make a simple change to the `README.md` file:
   * Navigate to where you cloned the `TEST` repos
   * Right-click and open `README.md` file in Notepad
   * Type out "`HELLO WORLD!`" at the bottom and save

[![.img/step05a.png](.img/step05a.png)](#nolink)

* `Add` these changes to your record of changes:
   * In the Git GUI, click on `Rescan` and our addition of "`HELLO WORLD!`" in the `README.md` file will be shown in the top-right window pane

[![.img/step05b.png](.img/step05b.png)](#nolink)

* Click on `Stage Changed` and the changes you have made will be `add`ed to the list on the bottom-left

[![.img/step05c.png](.img/step05c.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 6. `Commit`ting Changes

**`Commit`ting will organize and document the various changes made as a single group**

* Add a message relating to the changes you just made, e.g. `"Added "HELLO WORLD!" to README.md."`
* Click on `Commit`
* _You will not see any changes on GitHub at this point yet_

[![.img/step06a.png](.img/step06a.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 7. `Push`ing Changes

**`Push`ing will send all commits to be incorporated to the master repository on GitHub**

* Click on `Push` in lower-right window pane
* In the popup window that comes up, click on `Push` again

[![.img/step07a.png](.img/step07a.png)](#nolink)

* Another popup window will display the status of your `push` of local changes to the master on GitHub.
   * If you setup your connection correctly on Step 4, there will not be any errors here
   * Click on `Close`

[![.img/step07b.png](.img/step07b.png)](#nolink)

* You will now see all your `commit`s on GitHub

[![.img/step07c.png](.img/step07c.png)](#nolink)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 8. Typical Workflow

* You can think of each repos as all the content that comprises a single project
* All file additions, modifications, and/or deletions in this project will be tracked
* Identify breakpoints in a project and organize your efforts (and commits) around them:
   * "_Initial commit of project framework including X, Y, and Z._"
   * "_Implemented backend code to allow users to sort GUI results table._"
   * "_Fixed login bug #2 that caused QA's 'Unknown User' error._"
* Once you start getting used to the version control workflow, you'll notice it's mostly just `add` → `commit` → `push`

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## 9. Epilogue

* Anyone can incorporate Git into their development workflow and immediately gain benefits:
   * **Redundancy and Backup**: Copies of your files will exist in multiple locations (on the GitHub platform, your computer, collaborators, etc.)
   * **Versioning**: Revert to any previous version of your repos
* This was a quick introduction, but Git can be more powerful (and complex):
   * **Branching**: Collaborators can work on their own branch without affecting anyone else's and submit changes for review
   * **Command Line Access**: Quickly `add` → `commit` → `push` through a terminal instead of website drag-dropping or GUI button-pushing

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Troubleshooting

Issue | Solution
--- | ---
GitHub won't let me push a large file | GitHub will not allow a single file to be larger than 100 MB unless you enable [LFS](https://git-lfs.github.com/)
I erased a large file but GitHub still thinks it's in my repos | Even if you remove the file, once commited, it exists in your Git history. Follow these instructions to `reset` the `HEAD`: https://stackoverflow.com/a/54846502<br><br>`$ git status`<br>`$ git reset HEAD~<HOWEVER MANY COMMITS YOU ARE AHEAD>`<br>`$ git add . && git commit -m "" && git push -u origin master`


[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## Additional Tutorials

Title | Link
--- | ---
Git Concepts | [https://git-scm.com/book/en/v1/Getting-Started-Git-Basics](https://git-scm.com/book/en/v1/Getting-Started-Git-Basics)
GitHub's Web-GUI Introduction | [https://guides.github.com/activities/hello-world/](https://guides.github.com/activities/hello-world/)
Git Commands Cheat Sheet | [https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf](https://github.github.com/training-kit/downloads/github-git-cheat-sheet.pdf)

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

## GitHub vs. Other Git Platforms

* Git and GitHub are two different systems that work together:
   * GitHub provides the cloud hosting for your repos
   * Git is the language that can communicate with the remote repos
* GitHub is a popular service provider, but there are many others that can be accessed with the same Git workflow:

Company | Service | Website
--- | --- | ---
Microsoft | GitHub | www.github.com
Atlassian | Bitbucket | www.bitbucket.org
GitLab, Inc. | GitLab | www.gitlab.com

[Back to Top](#table-of-contents)

--------------------------------------------------------------------------------------------------

<p align="center">Copyright © 2019-∞ Athit Kao, <a href="http://www.athitkao.com/tos.html" target="_blank">Terms and Conditions</a></p>