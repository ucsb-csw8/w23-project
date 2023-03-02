---
layout: default
title: Step 4 - "Add" option
---

# {{page.title}}

New functions needed:
* `get_new_song()`
* `is_valid_addlist()`
* `is_valid_title()`
* `is_valid_time()`
* `is_valid_date()`
* `is_valid_uid()`

Add the following branch to your **main program**; replace the ellipses with the appropriate values. See below for sample run outputs.
```
    elif opt == 'A':
        continue_action = 'y'
        while continue_action == 'y':
            song_info = []
            print("::: Enter each required field:")
            # TODO: Get user inputs for all 9 song info fields (i.e. keys). 
            # Get *all* inputs as strings.
            ... input("Title: ")...
            ... input("Artist: ")... 
            ... etc ...

            result = get_new_song(...) # TODO: attempt to create a new song
            if type(result) == dict:
                ... # TODO: add a new song to the list of songs
                print(f"Successfully added a new song!")
                print_song(result, ...)
            elif type(result) == tuple:
                print(f"WARNING: invalid data!")
                print(f"Error: {result[0]}")
                       
            print("::: Would you like to add another song?", end=" ")
            continue_action = input("Enter 'y' to continue.\n> ")
            continue_action = continue_action.lower() 
            # ----------------------------------------------------------------
```

In your **functions file**, define `get_new_song()` that takes 3 parameters: a list of strings, a dictionary (the rating map - which you may or may not want to use in the function), and a key_list of the `all_songs` dictionary. See more details below.
```
def get_new_song(..., ..., ...):
    """
    Document the function correctly
    """
```
The function **returns** different types of values, _depending on whether it succeeds or fails_.

* The function has to first validate some things:
   * The entire input list has to be made up of strings. The function calls the helper function `is_valid_addlist()` to check this. 
      * This helper function returns a Boolean value. 
      * If the value is invalid, then `get_new_song()` has to return a tuple containing the message string `"Bad list. Found non-string, or bad length"` and the integer 0.

   * The "title" value has to be a string that's at least 2 characters long and at most 40 characters long. The function calls the helper function `is_valid_title()` to check this. 
      * This helper function returns a Boolean value. 
      * If the value is invalid, then `get_new_song()` has to return a tuple containing the message string `"Bad Title length"` and the integer -1.

   * The "length" value has to be in **00:00** format, that is, it's a string that has 2 digits, followed by a colon, followed by 2 digits. The function calls the helper function `is_valid_time()` to check this. 
      * This helper function returns a Boolean value. 
      * If the value is invalid, then `get_new_song()` has to return a tuple containing the message string `"Invalid time format for Length"` and the integer -2.

   * The "rating" value has to be a string that is a digit between 1 and 5 (inclusive). There is no need for a helper function for this.
      * If the value is invalid, then `get_new_song()` has to return a tuple containing the message string `"Invalid Rating value"` and the integer -3.

   * The "released" value has to be in **MM/DD/YYYY** format. The function calls the helper function `is_valid_date()` to check this.
      * `is_valid_date()` is very much like an exercise you all did before: refer to [Lab 7.19](https://learn.zybooks.com/zybook/UCSBCMPSCW8MatniFall2022/chapter/7/section/19) for big clues on how to do this.
      * This helper function returns a Boolean value. You have implemented a function like this in previous labs.
      * If the value is invalid, then `get_new_song()` has to return a tuple containing the message string `"Invalid date format for Release Date"` and the integer -4.

   * The "favorite" value has to be a string that either "true" or "false". It's ok for the user to also enter "True" or "T" or "t", etc... In other words the value has to start with T, t, F, or f. There is no need for a helper function for this.
      * If the value is invalid, then `get_new_song()` has to return a tuple containing the message string `"Invalid value for Favorite"` and the integer -5.

   * The "uid" value is a string that has to be made up of exactly 5 digits. The range of these digits can only be "10000" to "99999". Additionally, this value has to be **_unique_**  to any other uid value in the current song dictionary (`all_songs`). The function calls the helper function `is_valid_uid(str, key_list)` to check this. The `key_list` parameter is a list of all the keys in the song dictionary (hint: you can use the .key() method to obtain these).
      * This helper function returns a Boolean value. 
      * If the value is invalid, then `get_new_song()` has to return a tuple containing the message string `"Unique ID is invalid or non-unique"` and the integer -6.

* Once validation is taken care of, then the values passed into `get_new_song()` through its list parameter, must be added as values to a **new** dictionary with the 9 song keys (i.e. "title", "artist", "length", etc...)
   * **Important**: make sure when you add these values that they are added as the correct data type.
   * The new dictionary gets **returned** at the conclusion of this process.

The first input parameter is a **list** of all needed song dictionary values stored **as strings**: 
   * The order of the fields is ** title, artist, length, album, genre, rating, released, favorite, uid.**
   * An example valid input list might look like `["Cardigan - Extended Version", "Taylor Swift", "07:59", "Folklore", "folk,indie rock", "3", "07/27/2020", "True", "12333"]`
   * If the provided field values are valid, return a new dictionary:

```
{
    "title": ...,  # str
    "artist": ..., # str
    "length": ...  # str
    "album": ...,  # str
    "genre": ...   # list
    "rating": ...    # int
    "released": ...  # str
    "favorite": ...  # bool
    "uid": ...       # int
}
```

Note that  `get_new_song()` relies on several helper functions that validate different song fields. 
The helper functions will need to be added first, before defining `get_new_song()`.

⚠️ Pay close attention to the number of parameters and their types!

Example of asserts you could have in your **test file**:
```
addlist1 = ["Cardigan - Extended Version", "Taylor Swift", "07:59", "Folklore", "folk,indie rock", "3", "07/27/2020", "True", "12333"]
addlist2 = ["Cardigan - Extended Version", "Taylor Swift", "07:59", "Folklore", "folk,indie rock", 3, "07/27/2020", True, "12333"]
addlist3 = ["Cardigan - Extended Version", "Taylor Swift", "b7:59", "Folklore"]

assert is_valid_addlist(addlist1) == True
assert is_valid_addlist(addlist2) == False
assert is_valid_addlist(addlist3) == False

assert is_valid_time(addlist1[2]) == True
assert is_valid_time(addlist3[2]) == False

# ...etc...
```


# Sample Program Flow

Below is a demo of adding an incorrect song value (bad time length format):
```
You selected option A to > Add.
::: Enter each required field:
Title: Cardigan - Extended Version
Artist: Taylor Swift
Length (00:00 format): 7:59
Album: Folklore
Genres (separate them with commas): folk, indie rock
Rating (1-5): 3
Release Date (MM/DD/YYYY format): 07/27/2020
Favorite (T/F): t
Unique ID: 12333
WARNING: invalid data!
Error: Invalid time format for Length
::: Would you like to add another song? Enter 'y' to continue.
> 
```

Here is a demo of adding a different incorrect song value (non-unique Unique ID - I use one that's already in the song dictionary):
```
You selected option A to > Add.
::: Enter each required field:
Title: Cardigan - Extended Version
Artist: Taylor Swift
Length (00:00 format): 07:59
Album: Folklore
Genres (separate them with commas): folk, indie rock
Rating (1-5): 3
Release Date (MM/DD/YYYY format): 07/27/2020
Favorite (T/F): True!
Unique ID: 12332
WARNING: invalid data!
Error: Unique ID is invalid or non-unique
::: Would you like to add another song? Enter 'y' to continue.
> 
```

Finally, here's a demo of adding a new song successfully:
```
You selected option A to > Add.
::: Enter each required field:
Title: Cardigan - Extended Version
Artist: Taylor Swift
Length (00:00 format): 07:59
Album: Folklore
Genres (separate them with commas): folk, indie rock
Rating (1-5): 3
Release Date (MM/DD/YYYY format): 07/27/2020
Favorite (T/F): T
Unique ID: 12333
Successfully added a new song!
 TITLE: Cardigan - Extended Version
  ARTIST: Taylor Swift
  LENGTH: 07:59
   ALBUM: Folklore
   GENRE: Folk, Indie Rock
  RATING: Neutral
RELEASED: July 27, 2020
FAVORITE: True
******************************************
::: Would you like to add another song? Enter 'y' to continue.
> 
```

After successfully adding a new song, you should be able to see it in the List menu option. For example:
```
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
 TITLE: Fake Love
 TITLE: Foil
 TITLE: Cardigan - Extended Version
::: Press Enter to continue
```
