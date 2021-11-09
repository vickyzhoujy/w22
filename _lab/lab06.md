---
layout: lab
num: lab06
ready: false
desc: "Fun with shapes: Pointers and Structs"
assigned: 2021-11-10 12:00
due: 2021-11-19 23:59:00
---

# NOT READY YET
# NOT READY YET
# NOT READY YET
# NOT READY YET
# NOT READY YET
# NOT READY YET


# Goals of this lab

The goal of this lab is to demonstrate how we can abstract "things" in the world
(such as geometric objects) into program contructs. 
We also hope that you will get a lot more practice with using pointers, 
passing pointers to functions and using pointers along with structs. Y

You will continue to use the test-driven development (TDD) process to develop high quality and well-tested code in a systematic manner.
When you run into problems with your code, remember to use the skills we have been 
learning such as code tracing and drawing pointer diagrams, 
to understand the dynamics of your program and how it is interacting with memory.

# Step by Step Instructions

## Step 1: Getting Ready

1. Go to github and find a repo for lab06 assigned to your GitHub id.

2. Log on to your CSIL account.

3. Change into your `~/cs16` directory

4. Clone your empty lab06 repo into your `~/cs16` directory.

5. In your empty repo, do `git checkout -b main` to establish that you are on the `main` branch as your default branch.


## Step 2: Obtain the starter code

The starter code is in this repo:

* <https://github.com/ucsb-cs16-f21/STARTER-lab06>

The URL for cloning this repo is this: `git@github.com:ucsb-cs16-f21/STARTER-lab06.git`

Previous labs contain instruction for the process of:
* Adding a `starter` remote for this repo
* Pulling the code from that `starter` remote into your own repo.

Please do those steps now, and then do a `git push origin main` to populate your own repo with the starter code.

If you need help with these steps:
* First consult previous labs for more detailed instructions.   
* Then, if you are still having trouble, ask the staff for help during discussion section or office hours.

Once you've populated your repo, typing the `ls` command should show you the following files in your current directory

```
$ ls
Makefile			pointsApproxEqualTest.cpp
README.md			shapeFuncs.cpp
areaOfBoxTest.cpp		shapeFuncs.h
boxesApproxEqualTest.cpp	shapes.h
distanceBetweenTest.cpp		tddFuncs.cpp
initBoxTest.cpp			tddFuncs.h
initPointTest.cpp		utility.cpp
pointToStringTest.cpp		utility.h
$ 
```

## Step 3: Reviewing the files and what your tasks are

Here is a brief description of each of the files and expected implementation. 

Note that some of the files are organized in pairs of matching `.h`/`.cpp` files:
* These include:
  - `shapeFuncs.h`/`shapeFuncs.cpp`
  - `tddFuncs.h`/`tddFuncs.cpp`
  - `utililty.h`/`utility.cpp`
* In these cases, the `.h` file has function *declarations* (also known as function *prototypes*) and the `.cpp` file has the function *definitions*.
* Knowing about this separation is important.  Look over the contents of some of the `.h` files and `.cpp` files that are in pairs like this.
* Be sure, for future exams/homework, that you can identify whether some arbitrary C++ code looks more like it would appear in a `.h` or a `.cpp` file.
* Also be sure that you know how to spot the difference between function *declarations* (aka *prototypes*), and function *definitions*.

The `shapes.h` file is different; it isn't paired with any `.cpp` file.  That's because it contains `struct` declarations used in the other files.

Finally, there are also a variety of `.cpp` files that have the suffix `Test` in their names.   Each of these contains a `main` function, and code that runs our
tests.  These are the same tests that run on Gradescope.

Here's an overview of all of the files and their purpose:

* utility.h/cpp : Implement any of your own functions that you will need to solve the problems in this lab
* tddFuncs.h/cpp : Functions that you may use to test your code
* shapes.h : Contains the declaration of two structs: Point and Box. These data structures will be used in other files e.g. shapeFuncs.h/cpp
* shapeFuncs.h/cpp : Functions to compute metrics on geometric constructs such as points and boxes (see shapes.h)
* *Test.cpp: Each of the files that end in Test.cpp contain code to test a particular function in shapeFuncs.cpp. 


Here are some further notes about the files that end in `Test.cpp`:

* As an example,  `distanceBetweenTest.cpp` contains test code to test your implementation of the `distanceBetween()` function in `shapeFuncs.cpp`. 
* Note that each `*Test.cpp` file tests contains a main function, which means that each test file along with its  dependent code is meant to be compiled into a separate executable. 
* The provided `Makefile` makes sure that this is in fact the case. 

The rationale behind this approach is that each function in `shapeFuncs.cpp` can be developed and tested independently as much as possible.

## Tasks for this lab

Here is a list of your tasks for this lab.  You will see that we are working on one function at a time, seeing the tests fail, then editing code to see the tests pass.

### Get `distanceBetween` working

* Run `make` and see the given code being compiled.
* Run `./distanceBetweenTest` and see it fail.
* Edit the `distanceBetween` function in `shapeFuncs.cpp` to replace with correct code.
* Run `./distanceBetweenTest` and see it pass.
* Commit and push your code to github with commands:
  - `git status` to see which files have been changed and need to be added.
  - `git add shapeFuncs.cpp` (which is likely the only file you have changed)
  - `git commit -m "distanceBetween function is now passing tests"`  (the exact comment is up to you; this is a suggestion)
  - `git push origin main`


### Understand the `pointsApproxEqual` function

* Run ./pointsApproxEqualTest and see it pass.
* Look at the code in pointsApproxEqualTest.cpp and shapeFuncs.cpp and understand how it works.
* Notice how the pointsApproxEqual() function uses the distanceBetween() function that you just wrote and tested, rather than writing new code within pointsApproxEqual() that repeats the logic of distanceBetween(). 
* The takeaway here is that you want to keep your code as DRY as possible (DRY==Don't Repeat Yourself). 
* You also want to only reuse code that has already been tested. 
* You'll need to understand pointsApproxEqual() to get ./boxesApproxEqual to pass.

There is no code to commit for this step; this is just a step for you to read some code and understand it.

### Get `distanceBetween` working


* Run `./initPointTest` and see it fail.
* Looking at the test code in `initPointTest.cpp`, figure out what the `initPoint` function is supposed to do.
* Edit the `initPoint` function in `shapeFuncs.cpp` to replace the stub with correct code.
* Run `./initPointTest` and see it pass.
* Now, as preparation for homework and exam questions, reason about why your code works. Do this by drawing a pointer diagram that shows the state of memory right before the `initPoint` function returns when it is called for the very first time by the test code. Your pointer diagram should show the value of member variables `x` and `y` of the struct object `p1` in `initPointTest.cpp` 
  as well as the relationship between `p1` and the formal parameter `p` of the function `initPoint`. 
* You should also show the formal parameters `xVal` and `yVal` in memory and indicate whether or not they are colocated in memory with any other variables (such as `x` and `y`). 
* Make the drawing on a piece of paper or as ascii art in a text file and upload it to your gitrepo with the filename: pointer-diagram-initPoint. The diagram will be graded manually by us.

* Run ./boxesApproxEqualTest and see it fail.
* Edit the boxesApproxEqual function in shapeFuncs.cpp to replace the stub with correct code.  As you do, consider adding an approxEqual function that takes two double values into utility.h and utility.cpp, as this will make your coding job easier, and keep you code "DRYer".  Also, consider reusing the pointsApproxEqual function in your boxesApproxEqual solution.  Remember that the <code>&amp;&amp;</code> operator is the symbol for "logical and" in C++.
* Run ./boxesApproxEqualTest and see it pass.
* Reason about why your code worked, draw a diagram to show the relationship between the formal and actual parameters. You don't need to submit the diagram but you may be asked to draw such a diagram on an exam!
* Commit and push your code to github.

* Run ./initBoxTest and see it fail
* Edit the initBox function in shapeFuncs.cpp to replace with correct code. As you do, remember that you use -> to access members of a struct through a pointer, but simply . to access members of a struct directly.  You may need both in your answer.
* Run ./initBoxTest and see it pass
* Commit and push your code to github.


* Run ./areaOfBoxTest and see it fail
* Edit the areaOfBox function in shapeFuncs.cpp to replace with correct code.
* Run ./areaOfBoxTest and see it pass
* Commit and push your code to github.


* Run ./pointToStringTest and see it pass
* Copy pointToStringTest.cpp to boxToStringTest.cpp and make tests for the boxToString function.  Look in shapeFuncs.cpp at the boxToString function stub for an example of the format you need for boxToString's return values. Make tests for different precisions, just like pointToString has.
* Add code to the Makefile so that boxToString runs. Just follow the model--adding code for boxToStringTest everywhere you see code for pointToStringTest
* Run make
* Commit and push your code to github.


* Run ./boxToStringTest and see the tests fail
* Fix the definition of boxToString in shapeFuncs.cpp
* See the test ./boxToStringTest pass
* Commit and push your code to github.

* YOU ARE READY TO CHECK YOUR WORK.

## Step 4: Checking your work before submitting

When you are finished, you should be able to type <code>make clean</code> and then <code>make tests</code> and see the following output:

```
-bash-4.2$ make clean
/bin/rm -f distanceBetweenTest initPointTest pointsApproxEqualTest boxesApproxEqualTest initBoxTest areaOfBoxTest pointToStringTest *.o
-bash-4.2$ make tests
g++ -Wall -Wno-uninitialized   -c -o distanceBetweenTest.o distanceBetweenTest.cpp
g++ -Wall -Wno-uninitialized   -c -o tddFuncs.o tddFuncs.cpp
g++ -Wall -Wno-uninitialized   -c -o utility.o utility.cpp
g++ -Wall -Wno-uninitialized   -c -o shapeFuncs.o shapeFuncs.cpp
g++ -Wall -Wno-uninitialized  distanceBetweenTest.o tddFuncs.o utility.o shapeFuncs.o -o distanceBetweenTest
g++ -Wall -Wno-uninitialized   -c -o initPointTest.o initPointTest.cpp
g++ -Wall -Wno-uninitialized  initPointTest.o tddFuncs.o utility.o shapeFuncs.o -o initPointTest
g++ -Wall -Wno-uninitialized   -c -o pointsApproxEqualTest.o pointsApproxEqualTest.cpp
g++ -Wall -Wno-uninitialized  pointsApproxEqualTest.o tddFuncs.o utility.o shapeFuncs.o -o pointsApproxEqualTest
g++ -Wall -Wno-uninitialized   -c -o boxesApproxEqualTest.o boxesApproxEqualTest.cpp
g++ -Wall -Wno-uninitialized  boxesApproxEqualTest.o tddFuncs.o utility.o shapeFuncs.o -o boxesApproxEqualTest
g++ -Wall -Wno-uninitialized   -c -o initBoxTest.o initBoxTest.cpp
g++ -Wall -Wno-uninitialized  initBoxTest.o tddFuncs.o utility.o shapeFuncs.o -o initBoxTest
g++ -Wall -Wno-uninitialized   -c -o areaOfBoxTest.o areaOfBoxTest.cpp
g++ -Wall -Wno-uninitialized  areaOfBoxTest.o tddFuncs.o utility.o shapeFuncs.o -o areaOfBoxTest
g++ -Wall -Wno-uninitialized   -c -o pointToStringTest.o pointToStringTest.cpp
g++ -Wall -Wno-uninitialized  pointToStringTest.o tddFuncs.o utility.o shapeFuncs.o -o pointToStringTest
./distanceBetweenTest
PASSED: distanceBetween(p1,p2)
PASSED: distanceBetween(p2,p1)
PASSED: distanceBetween(p3,p4)
PASSED: distanceBetween(p4,p5)
PASSED: distanceBetween(p5,p3)
./initPointTest
PASSED: pointsApproxEqual(p1,p1Expected)
PASSED: pointsApproxEqual(p2,p2Expected)
PASSED: pointsApproxEqual(p3,p3Expected)
PASSED: pointsApproxEqual(p4,p4Expected)
./pointsApproxEqualTest
PASSED: pointsApproxEqual(p1,p1)
PASSED: pointsApproxEqual(p1,p2)
PASSED: assertFalse(pointsApproxEqual(p2,p1)
./boxesApproxEqualTest
PASSED: boxesApproxEqual(b0,b0)
PASSED: boxesApproxEqual(b1,b0)
PASSED: boxesApproxEqual(b0,b1)
PASSED: boxesApproxEqual(b0,b2)
PASSED: boxesApproxEqual(b0,b3)
PASSED: boxesApproxEqual(b0,b4)
PASSED: boxesApproxEqual(b5,b6)
PASSED: boxesApproxEqual(b6,b5)
./initBoxTest
PASSED: boxesApproxEqual(b1,b1Expected)
PASSED: boxesApproxEqual(b2,b2Expected)
PASSED: boxesApproxEqual(b1,b2)
./areaOfBoxTest
PASSED: areaOfBox(r)
PASSED: areaOfBox(s)
PASSED: areaOfBox(t)
PASSED: areaOfBox(u)
./pointToStringTest
PASSED: pointToString(p1)
PASSED: pointToString(p2)
PASSED: pointToString(p2,1)
PASSED: pointToString(p2,4)
PASSED: pointToString(p2,5)
-bash-4.2$
```

Plus, some output at the end with the output of your boxToStringTest

```
./boxToStringTest
PASSED: boxToString(b1,1)
PASSED: boxToString(b1,2)
PASSED: boxToString(b1,3)
PASSED: boxToString(b1,4)
PASSED: boxToString(b1,5)
PASSED: boxToString(b1,6)
-bash-4.2$
```

At that point, you are ready to try submitting on Gradescope.

## Step 5: Turn in your code on Gradescope

Submit all the .cpp and .h files to Lab05 assignment on Gradescope via your github repo. Then visit Gradescope and check that you have a correct score.

* You must check that you have followed these style guidelines:

1. Indentation is neat, consistent and follows good practice (see below)
2. Variable name choice: variables should have sensible names.
	More on indentation: Your code should be indented neatly.  Code that is inside braces should be indented, and code that is at the same "level" of nesting inside braces should be indented in a consistent way.    Follow the examples from lecture, the sample code, and from the textbook.   

* Your submission should be on-time. If you miss the deadline, you are subject to getting a zero.

Commit and push the latest version of your code on github

If you are logged in remotely, you can log out using the exit command:

```
$ exit
```
