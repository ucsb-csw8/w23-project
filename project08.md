---
layout: default
title: Step 8 - "Save" option
---

# {{page.title}}


New functions needed:
* `save_to_csv()`

We hope that by now you realize the importance of storing and retrieving data. It will help you resume your work from where you left without hardcoding those values. We will now add options that will let you store your songs into a file and read them back into your song information manager.

You need to complete the function ```save_to_csv()``` as defined below. You may refer to your ```save_temperature_statistics()``` function from [LA 9.9](https://learn.zybooks.com/zybook/UCSBCMPSCW8MatniFall2022/chapter/9/section/9). Both of these functions perform similar activity. The major change is in the data written in each line of the csv file.

To implement this function, we need to use `import csv` in our **songs\_functions.py** file.
The function then uses the csv writer object to write this list as a line into the `filename` file.

The function requires the `import csv` as well as `import os`. **NO OTHER import libraries/modules are allowed!**

```
def save_to_csv(song_dict, filename):
    """
    param: song_dict(dict of dict) - The dictionary of songs stored 
    param: filename (str) - A string that ends with '.csv' which represents
               the name of the file to which to save the songs. This file will
               be created if it is not present, otherwise, it will be overwritten.

    The function ensures that the last 4 characters of the filename are '.csv'.
    The function requires the `import csv` as well as `import os`.

    The function will use the `with` statement to open the file `filename`.
    After creating a csv writer object, the function uses a `for` loop
    to loop over every song in the dictionary and creates a new list
    containing only strings - this list is saved into the file by the csv writer
    object. The order of the elements in the dictionary is:

    * title
    * artist
    * length
    * album
    * genre (all element in the original list are converted to string
        joined with commas separating)
    * rating (converted to string)
    * released (written as string, i.e, "06/06/2022", NOT "June 6, 2022")
    * favorite (converted to string)
    * uid

    returns:
    -1 if the last 4 characters in `filename` are not '.csv'
    None if we are able to successfully write into `filename`
    """
```

The portion of the **main program** code is provided below. Complete the missing parts and add them in the correct place to your song information manager.

```
	elif opt == 'S':
		continue_action = ...
		while continue_action == 'y':
			print("::: Enter the filename ending with '.csv'.")
			filename = input("> ")
			... = save_to_csv(..., ...) # TODO: Call the function with appropriate inputs and capture the output
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
> saved_songs.csv
Successfully stored all songs to |saved_songs.csv|
::: Press Enter to continue
```

In your computer directory, you should now see a new file called `saved_songs.csv`. If you open it with a text editor, it would look like this:
```
Cardigan,Taylor Swift,03:59,Folklore,"folk,indie rock",4,07/27/2020,True,12332
Soul Meets Body,Death Cab for Cutie,,Plans,"indie pop,indie rock",5,07/16/2005,True,14567
Fake Love,BTS,04:02,,"hip hop,electro pop,Korean pop",3,05/18/2018,False,78210
Foil,'Weird Al' Yankovic,02:22,Mandatory Fun,"pop,parody",5,07/15/2014,True,99105
```
You can also open .csv files with Microsoft Excel (if you have that program - don't worry about it if you don't). You would see something like this:

![alt text](https://sites.cs.ucsb.edu/~zmatni/excel.png "Excel screen shot")

**NOTE:** This option and the next option (restore) should be compatible with each other: i.e., whatever you write to a csv file using this option, you should be able to read back using the next option and vice-versa.





