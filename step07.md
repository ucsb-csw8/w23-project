---
layout: default
title: Step 7 - "Restore" option
---

# {{page.title}}

New functions needed:
* `load_menu_from_csv()`

This function
* reads data from a csv file, one line at a time
* validates it by trying to create a menu
* stores that data into the menu dictionary. 

> Advice: If you have trouble with your function, we recommend reviewing Section 9.6, and 9.7 on zyBooks. 

To implement your function, you must ```import csv``` in the **functions.py** file. For more information, refer to zyBooks section 9.7. You should be able to reuse your code directly from [LA 9.8](https://learn.zybooks.com/zybook/UCSBCMPSCW8Winter2023/chapter/9/section/8).

The function requires the `import csv` as well as `import os`. **NO OTHER import libraries/modules are allowed!**


# Sample Menu File

Below are the contents of a CSV file that is used in the sample program flow below. This file has no empty rows (lines) and no bad (invalid) data. If it did, that row would counted as being invalid.

**`menu.csv`**

```csv
burrito,500,12.9,yes,2
rice bowl,400,14.9,no,3
margherita,800,18.9,no,2
```

# Two other things you need to do:

The code to implement the `R` option is similar to the one for the option `S`. You'll need:
* code in **`main.py`** to look for the `R` option and call the appropriate helper function, which must be called `load_helper`
* the function definition for `load_helper`, which must go into **`functions.py`**.)

# Sample Program Flow

This example run has the user doing the following:
* Starts by deleting all the dishes in current menu
* Then attempting to restore data from a file
   * First attempt: using a bad file name (doesn't end in .csv)
   * Second attempt: using a bad file name (ends in .csv, but file doesn't exist)
   * Third attempt: successful
* Then lists the menu to make sure they were indeed restored.

```
==========================
What would you like to do?
L - List
A - Add
U - Update
D - Delete
H - Display restaurant expense rating
S - Save the data to file
R - Restore data from file
Q - Quit this program
==========================
::: Enter a menu option
> D
You selected option D to > Delete.
Which dish would you like to delete?
Press A to delete the entire menu for this restaurant, M to cancel this operation
------------------------------------------
1. BURRITO
2. RICE BOWL
3. MARGHERITA
------------------------------------------
> A
::: WARNING! Are you sure you want to delete the entire menu ?
::: Type Yes to continue the deletion.
> Yes
Deleted the entire menu.
::: Press Enter to continue
==========================
What would you like to do?
L - List
A - Add
U - Update
D - Delete
H - Display restaurant expense rating
S - Save the data to file
R - Restore data from file
Q - Quit this program
==========================
::: Enter a menu option
> R
You selected option R to > Restore data from file.
::: Enter the filename ending with '.csv'.
> wrong_menu
WARNING: |wrong_menu| is an invalid file name!
::: Would you like to try again? Enter 'y' to try again.
>
WARNING: |wrong_menu| contains invalid data!
The following rows from the file were not loaded:
-1
::: Would you like to load another file? Enter 'y' to try again.
> y
::: Enter the filename ending with '.csv'.
> wrong_menu.csv
WARNING: |wrong_menu.csv| was not found!
::: Would you like to try again? Enter 'y' to try again.
> y
::: Enter the filename ending with '.csv'.
> menu.csv
Successfully restored restaurant menu from |menu.csv|
::: Press Enter to continue
==========================
What would you like to do?
L - List
A - Add
U - Update
D - Delete
H - Display restaurant expense rating
S - Save the data to file
R - Restore data from file
Q - Quit this program
==========================
::: Enter a menu option
> L
You selected option L to > List.
::: What field would you like to list?
A - complete menu
V - vegetarian dishes only
::: Enter your selection
> A
You selected |A| to list |complete menu|.
------------------------------------------
1. BURRITO
* Calories: 500
* Price: 12.9
* Is it vegetarian: yes
* Spicy level: Low key spicy

2. RICE BOWL
* Calories: 400
* Price: 14.9
* Is it vegetarian: no
* Spicy level: Hot

3. MARGHERITA
* Calories: 800
* Price: 18.9
* Is it vegetarian: no
* Spicy level: Low key spicy

------------------------------------------
```

# What if the CSV file has **bad** data?

Now, what if the CSV file has "invalid data" in it? "Invalid data" is **only** defined as data that would be flagged as an error by the `get_new_menu_dish()` function (example: bad name, bad format, etc...). For example, a dish with price `10.001`, should not be considered to be "invalid" because that is not something that is validated by `get_new_menu_dish()`.  

For instance, if the CSV file being read is:

**`menu_somebad.csv`**

```csv
burrito,500,12.9,maybe,2
rice bowl,400,14.9,no,3
margherita,800,18.9,no,100
```

Notice that line (row) 1 has a bad (invalid) is_vegetarian (`maybe`) and that line 3 has a bad spicy_level (`100` - that's too hot!).
The function `load_from_csv()` should update the menu dictionary with new dishes from line 2 _only_ AND it should return a list that is **[1, 3]** (because lines 1 and 3 are the ones with invalid data in them).

Here's a sample run for when a file, like the one above, is restored:

```
==========================
What would you like to do?
L - List
A - Add
E - Update
D - Delete
M - Show statistical data on
S - Save the data to file
R - Restore data from file
Q - Quit this program
==========================
::: Enter a menu option
> r
You selected option R to > Restore data from file.
::: Enter the filename ending with '.csv'.
> menu_somebad.csv
WARNING: |menu_somebad.csv| contains invalid data!
The following rows from the file were not loaded:
[1, 3]
::: Would you like to try again? Enter 'y' to try again.
```

# A hint

If the `Save` option from the previous step is working correctly, the file you wrote into using that option should work perfectly with your new `Restore` option.

When saving and restoring, your entire menu information should be loaded properly.

You may want to try saving, restoring, and listing a few times to make sure that everything works.


# Checkpoint 2

After finishing this step, you are ready for Checkpoint 2.

See the [Checkpoint 2 instructions at Step 2](/w23-project/step01#checkpoint2) for more information
