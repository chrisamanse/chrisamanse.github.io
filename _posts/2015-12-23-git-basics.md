---
layout: post
title:  "Git Basics"
date:   2015-12-23 23:50:00 +0800
categories: git
excerpt: If you're really serious about software development, you should start learning Git. In fact, you SHOULD know git when you're a software developer.

---

## What is Git?

If you're really serious about software development, you should start learning Git. In fact, you **SHOULD** know git when you're a software developer. Git is a version control system, which means Git allows you to track changes in a project, and revert any changes you made. For example, you've released a version 1.0 of an app. You then made several revisions to its code and have released versions from 1.1, 1.2, up to 2.0. Let's say that you've found out that since version 1.8, the app doesn't work for most of your users, so you want to go back to 1.7 where every user can use the app. Git can let you do that easily, and that is only one of its basic features. Git has a lot of features, but first, let's start with saving "versions" of your project.

## Installation

If you're using Mac OS X, you're in luck, Git is installed by default in your operating system. If you're using other platforms, follow the installation instructions from the [Git website](https://git-scm.com). After you've installed git, open your command line, then run the command `git --version`, and you should see the version number of Git installed in your system.

    $ git --version
    > git version 2.5.4 (Apple Git-61)  

## Create Your Project Folder

Now we'll begin with the fun part! I hope you're comfortable in using the command line because it is where Git is best used. I also highly recommend using Git from the command line when learning Git. You can use a GUI for more complicated tasks which will not be covered in this article.

First, create a folder named "FirstGitProject" and navigate to it in the command line. You can use the command line to create the folder using these commands if you're on OS X or Linux:

    [~]$ mkdir FirstGitProject
    [~]$ cd FirstGitProject/
    
Now, create a file called HelloGit.txt with the contents "My First Git Project". You can also do this in the command line, and just make sure you're in the correct folder: `nano HelloGit.txt`. The nano editor should be displayed in your command line. Now, type in "My First Git Project". To save, use `^X` using your keyboard. If you're on a Mac, `^X` means `control+X`. Then, follow the instructions to save the file. You should now see the file in your folder.

    [~/FirstGitProject/]$ ls
    > HelloGit.txt
    
## Initializing Git

This part is now where you use Git. Run `git init` in your project folder and you should see this:

    $ git init
    > Initialized empty Git repository in /Users/yourusername/FirstGitProject/.git/
    
The full path will be different depending on where your project folder is located. Your Git repository is empty for now, and you'll have to "commit" your changes first to add it to your "changes history", which is sometimes called the Git history. "Committing", on the other hand, means that you save your changes in the Git history so that you can revert to it if needed. You can think of commits as **checkpoints** for your project. **Commits** can be from small to big changes. Usually, you commit when you make some changes in your project, such as adding, modifying, or removing files. Modifications can be a simple edit of a function. You should also add messages to these commits so you would know what you did during that commit.

## Initial Commit

Now that you're repository's initialized (it's still empty - the Git history is empty), you have to make your first commit, which is commonly given the message "Initial commit". Run `git status` in the command line in your project folder. You should see something similar to this:

    > On branch master
    > 
    > Initial commit
    > 
    > Untracked files:
    >   (use "git add <file>..." to include in what will be committed)
    > 
    >         HelloGit.txt
    > 
    > nothing added to commit but untracked files present (use "git add" to track)

You'll see in the first line it says "On branch master". We'll talk about branches later. You'll se that "HelloGit.txt" is "untracked" meaning Git doesn't track the changes in that file yet. To add this, you need to run the command `git add HelloGit.txt`. The format is `git add <filename of the file to track>`. You can easily add all files using a period, ".", in place of the filename: `git add .`.

Now run `git status` again. You'll see that Git now sees the "HelloGit.txt" and is now ready to be committed, i.e. added to the Git history. It is also called the **staging area**. The staging area is the area where Git determines which changes will be part of the next commit.

Let's now make your *INITIAL COMMIT*. Run `git commit -m "Initial commit"`. Next to the "-m" is the message for your commit. Commit messages should be short but descriptive of the changes you made. A summary of the commit will be showed after you run the command. Congratulations! You've now created your first Git repository, and your first commit!

## Second Commit

Let's add more commits in your Git repository. Modify your "HelloGit.txt" file (add a few lines, delete, or do whatever you want with it). Now run `git status` to check if Git sees some changes in your Git repository. If you have modified the file, Git will see the changes:

    > On branch master
    > Changes not staged for commit:
    >   (use "git add <file>..." to update what will be committed)
    >   (use "git checkout -- <file>..." to discard changes in working directory)
    > 
    >         modified:   HelloGit.txt
    > 
    > no changes added to commit (use "git add" and/or "git commit -a")

Git shows you a summary of the changes. In my case, I modified "HelloGit.txt".

> Git can also show you more specific changes such as added or deleted lines by simply running `git diff`.

Also note the output  `git status` - it tells you that the changes are not staged for the next commit. So, if you run `git commit`, it won't include that change in your commit. Run the same steps you did for your initial commit:

    $ git add HelloGit.txt
    $ git commit -m "Add new line in HelloGit.txt"

There you go. You now have two commits in your Git repository. To show a list of your commits, run `git log`.

    > commit 658cc8cbbc453263dbd1d900be3f8252338b98e3
    > Author: Chris Amanse <christopheramanse@gmail.com>
    > Date:   Thu Dec 24 00:09:10 2015 +0800
    > 
    >     Add new line in HelloGit.txt
    > 
    > commit ced39f4c55836be8b3420ec7fcbae92cac02c225
    > Author: Chris Amanse <christopheramanse@gmail.com>
    > Date:   Wed Dec 23 23:43:56 2015 +0800
    > 
    >     Initial commit

## Reset Changes

There are times when you've made lots of changes in your project and wanted to go back before all those changes. With Git, you can finally do that with a single command. Modify your "HelloGit.txt", and run the commands you've learned to check if Git sees those modifications. Now, if you want to reset your project to the latest commit you made, simply run `git reset --hard`. Adding "--hard" after reset means you allow git to modify your project or called working directory. Finally, look at your "HelloGit.txt", and you'll see that the changes you've made are now gone!


## Conclusion and Resources

With just this simple feature, we can see how integrating a version control system, Git specifically, helps the stability of our projects. Some people even use it to track changes in their notes. Tracking and reverting changes is really just one small feature of Git, and it has more powerful features in addition to that. You can learn more about them by using the documentation found in the [Git website](https:git-scm.com). You can also use the [online interactive tutorial](https://try.github.io) by Code School, which takes only a few minutes to learn Git and get to know its best features. 
