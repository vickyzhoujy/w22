---
desc: "Finish H04 if not done, verify CSIL Account, then zyBooks"
assigned: 2021-10-06 13:00
due: 2021-10-12 21:00
layout: lab
num: lab01
ready: true
---

# What we are working on today

* If you haven't completed [h04](https://ucsb-cs16.github.io/f21/hwk/h04/), enrolling in the GitHub organization, please start by doing that.
* If you want to do the extra credit, and you haven't done that yet, please do that next: [ec00](https://ucsb-cs16.github.io/f21/hwk/ec00/)
* Then, please try your CSIL/ECI account if you haven't already 
  * If you already logged in to any of the desktop machines in Phelps 3525, you've already verified that your CSIL/ECI account works.
  * If you haven't, try the commands in the section `CSIL/ECI Account` below.  
  * This is preparation for next week's lab.
* Then you have a choice between a two activities:
  * Getting a head start on next week's lab by:
    * Learning some basic vim commands by playing this game: <https://vim-adventures.com/>
    * Then trying your hand at creating and compiling a "Hello World" program on your CSIL/ECI account.
  * Or: just continue working in the zyBook where you left off.
* If the TAs/LAs are not busy helping students with CS16 questions, you may also just ask your TAs/LAs general questions about the course, about Computer Science, and about UCSB; but please give priority to students with questions about CMPSC 16 material.

# CSIL/ECI Account

If you are using the desktop machines in Phelps 3525, you are already using your CSIL/ECI account; a terminal window there is a "CSIL/ECI account shell prompt".

Otherwise:
* On Windows, you can use Powershell
* On MacOS, use Terminal
* On a Linux system, use any terminal prompt
* For other systems, e.g. ChromeOS, ask a staff member for help in finding an ssh option for your platform.

At the command prompt, type the following, substituting your ECI/CSIL account in place of `username`

```
ssh username@csil.cs.ucsb.edu
```

The first time you connect, you may be presented with a one type prompt saying that the "credentials could not be verified", and asking a Yes/No question. Say "Yes".

Then, you are in.  You can use `pwd` and `ls` commands as shown in lecture, plus other Unix commands such as `vim` and `make`.

The command `logout` or `exit` can be used to return to your own system.

# Editing and compiling a Hello World program on ECI/CSIL

First, learn about vim, perhaps using one of these resources:

* <https://vim-adventures.com/> Learn vim while playing a game in your browser
* Intro articles about vim:
  * vim overview: <https://ucsb-cs16.github.io/topics/vim/>
  * vim basic eight commands: <https://ucsb-cs16.github.io/topics/vim_basic_eight/>
  * vim customization: <https://ucsb-cs16.github.io/topics/vim_customization/>

Then, to create a `Hello World` program in vim:

1. Type `vim hello.cpp`
2. Make sure you are in insert mode (you'll learn about that when you learn about vim)
3. Type in your program, e.g.
   ```cpp
   #include <iostream>
   using namespace std;
   
   int main() {
     cout << "Hello, World!" << endl;
     return 0;
   }
   ```
4. Press the escape key, then type `:wq` to save.
5. To compile the program: `make hello`
6. To run the program `./hello`

There is nothing to turn in *this* week, but next week, you'll be asked to show that you know how to do this with a live demo either during office hours, or during your discussion section.  So, practicing this week is good preparation.

# Will we always use vim? No!

We will pivot to using a better editor, VS Code, once we understand the basics of using `vim`.  However, we want to start with `vim`, because it is an essential skill for computing professionals, especially if you will be involved in Cloud Computing systems, backend web servers, Docker containers, etc.

# What if I'm completely stuck on this vim / ECI stuff?

No worries; you can ask the staff for help.  In the meantime, if you prefer, you can just make progress in the zyBook, up through Chapter 7.

# For TAs:

You can basically adapt the outline from the TA instructions from lab00, leaving out the detailed introductions of staff; please do, however, still briefly introduce each staff member for at least the first 2-3 weeks.

