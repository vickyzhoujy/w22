---
layout: lab
num: lab04
ready: true
desc: "Counting ducks: File I/O and flow control"
assigned: 2021-10-27 12:00
due: 2021-11-09 23:59:00
---

# What to work on today

Your choice:
* Study for the exam. There are several options here:
  * Go back through zyBook chapters and rework the exercises.  I suggest reverse order: Chapter 7, then 6, etc. since the harder questions are likely to be in the later chapters.  Read Chapter 8 too, even though there are no exercises in it.
  * Go back through the lab02 and lab03 instructions and be sure you are comfortable with the Unix and GitHub steps described there.  If you skimmed over instructions, now go back and read them carefully.  They may be a source of exam questions.
  * Rewatch videos (possibly fast-forwarding through parts that you already understand well.)
* Work on the new zyBook chapter, Chapter 9 about files.  
  * This will not be on the exam, but it is helpful for working on lab04.
  * The due date for Chapter 9 in the zyBook is one week from today (with the grace period extending one week beyond that.)
  * The due date for the lab extends then a couple of days beyond the due date for Chapter 9.
* Jump right in on lab04 (the programming exercise described below).

# Introduction

By the time you have completed this lab, you should be able to:

* Use for loops to count up and count down
* Check command line argument for input filename, and open that input file for reading
* Read every line of text in an input file and process it, using a while loop
* Use if-else statements to select blocks of code
* Count how many times a value occurs in a file
* Use Unix commands to create directories, navigate to directories, list files, and copy files
* Use the "make" command to compile simple stand-alone C++ programs (i.e. single source code file)
* Run simple C++ programs both with and without a single command line parameter


# Helpful background material

You might find it useful to work though Chapter 9 in the zyBook, named "Brief introduction to File I/O" before completing this lab.

The following code from lecture may also help you complete this assignment:

* <https://github.com/ucsb-cs16-f21/lectures/tree/main/10.19/files>

It illustrates some code similar to what you'll need to count things.


## Step 0: Log on to CSIL and bring up a terminal window. 

As a reminder, here's how to get a terminal:

| From | Get a terminal on CSIL by |
|------|---------------------------|
| Machines in Phelps 3525 | Go to the <strong>Application</strong> Menu, then <strong>System Tools</strong>, then <strong>Terminal Window</strong> |
| Windows | Use Powershell, then `ssh username@csil.cs.ucsb.edu` |
| MacOS | Use Terminal, then `ssh username@csil.cs.ucsb.edu` |
| Unix/Linux | Use a terminal shell, then `ssh username@csil.cs.ucsb.edu` |
{:.table .table-sm .table-striped .table-bordered}

## Step 1: Set default git branch

In October 2020, GitHub changed their default branch name from `master` to `main`.   

To configure  `git` for this change, we can run the following command.  We should only need to do it once.

```
git config --global init.defaultBranch main
```

## Step 2: Find your lab04-GITHUBID repo, and clone it into `~/cs16`

* Use `cd` to move into your `~/cs16` directory.
* Find the repo `lab04-GITHUBID` in the GitHub org for this course.
* Copy the ssh URL for that github repo (it should start with `git@github.com`, not `https`) 
* Use `git clone PASTE-SSH-URL-HERE` to clone that repo into your `~/cs16` directory. 
 
  You may see this message; if so, that's normal:
  ```
  warning: You appear to have cloned an empty repository.
  ```
 
* Use `cd lab04-GITHUBID` to move yourself into that directory.


## Step 3: Add a remote for starter code.

While in your `~/cs16/lab04-GITHUBID` directory, type this command:

```
git remote -v
```

The `-v` here stands for `verbose`, and it means that the command will give lots of helpful information. The output should look like this:

```
$ git remote -v
origin	git@github.com:ucsb-cs16-f21/lab04-GITHUBID.git (fetch)
origin	git@github.com:ucsb-cs16-f21/lab04-GITHUBID.git (push)
$ 
```

Explanation:
* The word *remote* refers here to a Git repo that lives on some other computer; in this case, a GitHub.com server. 
* The output above shows that you have one *remote* called `origin` and it shows the URL associated with that name `origin`.  
* By convention, the name `origin` is used for the GitHub repo from which you cloned the current repo, i.e. the one that came after `git clone` in a previous step.

What we are doing to do next is add a second remote, called `starter`.  From this remote, you'll be able to pull in some starter code; your lab solution will involve
working with some of that starter code.

The starter code lives in this repo, which you can visit in a web browser to look at the starter code:
* <https://github.com/ucsb-cs16-f21/STARTER-lab04>

To add a remote for this repo, we'll use the ssh url, like this:

```
git remote add starter git@github.com:ucsb-cs16-f21/STARTER-lab04.git
```

To see if it worked, you can type the `git remote -v` command again. Output should look like this (with YOUR-GITHUB-ID replaced by your github id. 

```
$ git remote -v
origin	git@github.com:ucsb-cs16-f21/lab04-GITHUBID.git (fetch)
origin	git@github.com:ucsb-cs16-f21/lab04-GITHUBID.git (push)
starter	git@github.com:ucsb-cs16-f21/STARTER-lab04.git (fetch)
starter	git@github.com:ucsb-cs16-f21/STARTER-lab04.git (push)
$ 
```

Note that if the URLs are wrong for either the `origin` or the `starter` remotes, you can fix that by doing this command to remove a remote:
* `git remote remove origin` to remove the remote `origin`
* `git remote remove starter` to remove the remote `starter`

Then you can add the remote back with the correct URL, e.g.:
* `git remote add origin git@github.com:ucsb-cs16-f21/lab04-GITHUBID.git`
* `git remote add starter git@github.com:ucsb-cs16-f21/STARTER-lab04.git`

This can be used, for example, if you accidently cloned the repo using the `https` url instead of the one that starts with `git@github.com` (which is the SSH based URL).

Assuming your remote for `starter` is now set up correctly, the next step is to pull in the starter code.

## Step 4: Pull in Starter Code

To pull in the starter code, use:

```
git pull starter main
```

Then use an `ls` command, and you should see new files in your directory.  That should look something like this:

```
$ ls
$ git pull starter main
remote: Enumerating objects: 10, done.
remote: Counting objects: 100% (10/10), done.
remote: Compressing objects: 100% (7/7), done.
remote: Total 10 (delta 2), reused 7 (delta 2), pack-reused 0
Unpacking objects: 100% (10/10), 2.45 KiB | 47.00 KiB/s, done.
From github.com:ucsb-cs16-f21/STARTER-lab04
 * branch            main       -> FETCH_HEAD
 * [new branch]      main       -> starter/main
$ ls
README.md animals01.txt  animals02.txt  countDucks.cpp  sample01.cpp
$ 
```

With these files in place, you are ready to start coding.

If you don't see those files, go back through the instructions and make sure you didn't miss a step.


## Step 5: Compile and run the first program for this assignment 

The first program we are going to compile and run is one that demonstrates a for loop in C++.   

In your `lab04-GITHUBID` directory, you should have a program called `sample01.cpp` that we copied in the previous step. Here's how you can put yourself in that directory (though you should already be there):

```
-bash-4.2$ cd ~/cs16/lab04-jgaucho
-bash-4.2$ pwd
/cs/faculty/richert/cs16/lab04-jgaucho
-bash-4.2$
```

Then you can list out your files with the <code>ls</code> command:

```
-bash-4.2$ ls
animals01.txt  animals02.txt  countDucks.cpp  sample01.cpp
-bash-4.2$
```

Finally, use the Unix <code>cat</code> command to list the contents of the file sample01.cpp. (The reason this command is called "cat" has nothing to do with the animal that goes "meow". If you ask me in lecture and I'll tell you where the name comes from).

```
-bash-4.2$ cat sample01.cpp
// sample01.cpp
#include <iostream>
using namespace std;
 
int main() {
    // Simple for loop that counts from 1 up to n
 
    int n=5;
 
    for (int i=1; i<=n; i++) {
       cout << "i=" << i << endl;
    }
 
    return 0;
}
-bash-4.2$
```

Compile this with the command <code>make sample01</code> and run it with the command <code>./sample01</code>.  That looks like this:

```
-bash-4.2$ make sample01
g++     sample01.cpp   -o sample01
-bash-4.2$ ./sample01
i=1
i=2
i=3
i=4
i=5
-bash-4.2$
```

If you get that output, you are ready for the next step.

## Step 6: Copy sample01.cpp to myProg01.cpp and make changes 

Now we'll use the the Unix command <code>cp </code><em>oldfile newfile</em> which copies files, to copy from sample01.cpp to a new file called myProg01.cpp, as shown here:

```
-bash-4.2$ cp sample01.cpp myProg01.cpp
-bash-4.2$ ls
animals01.txt  countDucks.cpp  sample01
animals02.txt  myProg01.cpp    sample01.cpp
-bash-4.2$
```

Now you have a new file called myProg01.cpp that is a copy of sample01.cpp. Open it up in a text editor and make the following changes:

1. Change the comment at the top of the file so that it says // myProg01.cpp
2. Change the second line of the file to be of the format "Author: your name"
3. Change the comment within the code to "Simple that counts down from n to 1"

4. Change the for loop as follows:

  * Instead of initializing to 1, initialize to n
  * Instead of testing <code>i&lt;=n</code>, test whether <code>i&gt;0</code>
  * Instead of changing i by incrementing with <code>i++</code>, change it by decrementing with <code>i--</code>
  * Remove the printing of "i=" each time.  Instead just print the number. And Instead of printing a newline after each number, just print one space.  We do that by changing <code>cout &lt;&lt; "i=" &lt;&lt; i &lt;&lt; endl;</code> to <code> cout &lt;&lt; i &lt;&lt; " ";</code>
  * Add a line that prints a newline at the very end, just after the for loop is over, but BEFORE the <code>return 0;</code> statement.

Compile and run myProg01.cpp with these changes. The output should look like this:

<pre>
5 4 3 2 1
</pre>

You are now ready to move to the next step.   

Tip: *If you make a mistake that results in an "infinite loop", i.e. the window is just scrolling by without stopping, you can use CTRL+C (hold down Control and type C) to stop the program.*

## Step 7: Reading from input files and counting ducks 

The next files we are going to look at are not C++ code, but rather data files.

Use the "cat" command to look at the contents of animals01.txt and animals02.txt. You should get results like these:

```
-bash-4.2$ cat animals01.txt
duck
duck
goose
-bash-4.2$ cat animals02.txt
duck
duck
goose
duck
duck
cow
duck
duck
dog
-bash-4.2$
```

The next program we are going to look at will read input from files such as these. It is called <code>countDucks.cpp</code> and it will simply count the number of ducks in each file.

Before you look at the code, try compiling the program and running it, because this will help you understand what the program is trying to do.  Compile with:

```
-bash-4.2$ make countDucks
g++     countDucks.cpp   -o countDucks
-bash-4.2$
```

Then try running it with just <code>./countDucks</code>.  You'll see that you get a "Usage" message.  This is telling us that the program expects a "command line argument", which is the name of the file to read:

```
-bash-4.2$ ./countDucks
Usage: ./countDucks inputFile
-bash-4.2$
```

In the file `countDucks.cpp` make modifications so that when you run the program with argument `animals01.txt` as the filename, 
it produces the following output:

```
-bash-4.2$ ./countDucks animals01.txt
There were 2 ducks in animals01.txt

```

Alternatively if you give `animals02.txt` as the argument it should produce the following output.
```
-bash-4.2$ ./countDucks animals02.txt
There were 6 ducks in animals02.txt
-bash-4.2$
```

Note that this isn't just an `if` statement that checks whether the filename is `animals01.txt1` or `animals02.txt`; you actually need to 
open the file and count the number of times that `duck` appears on a line.   When we test your program, we'll test it on other input files
too.

Once you've done that, you are ready for the next step.

## Step 8: A more detailed counting program 

Your job is now to copy `countDucks.cpp` to a file `myProg02.cpp` and make some changes.

First, let's stipulate that you may assume that everything in the input file is an animal, one per line&mdash;if someone adds "potato" or "bicycle" to the file, you can just assume that potato and bicycle are now to be considered types of animals.

1. Add a variable that will count ALL animals in the file. Give it an appropriate name and initialize it to zero.
2. Add a variable that will count ALL animals in the file that are NOT ducks.   Give it an appropriate name and initialize it to zero.
3. Add code that will increment those counts when appropriate. It may help to know that C++ has an else clause for an if that looks like this:

```
   if (condition) {
     // lines of code here are
     // executed when condition is true
   } else {
     // lines of code here are
     // executed when condition is false
   }
```

Note that it is NOT required for every if statement to have an else clause.

Also note that the braces <code>{ } </code> are:

* OPTIONAL when there is a SINGLE statement inside a particular if or else block
* REQUIRED when there is more than one statement inside a particular if or else block

After making these changes, one more thing: change the lines that give the output so they look like the ones shown below.

<pre>
Report for animals01.txt:
   Animal count:    3
   Duck count:      2
   Non duck count:  1
</pre>

<pre>
Report for animals02.txt:
   Animal count:    9
   Duck count:      6
   Non duck count:  3
</pre>

It is IMPORTANT to be EXACT since the Gradescope system will compare your output with the expected output character-by-character. The spacing MATTERS! You can add extra spaces at the beginning and end of the string literals for <code>"   Animal count:   "</code>  and <code>"   Duck count:   "</code> so that the spacing comes out right and matches the expected output below. I'm not going to tell you how many; you'll have to figure that out.

Note that we will also test your program on other input files, so you should too. Use the cp command to copy animals02.txt to animals03.txt and add some ducks and some other animals. Count by hand, and make sure that the count when you run your program matches what is expected.

When you are satisfied that the count is correct and that format of the output is precise, you are ready to submit your code for grading.

## Step 9: Push your changes to GitHub

You don't have to wait until you are completely finished with your code to push your changes to GitHub.  You can do it at any time during the assignment.  In fact, each time you complete part of an assignment, or are finished for the day, that's a really good time to update GitHub with the changes to your code.

You can see which files are "out of date" with GitHub by typing the command:

```
git status
```

Files that show up in red are files that have been updated or created since the last time GitHub was updated.  For each of these, you can use
a `git add filename` command to add them to the next commit, e.g.

```
git add countDucks.cpp
git add myProg02.cpp
```

You can also add all files ending in `.cpp` like this:

```
git add *.cpp
```

Type `git status` again to see the files that will be added to the next commit.

Then, you can type this, substituting an appropriate message.  Be sure your message has `""` around it.

```
git commit -m "half way done with lab04, but stuck on loop in myProg02.cpp`
```

or

```
git commit -m "finished with lab04, going to test on Gradescope"
```

This makes a commit, but *only on your local machine* (CSIL if you are working there.)

To update the files on github.com, use this:

```
git push origin main
```

Go to: <https://github.com/ucsb-cs16-f21>, find your `lab04-GITHUBID` repo, and make sure that the changes are there.  You should see your commit message beside the file that are changed.

Then you should be able to submit to Gradescope.

## Step 10: Submit to Gradescope

Once you are satisfied that your program is correct, then it's time to submit it.

Log into your account on [https://www.gradescope.com/](https://www.gradescope.com/) and navigate to our course site: CMPSC 16.  Select this assignment. 

Then click on the "Submit" button on the bottom right corner to make a submission. You will be given the option of uploading files from GitHub.

You should receive 100/100 for a set of completely correct programs, and partial credit if one or two of the three is correct.

Note that if the assignment requires more than one program, and you are looking for partial credit, you need to at least submit a minimal "empty" main program
for the  `.cpp` files that are required, but not yet complete.  Here is what an "empty main" looks like:

```cpp
int main() {
  return 0;
}
```

If any errors are shown, you can address that with this sequence of steps:
* Go back to edit the file with `vim filename.cpp` and make the needed changes
* Recompile with `make filename`
* Test interactively by running `./filename` 
* Use this sequence of steps to update GitHub:
  * `git add filename.cpp`
  * `git commit -m "message goes here explaining what you did"` 
  * `git push origin main`
* Resubmit on Gradescope from your GitHub repo.


## Style Guidelines


1. Indentation is neat, consistent and follows good practice (see below)
2. Variable name choice: variables should have sensible names.
	More on indentation: Your code should be indented neatly. Code that is inside braces should be indented, and code that is at the same "level" of nesting inside braces should be indented in a consistent way. Follow the examples from lecture, the sample code, and from the textbook.   
