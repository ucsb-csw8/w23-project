---
layout: default
title: 'Step 2 - Intro, and "Quit" option'
---

# {{page.title}}

# Restaurant Menu Management System 📝

## Read these guidelines _in their entirety_ before implementing anything.

In this project, similar in structure to the Grades Management System from Lab 8, you will create a **Restaurant Menu Management System**!

Incorporate functions from multiple labs to implement an interactive program, which you can use to collect and create data needed to store restaurant menu information.

This project is intended to be implemented in an IDE, which will allow you to run your code interactively.
You will need to create several files in order to implement and test your functions as well as to run your main program.

The “Getting Started” section shows you the steps to modify the Main Program (Template), so that within 15-20 minutes, you should be able to have a fully running skeleton of the system.

# Table of Contents
1. [Introduction](#introduction)
1. [Main Menu](#mainmenu)
1. [Main Program (Template)](#maintemplate)
1. [Getting Started](#gettingstarted)
1. [Create the test file](#testfile)

---

## Introduction <a name="introduction"></a>

You will implement the following features for this system:

* Create an interface that allows the users to interact with the system (will use `while True` and `input()` to collect user data).
* Create a collection to store menu item information that the users can view and maintain by adding and editing entries.
* Allow the user to save the state of the system by saving the information to file and retrieving it from it.

You will need to use some code that you wrote in previous labs.


[Back to top](#top)

---


## Main Menu <a name="mainmenu"></a>

In your main program (main.py), you need to define a dictionary `the_menu` that has the options shown below.
```
    "L" : "List"
    "A" : "Add"
    "U" : "Update"
    "D" : "Delete"
    "M" : "Show average price"
    "S" : "Save the data to file"
    "R" : "Restore data from file"
    "Q" : "Quit this program"
```

The menu should be printed by the `print_main_menu()` function when the user starts this system.
🎊 You already implemented this function in prior labs.

* You can find this function definition in your prior labs and then copy it directly into the  **functions.py**.
* If you are having trouble locating that file, you can always look at your past Gradescope and zyLabs submissions for it.

The `print_main_menu()` function does not return anything, it just prints the correctly-formatted options that are provided in the dictionary.

[Back to top](#top)

---

## Main Program (Template) <a name="maintemplate"></a>

**Use the following starter code** to implement the main loop for your program:

```python
from functions import *

if __name__ == "__main__":
    the_menu = {} # TODO 1: add the options from the instructions
    opt = None

    while True:
        # print_main_menu(...) # TODO 1: uncomment, define the function, and call with the menu as an argument
        print("::: Enter an option")
        opt = input("> ")

        if opt == ...: # TODO 2: make Q or q quit the program
            print("Goodbye!\n")
            break # exit the main `while` loop
        else:
            if ...: # TODO 3: check of the character stored in opt is in the_menu dictionary
                print(f"You selected option {opt} to > {the_menu[opt]}.")
            else:
                print(f"WARNING: {opt} is an invalid option.\n")

    print("Have a delicious day!")
```

**Important:** Every time you see the `:::` and `>` in the prompts, it denotes the call to the `input()` function as shown in the starter code. After the `"::: Press Enter to continue"` prompt is displayed and the user presses Enter, the system is set up to print the main menu at the start of the loop.

[Back to top](#top)

---

## Getting Started <a name="gettingstarted"></a>

1. Create the requested Python files.
1. Copy the above template into your **main program file**.
1. Upload the files to Gradescope to ensure the names are correct. **You will need to submit _all_ files at _the same_ time to Gradescope (not in zyBooks).**
1. Address the TODO comments in the code (including adding the `print_main_menu()` to the **functions.py**)

Now, you are ready to create the `if`/`elif` branches to call the functions for the various menu options. 
In the rest of the instructions, you will get to implement the rest of the options, defining the needed functions, and calling them (remember to remove the `TODO` comments).

[Back to top](#top)

---


# Submit the three files to Gradescope

TODO: Once you assembled the above template and your main program, and the testing code runs without any errors, **submit your files to Checkpoint 1 on Gradescope**.  

You should still at least pass the basic "Check required files" test, but you might be passing a few more as well.

You should now have a basic structure for the system, and you are ready to begin implementing each option.

