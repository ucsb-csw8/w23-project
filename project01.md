---
layout: default
title: Step 1 - Overview
link_to_shared_gradescope_for_final_project: https://www.gradescope.com/courses/518308
---

# {{page.title}}

In this project, you are asked to create a **Restaurant Menu Management System**, which can help with managing a database containing a restaurants menu items (i.e. the food and beverage items that would appears on their printed menu, or a display menu on a computer monitor, for example.)

The due dates and intermediate checkpoints are listed below.

**START WORKING ON THIS PROJECT RIGHT AWAY to give yourselves adequate time to get all of it done. The deadlines are not flexible and we will not accept any late submissions.**

# Table of Contents
1. [Instructions about Academic Honesty](#academichonesty)
1. [Submission to Gradescope](#gradescope)
1. [Due Dates](#dates)
1. [Late Submissions](#latesub)
1. [Project requirements](#reqs)
1. [Grading](#grading)
1. [Workflow Recommendations](#workflow)
1. [Submission checklist](#checklist)
1. [Asking for help](#help)
1. [Updates](#updates)

-----

# Instructions about Academic Honesty <a name="academichonesty"></a>

This project is supposed to be your **own individual work**. This project is open book, open notes, however, you are not allowed to ask others for help with coding (in-person or virtually) or look things up in sources other than the zyBook and the course lecture notes.  Doing so constitutes an academic integrity violation. A violation of academic integrity on the final project can result in getting an **F** in the **entire course**, since it puts into question your work throughout the quarter.

We will run an automatic similarity check, which is not easily fooled by the variable / whitespace changes or other modifications.

## Using advanced Python concepts

You **MAY NOT USE**  material or techniques that we haven't covered in this course, either in the zyBook or in lecture, without *express advance permission* from the course staff.   If you do, you are subject to a grade of **FAIL** for the project.

Here's why: when very advanced Python concepts show up in your code, it's often an indication that you got a solution to a problem from an online source rather than solving it yourself.

If you are unsure about a specific , please check in via private post on Piazza.  

## Academic Integrity Reporting

All students involved in an academic integrity incident, regardless if they are copying or sharing their work, are going to be reported to The Office of Student Conduct, and get an **F** grade in the course.

Please complete **your own work** (without using resources other than your own knowledge) and keep it to yourself. You should not share your code or answers directly with other students.


> By submitting your final project work, _you are asserting that **all work on this project is yours alone**_, and that you will not provide any information to anyone else doing the project, nor will you solicit help from anyone in the class or on the internet. In addition, you are agreeing that you will not discuss any part of the solutions for this project with anyone. This includes discussing the solutions with others after you finish this course or posting any information about this project on any site on the internet. Doing so constitutes a violation of the academic integrity agreement for this course, which can lead to getting an **F** in the course. We reserve the right to change the grade retroactively, even after the final grades have been posted.

-----

# Submissions to Gradescope <a name="gradescope"></a>

## Required files

You will not need to submit anything on zyBooks. You will need to submit three (3) Python files to Gradescope:

* `functions.py`
* `main.py`
* `tests.py`

Each of these is explained below.

**Important**: The files need to be in the _same folder_ on your computer. The import statements in your code will not work correctly, if the files are in different locations on your hard drive.

**File 1 - all your functions**
Create a file called **`functions.py`** in which you will assemble all the relevant functions.

You do not need to use `if __name__ == 'main'` in _any_ of your files, because we can import your functions as shown below.

At the start of the _other two files_, you will need to import the function file you wrote as follows (`functions` is the name of our Python file/module; the asterisk `*` means "all/everything"):

**`from functions import *`**

Again, all this project's functions will need to be implemented and added to this file.


**File 2 - the main program**
Create a new file **`main.py,`** which will contain your main program. As you will place all function definitions in the `functions.py`, you can import them here, as per the above import statement.

**File 3 - test code**
Create a separate file to test your work. Call it **`tests.py`** - this is where the `assert` statements will be collected to help you verify that your implementation of each function is correct.

**Important**: you need to run this file separately: running the main program will not execute the assert statements.
Each function that returns values will need to have the corresponding assert statements to check its correctness.

If the assert statements are failing, then the autograder on Gradescope will surely fail as well.

If you are getting an `AssertionError`, then fix the corresponding function - do not modify the `assert` test to pass, fix the code instead.

Write your own `assert` statements to make sure to test all edge cases specified in the instructions: the autograder will be verifying that those work correctly.

**You will need to submit all files at the same time to Gradescope (again, not in zyBooks).**

## Uploading / backing up to Gradescope

When submitting to Gradescope, you'll be submitting to a *different course* than what you've been using throughout the quarter. 

It looks like the screenshot below, and is at this url: <{{page.link_to_shared_gradescope_for_final_project}}>

<img width="353" alt="image" src="https://user-images.githubusercontent.com/1119017/223179642-a474760c-f640-45f5-926f-bb3b7a0f23a2.png">

There are **required Checkpoint submissions**, which are described below. EVERYTHING is submitted via Gradescope (NOT zyBooks).

The project will be automatically graded for some functions, and manually graded for functionality and style in Gradescope. Upload the files to Gradescope all at once to the correct assignment.

When submitting on Gradescope, remember that you can either navigate to your file or "drag-and-drop" them into the "Submit Programming Assignment" window. If you already submitted something on Gradescope, it will take you to their "Autograder Results" page. There is a "Resubmit" button on the bottom right that will allow you to update the files for your submission.
_You can re-submit your work as many times as you would like until the deadline._

Submit the files and the function stubs as soon as you read the assignment. See the Checkpoints below.

Make sure to periodically backup your work by submitting it to Gradescope, so that in an unexpected event, we can use your backup, instead of giving you a 0 for a missing submission.

We will only grade the latest Gradescope submission.

-----

# Due Dates <a name="dates"></a>

The following components will count in your final project grade as follows:

- 5% - Checkpoint 1 grade
- 20% - Checkpoint 2 grade
- 75% - Final submission grade

The autograder for the project functions will be added to the assignment after Checkpoint 2 closes. Until then, make sure that you write the assert statements and test your program interactively on your Python IDLE (or other IDE if you want).

## Checkpoint 1: due {{site.checkpoint1 | date: "%a, %b %d, %H:%M" }}
}}

Create the required files listed above and verify that you can submit them all at once to Gradescope. If you run into any issues, let the TAs and/or ULAs know during your lab in Week 10.

To get full score for Checkpoint 1, make sure that you correctly implemented the **"List"**, **"Delete"**, and **"Quit"** menu options and everything that they need (see further sections about what those are).

- Upload the requested files shown above with the required functions added to them.
- Add the code and proper documentation (i.e. docsis and comments) for all functions.
- Add the function stubs and the documentation for the rest of the functions that are not implemented here - full functionality is not required for this checkpoint but you are welcome to include it as well.

## Checkpoint 2: due {{site.checkpoint2 | date: "%a, %b %d, %H:%M" }}
Checkpoint 2 assignment will open up on Gradescope as soon as Checkpoint 1 closes.

To get a full score for Checkpoint 2, make sure that you correctly implemented the **"Add"**, **"Restore"** and **"Save"** menu options and everything that they need. 

- Upload the requested files shown above with the required functions added to them.
- Add the code and proper documentation (i.e. docsis and comments) for all functions.
- Add the function stubs and the documentation for the rest of the functions that are not implemented here (i.e. the menu options for **"Edit"** and **"Show statistical data on"**) - full functionality is not required for this checkpoint but you are welcome to include it as well.

## Final Submission: due {{site.checkpoint3 | date: "%a, %b %d, %H:%M" }}
The Final Project assignment will open up on Gradescope as soon as Checkpoint 2 closes.
Submit your final version of the entire project here (i.e. full functionality required).

-----

# Late Submissions <a name="latesub"></a>

Submitting late Checkpoint 1 and Checkpoint 2 (by a max of 24 hours) will cause a 20% loss in grade for those checkpoints. Once Gradescope is closed for submission, it will not be re-opened.

**We will not accept any late submissions at all for the final submission.** The deadline for checkpoint 3 (i.e. {{site.checkpoint3 | date: "%a, %b %d, %H:%M" }}) is **absolutely the last day to submit**. This is a hard rule to ensure that we can grade the submissions in a timely manner and submit the final grades before the university deadline.

Please plan accordingly to make sure that travel, Internet or electricity outages or any other unexpected circumstances or events will not have a severe effect on your submission. **Start early, test often, and backup your work on Gradescope periodically.**

-----

# Project requirements <a name="reqs"></a>

## Programs that have syntax errors in the file will not receive any credit.

- ⚠️ Test your code for syntax errors before making a final submission.

   - _Run it in an IDE each time you make even a smallest change_: remember that even an extra space character can cause an error in Python. It is better for you to submit a partially working program than one that has syntax errors. We will not be modifying/correcting your code.

- **You are not allowed to use external libraries (like `math` or `statistics`) for this assignment except where specified in the instructions.** Your project might fail because of an unrecognized import (this includes libraries that we have not used in this class). Do not import anything unless the project specifically requests it.

- Do not create new functions or change the requested functions' names and/or the parameters, since you may lose points from the rubric set in Gradescope.

- You must correctly and appropriately comment your code to clearly explain your solution.

   - Every function should include an appropriate, informative docstring that is included immediately underneath the function signature. You will be graded on the presence and quality of your documentation. Include more extensive comments for the parts that you found harder to code. There shouldn't be any `pass` or `TODO` or `FIXME` comments left in your code!

-----

# Grading <a name="grading"></a> 

Your project will be automatically graded on Gradescope for the presence and naming of required files, functions, inclusion of docstrings, correct return values, etc. The autograder score will be the majority of the project grade.

If there are no syntax errors, we will manually grade the final project checking the correct code style, use of comments, and use of asserts in your test file.

If your project fails due to syntax errors, we will not manually grade it, automatically assigning it a 0 for the manual score. 

⚠️ Test your code for syntax errors before making a final submission!


-----

# Workflow Recommendations <a name="workflow"></a> 

We very highly recommend that you start working on this project early on. This is a large task ahead of you and good time management will help you complete this on time. Remember: you have TWO WEEKS to work on this, so **don't leave things until the last minute**. The deadlines are extremely firm.

As you are reading project instructions, each time you come across an edge case or a specific value that you need to check/test, immediately add an assert statement to your test file. Add a comment above it to remind you what part of the instructions you are testing.

We highly recommend developing your code **incrementally**: as soon as you add an option or a new condition, immediately run your code to verify that it works as intended.

Use the `assert` statements to check that your code returns the expected value and is of a correct type. Use it especially to test the edge cases (e.g., when to return -1 or 0, what to do when the input is empty).

We highly encourage you to add your own tests to check each function specification and to verify the correctness of your implementation.

If you see an `AssertionError`, check the line number that the error message pointed to. In IDLE, you can select the "Show Line Numbers" option from the top "Options" menu.

-----

# Submission Checklist <a name="checklist"></a> 

Long before each checkpoint deadline, walk through these steps:

- run your files to ensure that they are free from syntax errors.
- verify that the function names are correct - check them again.
- check that each function has a proper docstring directly underneath each function signature
- make sure that the main program only has the necessary import (it's just one import instruction)
- check all default values! We will test that you are using them.
- be sure that you test for the invalid 'arguments'/'input values' in each function (use the assert statements).
- submit all properly-named Python files to Gradescope

-----

# Asking for Staff Help <a name="help"></a> 

This assignment is supposed to be like an exam in that it is supposed to test your knowledge and understanding of the course material, so it is supposed to be your own work. Make sure that you read and follow the instructions carefully.

- No project-related coding questions during the office hours! You can ask questions on concepts or general techniques, but not specific coding questions.
- It's actually best to have your questions or clarifications be made as a public post on Piazza (so everyone can benefit).
   - Posts have to follow the forum guidelines - no publicly shared code/solutions! Violation of the forum guidelines will result in a deduction of 10% of your grade per violation.
   - If necessary, post a short, self-contained snippet to reproduce the error: follow the style/examples that we've discussed as part of how to debug a program.
   - No posts after the final submission is due (i.e. after Monday, December 5, at 11:59 PM).
- Do not email the TAs/ULAs directly: again - use Piazza instead.
- Make sure to submit your code to Gradescope before posting something on the forum (if necessary, we can load your submission for reference).
- If you are asking a question that is too open-ended, we cannot guarantee that we can provide you with a hint. We will try and give you as much help as we can, _but in the end we cannot provide any solutions to you_. Again, this project is supposed to be your own work.

-----

# Updates <a name="updates"></a> 

If there are any updates to be given, they will be announced on Piazza. Make it a habit to check Piazza frequently. We will also put any major updates in this section here.

