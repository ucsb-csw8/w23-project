---
layout: default
title: Step 8 - "Save" option
---

# {{page.title}}


New functions needed:
* `save_menu_to_csv()`

We hope that by now you realize the importance of storing and retrieving data. It will help you resume your work from where you left without hardcoding those values. We will now add options that will let you store your restaurant menu into a file and read them back into your dishes information manager.

You need to complete the function ```save_menu_to_csv()``` as defined below. You may refer to your ```save_menu_to_csv()``` function from [LA 9.9](https://learn.zybooks.com/zybook/UCSBCMPSCW8Winter2023/chapter/9/section/9). Both of these functions perform similar activity. The major change is in the data written in each line of the csv file.

To implement this function, we need to use `import csv` in our **functions.py** file.
The function then uses the csv writer object to write this list as a line into the `filename` file.

The function requires the `import csv` as well as `import os`. **NO OTHER import libraries/modules are allowed!**

```
def save_menu_to_csv(restaurant_menu_list, filename):
    """
    param: restaurant_menu_list(list of dict) - The list shore dictionary of dishes 
    param: filename (str) - A string that ends with '.csv' which represents
               the name of the file to which to save the songs. This file will
               be created if it is not present, otherwise, it will be overwritten.

    The function ensures that the last 4 characters of the filename are '.csv'.
    The function requires the `import csv` as well as `import os`.

    The function will use the `with` statement to open the file `filename`.
    After creating a csv writer object, the function uses a `for` loop
    to loop over every dishes dictionary in the dictionaries list and creates a new list
    containing only strings - this list is saved into the file by the csv writer
    object. The order of the elements in the dictionary is:
    * name
    * calories
    * price
    * is_vegetarian
    * spicy_level
    
    returns:
    -1 if the last 4 characters in `filename` are not '.csv'
    None if we are able to successfully write into `filename`
    """
```

The portion of the **main program** code is provided below. Complete the missing parts and add them in the correct place to your menu information manager.

```
	elif opt == 'S':
		continue_action = ...
		while continue_action == 'y':
			print("::: Enter the filename ending with '.csv'.")
			filename = input("> ")
			... = save_menu_to_csv(..., ...) # TODO: Call the function with appropriate inputs and capture the output
			if ... == -1: # TODO
				print(f"WARNING: |{...}| is an invalid file name!") # TODO
				print("::: Would you like to try again?", end=" ")
				continue_action = input("Enter 'y' to try again.\n> ")
			else:
				print(f"Successfully stored all the songs to |{...}|")
                                continue_action = 'n'
	#--------------------------------------------------------------------------
```

# Sample Program Flow

This example run has the user doing the following:
* Attempts to save the file with a bad file name (does not end in .csv)
* Saves the file with a good file name.

```
> s
You selected option S to > Save the data to file.
::: Enter the filename ending with '.csv'.
> xxx
WARNING: |xxx| is an invalid file name!
::: Would you like to try again? Enter 'y' to try again.
> y
::: Enter the filename ending with '.csv'.
> saved_menu.csv
Successfully stored all songs to |saved_menu.csv|
::: Press Enter to continue
```

In your computer directory, you should now see a new file called `saved_menu.csv`. If you open it with a text editor, it would look like this:
```
burrito,500,12.9,yes,2
rice bowl,400,14.9,no,3
margherita,800,18.9,no,2
```
You can also open .csv files with Microsoft Excel (if you have that program - don't worry about it if you don't). You would see something like this:


|       name | calories | price | is_vegetarian | spicy_level |
|-----------:|---------:|-------|--------------:|------------:|
|    burrito |      500 | 12.9  |           yes |           2 |
|  rice bowl |      400 | 14.9  |            no |           3 |
| margherita |      800 | 18.9  |            no |           2 |

**NOTE:** This option and the next option (restore) should be compatible with each other: i.e., whatever you write to a csv file using this option, you should be able to read back using the next option and vice-versa.





