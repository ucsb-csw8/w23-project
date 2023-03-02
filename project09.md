---
layout: default
title: Step 9 - "Restore" option
---

# {{page.title}}

New functions needed:
* `load_from_csv()`

This function
* reads data from a csv file, one line at a time
* validates it by trying to create a song
* stores that data into the song dictionary. 

> Advice: If you have trouble with your ```load_from_csv()```, we recommend reviewing Section 9.6, and 9.7 on zyBooks. 

To implement your function, you must ```import csv``` in the **song\_functions.py** file. For more information, refer to zyBooks section 9.7. You can also refer to [LA 9.8](https://learn.zybooks.com/zybook/UCSBCMPSCW8MatniFall2022/chapter/9/section/8).

The function requires the `import csv` as well as `import os`. **NO OTHER import libraries/modules are allowed!**

The template for ```load_from_csv()``` is provided below.

```
def load_from_csv(filename, in_dict, rating_map, allkeys):
    """
    param: filename (str) - A string variable which represents the
            name of the file from which to read the contents.
    param: in_dict (dict of dict) - A dictionary of songs (dictionary objects) to which
            the songs read from the provided filename are added.
            If in_dict is not empty, the existing songs are not dropped.
    param: rating_map (dict) - a dictionary object that is expected
            to have the integer keys that correspond to the "rating"
            integer values stored in the song; the stored value is displayed 
            for the rating field, instead of the numeric value.
    param: allkeys (key_list) - a key_list of all keys in the song dictionary
    
    The function ensures that the last 4 characters of the filename are '.csv'.
    The function requires the `import csv` and `import os`.

    If the file exists, the function will use the `with` statement to open the
    `filename` in read mode. For each row in the csv file, the function will
    proceed to create a new song using the `get_new_song()` function.
    - If the function `get_new_song()` returns a valid song object,
    it gets added to `in_dict`.
    - If the `get_new_song()` function returns an error, the 1-based
    row index gets recorded and added to the NEW list that is returned.
    E.g., if the file has a single row, and that row has invalid song data,
    the function would return [1] to indicate that the first row caused an
    error; in this case, the `in_dict` would not be modified.
    If there is more than one invalid row, they get excluded from the
    in_dict and their indices will be appended to the new list that's
    returned.

    returns:
    * -1, if the last 4 characters in `filename` are not '.csv'
    * None, if `filename` does not exist.
    * A new empty list, if the entire file is successfully read from `in_dict`.
    * A list that records the 1-based index of invalid rows detected when
      calling get_new_song().

    Helper functions:
    - get_new_song()
    """
```

# Sample Song File

Below are the contents of a CSV file that is used in the sample program flow below. This file has no empty rows (lines) and no bad (invalid) data. If it did, that row would counted as being invalid.

**`matni_songs_allgood.csv`**
```
Cardigan,Taylor Swift,03:59,Folklore,"folk,indie rock",4,07/27/2020,True,12332
Soul Meets Body,Death Cab for Cutie,04:04,Plans,"indie pop,indie rock",5,07/16/2005,True,14567
X&Y,Coldplay,04:11,X&Y,"rock",5,07/18/2005,True,14568
Fake Love,BTS,04:02,,"hip hop,electro pop,Korean pop",3,05/18/2018,False,78210
Fake Love - VERSION 2,BTS,04:02,,"hip hop,electro pop,Korean pop",3,05/18/2018,False,78211
Foil,'Weird Al' Yankovic,02:22,Mandatory Fun,"pop,parody",5,07/15/2014,True,99105
```
The corresponding code for the **main program** is similar to the one for the option `S`. Your task to figure out what to add using the following user interactions. 

# Sample Program Flow

This example run has the user doing the following:
* Starts by deleting all the songs
* Then attempting to restore data from a file
   * First attempt: using a bad file name (doesn't end in .csv)
   * Second attempt: using a bad file name (ends in .csv, but file doesn't exist)
   * Third attempt: successful
* Then lists the songs to make sure they were indeed restored.

```
==========================
What would you like to do?
L - List
A - Add
E - Edit
D - Delete
M - Show statistical data on
S - Save the data to file
R - Restore data from file
Q - Quit this program
==========================
::: Enter a menu option
> D
You selected option D to > Delete.
******************************************
      ID: 12332 | TITLE: Cardigan
      ID: 14567 | TITLE: Soul Meets Body
      ID: 78210 | TITLE: Fake Love
      ID: 99105 | TITLE: Foil
Which song would you like to delete?
X - Delete all songs at once
::: OR Enter the number corresponding to the song ID
::: OR press 'M' to cancel and return to the main menu.
> X
::: WARNING! Are you sure you want to delete ALL songs?
::: Type Yes to continue the deletion.
> Yes
Deleted all songs.
::: Press Enter to continue
==========================
What would you like to do?
L - List
A - Add
E - Edit
D - Delete
M - Show statistical data on
S - Save the data to file
R - Restore data from file
Q - Quit this program
==========================
::: Enter a menu option
> R
You selected option R to > Restore data from file.
::: Enter the filename ending with '.csv'.
> xxx
WARNING: invalid input - must end with '.csv'
::: Would you like to try again? Enter 'y' to try again.
> y
::: Enter the filename ending with '.csv'.
> xxx.csv
WARNING: |xxx.csv| was not found!
::: Would you like to try again? Enter 'y' to try again.
> y
::: Enter the filename ending with '.csv'.
> matni_songs.csv
Successfully restored all songs from |matni_songs.csv|
::: Would you like to try again? Enter 'y' to try again.
> n
::: Press Enter to continue
==========================
What would you like to do?
L - List
A - Add
E - Edit
D - Delete
M - Show statistical data on
S - Save the data to file
R - Restore data from file
Q - Quit this program
==========================
::: Enter a menu option
> L
You selected option L to > List.
::: What would you like to list?
A - all songs - full
B - all songs - titles only
F - favorite songs
G - songs of a specific genre
::: Enter your selection
> b
You selected |B| to list |all songs - titles only|.
******************************************
 TITLE: Cardigan
 TITLE: Soul Meets Body
 TITLE: X&Y
 TITLE: Fake Love
 TITLE: Fake Love - VERSION 2
 TITLE: Foil
::: Press Enter to continue
```
> NEW! - More Detailed Instructions: What if the CSV file has **bad** data?

Now, what if the CSV file has "invalid data" in it? "Invalid data" is **only** defined as data that would be flagged as an error by the `get_new_song()` function (example: bad title, bad date format, etc...). For example, a blank Album string, should not be considered to be "invalid" because that is not something that is validated by `get_new_song()`. 

For instance, if the CSV file being read is:

**`matni_songs_somebad.csv`**
```
Cardigan,Taylor Swift,3:59,Folklore,"folk,indie rock",4,07/27/2020,True,12332
Soul Meets Body,Death Cab for Cutie,04:04,Plans,"indie pop,indie rock",5,07/16/2005,True,14567
X&Y,Coldplay,04:11,X&Y,"rock",5,07/1B/2005,True,14568
Fake Love,BTS,04:02,,"hip hop,electro pop,Korean pop",3,05/18/2018,False,78210
Fake Love - VERSION 2,BTS,04:02,,"hip hop,electro pop,Korean pop",3,05/18/2018,False,78211
Foil,'Weird Al' Yankovic,02:22,Mandatory Fun,"pop,parody",5,07/15/2014,True,99105
```

Notice that line (row) 1 has a bad (invalid) time format (`3:59`) and that line 3 has a bad date format (`07/1B/2005`).
The function `load_from_csv()` should update the song dictionary with new songs from lines 2, 4, 5, and 6 _only_ AND it should return a list that is **[1, 3]** (because lines 1 and 3 are the ones with invalid data in them).

Here's a sample run for when a file, like the one above, is restored:

```
==========================
What would you like to do?
L - List
A - Add
E - Edit
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
> matni_songs_somebad.csv
WARNING: |matni_songs_somebad.csv| contains invalid data!
The following rows from the file were not loaded:
[1, 3]
::: Would you like to try again? Enter 'y' to try again.
```

**ADDITIONAL NOTE:** If your ```Save the data to file``` option is working correctly, the file you wrote into using that option should work perfectly with this option and your entire song information should be loaded properly.


