---
layout: default
title: Step 3 - "List" option
---

# {{page.title}}


## Background

Oftentimes, data is stored in a very compact but not human-friendly way. Think of how our forum questions may be stored in Piazza databases somewhere in the cloud. One way a question-object may be stored is this:

```
{
    'title': 'Extension',
    'description': 'hey i submitted my lab 2 hours after the deadline. Do you think there is...',
    'author_uid': 'a_39',
    'answers': [],
    'is_private': False,
    'tags': ['logistics', 'week7'],
    'created': '2022-05-21T05:28:43Z',
    ...
}
```

Obviously, this format is not user-readable, so Piazza's _frontend_ team produced many lines of code to render and display this content in a way that's more understandable to us, the Piazza users.

We have a mini-version of the same task coming up. Given a list of similar complex objects (represented by Python dictionaries, lists, and other "data containers"), display them in a user-friendly way that we'll define in these instructions.

Since we will be doing this for menu information items, we need to figure out how and what to store for each piece of information.


# What is "menu information"?

* In this project, for the ease of testing, you can **hard-code** a list "information" at the top of your **main program**, after the dictionary `the_menu`
*'. We will refer to it as `all_songs`. This **list** will contain **dictionaries** with each menu item's information.

In this project, **one menu items's information** is a **dictionary** object that is guaranteed to have the following keys:

* `"name"`: a string with the menu item's name.
* `"calories"`: an integer with the number of calories in the menu item.
* `"price"`: a float with the menu item's price using the format 00.00.
* `"is_vegetarian"`: a string with value "yes" or "no" for if the menu item is vegetarian.
* `"genre"`: a variable length list of strings with the genres of the music applicable to the song.
* `"spicy_level"`: an integer from 1 to 4, representing the menu item's spice level.

Here is an example of what a dictionary with a **single menu item's information** could look like:

```
{
"name": "burrito",
"calories": 500,
"price": 12.90,
"is_vegetarian": "yes",
"spicy_level": 2
}
```

In this project, for the ease of testing, we will **hard-code** a list  of menu item information at the top of the **main program**, after the dictionary `the_menu`. We will refer to it as `restaurant_menu_list`. This is just an example dictionary containing 4 menu item information dictionaries that can be used to test our system as we develop it. You can add more of your own examples as longs as they adhere to the correct formats and types of the dictionary values.

```
restaurant_menu_list = [
            {
                "name": "burrito",
                "calories": 500,
                "price": 12.90,
                "is_vegetarian": "yes",
                "spicy_level": 2
            },
            {
                "name": "rice bowl",
                "calories": 400,
                "price": 14.90,
                "is_vegetarian": "no",
                "spicy_level": 3
            },
            {
                "name": "margherita",
                "calories": 800,
                "price": 18.90,
                "is_vegetarian": "no",
                "spicy_level": 2
            }
        ]
```

# Your TODO <a name="inittodo"></a>

* Create a variable to hold a nested dictionary of menu item information data (dictionaries) at the top of your **main program**. We will refer to it as `restaurant_menu_list`.

* Additionally, you need to add two more dictionaries to your **main program**:
  * `list_menu` will contain the "List" menu sub-options
  * `spicy_scale_map` will contain the mapping of the spicy_level values, as integers, to a string for the name of the spice level

```
list_menu = {
    "A": "all songs - full",
    "B": "all songs - titles only",
    "F": "favorite songs",
    "G": "songs of a specific genre"
}

rating_map = {
    "1": "Hate",
    "2": "Dislike",
    "3": "Neutral",
    "4": "Like",
    "5": "Love!"
}
```

* Next, add the following code to your **main program** to implement the listing of the menu items - you do not need to change it as shown below.
  * Note that there is a new function `get_selection()` that needs to be implemented and that is _also_ given to you after the code below.

```
    elif opt == 'L':
        if all_songs == {}:
            print("WARNING: There is nothing to display!")
            # Pause before going back to the main menu
            input("::: Press Enter to continue")
            continue

        subopt = get_selection(the_menu[opt], list_menu)
        if subopt == 'A':
            print_songs(all_songs, rating_map, showid = True)
        elif subopt == 'B':
            print_songs(all_songs, rating_map, title_only = True)
        elif subopt == 'F':
            print_songs(all_songs, rating_map, fave = True)
        elif subopt == 'G':
            print_songs(all_songs, rating_map, get_genre = True)
```

* In your **song\_functions.py**, copy the `get_selection()` function given below - you will use this function as-is. This function is central to many of the menu options this program can perform. We have an option in the function parameters (`go_back`) that can be used if the user changes their mind and wants to return to the main menu.

```
######## LIST OPTION ########

def get_selection(action, suboptions, to_upper = True, go_back = False):
    """
    param: action (string) - the action that the user
            would like to perform; printed as part of
            the function prompt
    param: suboptions (dictionary) - contains suboptions
            that are listed underneath the function prompt.
    param: to_upper (Boolean) - by default, set to True, so
            the user selection is converted to upper-case.
            If set to False, then the user input is used
            as-is.
    param: go_back (Boolean) - by default, set to False.
            If set to True, then allows the user to select the
            option M to return back to the main menu

    The function displays a submenu for the user to choose from. 
    Asks the user to select an option using the input() function. 
    Re-prints the submenu if an invalid option is given.
    Prints the confirmation of the selection by retrieving the
    description of the option from the suboptions dictionary.

    returns: the option selection (by default, an upper-case string).
            The selection be a valid key in the suboptions
            or a letter M, if go_back is True.
    """
    selection = None
    if go_back:
        if 'm' in suboptions or 'M' in suboptions:
            print("Invalid submenu, which contains M as a key.")
            return None

    while selection not in suboptions:
        print(f"::: What would you like to {action.lower()}?")
        for key in suboptions:
            print(f"{key} - {suboptions[key]}")
        if go_back == True:
            selection = input(f"::: Enter your selection "
                              f"or press 'm' to return to the main menu\n> ")
        else:
            selection = input("::: Enter your selection\n> ")
        if to_upper:
            selection = selection.upper() # to allow us to input lower- or upper-case letters
        if go_back and selection.upper() == 'M':
            return 'M'
        
    if to_upper:    
        print(f"You selected |{selection}| to",
              f"{action.lower()} |{suboptions[selection].lower()}|.")
    else:
        print(f"You selected |{selection}| to",
          f"{action.lower()} |{suboptions[selection]}|.")
    return selection
```

* NOW: Define 3 new functions: `print_song()`, `print_songs()`, `get_written_date()`. 
    * Does that last one sound familiar? (it should from a prior chapter)
    * ⚠️ **Add the implementation based on the documentation provided below.**
    * ⚠️  See the example of the `print_song()` output provided below in the Sample Program Flow section.
    * you should have already added the `get_written_date()` function implementation from [LAB 7.18](https://learn.zybooks.com/zybook/UCSBCMPSCW8MatniFall2022/chapter/7/section/18)

1. List an **individual** song.
```
def print_song(song, rating_map, title_only = False, showid=False):
    """
    param: song (dict) - a single song dictionary
    param: rating_map (dict) - a dictionary object that is expected
            to have the string keys that correspond to the "rating"
            integer values stored in the song; the stored value is displayed for the
            rating field, instead of the numeric value.
    param: title_only (Boolean) - by default, set to False.
            If True, then only the name of the song is printed.
            Otherwise, displays the formatted song fields.
    param: showid (Boolean) - by default, set to False.
            If False, then the id number of the song is not displayed.
            Otherwise, displays the id number.

    returns: None; only prints the song values

    Helper functions:
    - get_written_date() to display the 'duedate' field
        You created a similar function in a previous lab.
    """
    # TO-DO: print some or all information of one song (dict),
    #              depending on the options in the parameters
    #    You have to ensure that you use f-strings with the following padding settings:
    #              pad your string labels with 9 spaces and justify right.
    #    To see what these should look like, see further below for example runs.
```

2. List all or some of the songs stored in the nested song dictionary. 

```
def print_songs(song_dict, rating_map, title_only = False, showid = False, fave = False, get_genre = False):
    """
    param: song_dict (dict) - a dictionary containing dictionaries with
            the song data
    param: rating_map (dict) - a dictionary object that is expected
            to have the integer keys that correspond to the "rating"
            integer values stored in the song; the stored value is displayed 
            for the rating field, instead of the numeric value.
    param: title_only (Boolean) - by default, set to False.
            If True, then only the title of the song is printed.
            Otherwise, displays the formatted song fields.
    param: showid (Boolean) - by default, set to False.
            If False, then the key (unique ID number) of the song is not displayed.
            Otherwise, displays the id number.
    param: fave (Boolean) - by default, set to False, and prints all songs.
            Otherwise, if it is set to True, prints only the songs marked as favorite.
            This parameter is meant to be used exclusive of get_genre
            (i.e. if fave=True, then get_genre should be False, and vice versa).
    param: get_genre (Boolean) - by default, set to False, and prints all songs.
            If set to True, then the function should ask the user for a
            genre keyword (string) and print only those songs that contain that string in its genre value.
            This parameter is meant to be used exclusive of fave (i.e. if fave=True, then get_genre should be False, and vice versa).
            NOTE: If a song has multiple instances of that genre keyword, you should only print the song once.

    returns: None; only prints the song values from the song_list

    Helper functions:
    - print_song() to print individual songs
    """
    print("*"*42)
    # Check to see if get_genre is True, so that you can ask for the genre keyword
   # Go through all the songs in the song dictionary:
    for ...: 
        # if not asking for favorites or specific genres: print everything
        if fave == False and ... :
            print_song(.....)
        # otherwise: if asking for favorites, print just those:
        elif fave and .... :
            print_song(.....)
        # otherwise: if asking for a specific genre, print just those:
        elif get_genre:
            # search all the songs' genres for the genre keyword
            # and print only those songs where that keyword appears in the genre value
            # NOTE: You should only print a song *once* 
            # even if the genre keyword appears more than once in it
            print_song(.....)

        # ... TO DO: fill in the missing parts of this function
```
Make sure that:
* the `fave` field correctly displays either all songs (setting is False - the default) or **only** songs that are marked as favorite (setting is True), depending on what was selected by the user in the main program. If none of the songs are marked as favorite, then nothing is printed.
* the `get_genre` field correctly displays either all songs (setting is False - the default) or **only** a specific genre (setting is True), depending on what was selected by the user in the main program. If the setting is True, then the function should ask the user for a genre  keyword(string) and print only those songs whose genre value contains this keyword in it. If the genre keyword given is not found in any of the songs, then nothing is printed.

Additionally, to make your lives easier, the `fave`  and `get_genre` fields are meant to be used (meaning, as arguments) exclusive of one another, i.e. if `fave`=`True`, then `get_genre` should be used with a `False` value, and vice versa. In other words, no one will be looking for favorites AND specific genres - just one or the other.


# Sample Program Flows for "List" Menu Options

1. Assuming the song dictionary that's hard-coded above, below is a sample program output for listing `A`ll Songs (full). Note the string padding for the strings like `"ARTIST"` or  `"ALBUM"`, etc...:

```
You selected option L to > List.
::: What would you like to list?
A - all songs - full
B - all songs - titles only
F - favorite songs
G - songs of a specific genre
::: Enter your selection
> a
You selected |A| to list |all songs - full|.
******************************************
      ID: 12332 |   TITLE: Cardigan
  ARTIST: Taylor Swift
  LENGTH: 03:59
   ALBUM: Folklore
   GENRE: Folk, Indie Rock
  RATING: Like
RELEASED: July 27, 2020
FAVORITE: True
******************************************
      ID: 14567 |   TITLE: Soul Meets Body
  ARTIST: Death Cab for Cutie
   ALBUM: Plans
   GENRE: Indie Pop, Indie Rock
  RATING: Love!
RELEASED: July 16, 2005
FAVORITE: True
******************************************
      ID: 78210 |   TITLE: Fake Love
  ARTIST: BTS
  LENGTH: 04:02
   GENRE: Hip Hop, Electro Pop, Korean Pop
  RATING: Neutral
RELEASED: May 18, 2018
FAVORITE: False
******************************************
      ID: 99105 |   TITLE: Foil
  ARTIST: 'Weird Al' Yankovic
  LENGTH: 02:22
   ALBUM: Mandatory Fun
   GENRE: Pop, Parody
  RATING: Love!
RELEASED: July 15, 2014
FAVORITE: True
******************************************
::: Press Enter to continue
```

2. Below is another sample program output for listing B (song titles only). Again, note the string padding for the strings like `"ARTIST"` or  `"ALBUM"`, etc...:
```
You selected |B| to list |all songs - titles only|.
******************************************
   TITLE: Cardigan
   TITLE: Soul Meets Body
   TITLE: Fake Love
   TITLE: Foil
::: Press Enter to continue
```

3. Here is a sample program output for listing F (favorite songs only):
```
You selected |F| to list |favorite songs|.
******************************************
   TITLE: Cardigan
  ARTIST: Taylor Swift
  LENGTH: 03:59
   ALBUM: Folklore
   GENRE: Folk, Indie Rock
  RATING: Like
RELEASED: July 27, 2020
FAVORITE: True
******************************************
   TITLE: Soul Meets Body
  ARTIST: Death Cab for Cutie
   ALBUM: Plans
   GENRE: Indie Pop, Indie Rock
  RATING: Love!
RELEASED: July 16, 2005
FAVORITE: True
******************************************
   TITLE: Foil
  ARTIST: 'Weird Al' Yankovic
  LENGTH: 02:22
   ALBUM: Mandatory Fun
   GENRE: Pop, Parody
  RATING: Love!
RELEASED: July 15, 2014
FAVORITE: True
******************************************
::: Press Enter to continue
```

4. Here is a sample program output for listing G (specific genre of songs). Note that the user is asked to input a genre (pop, in this example) and that the songs that are listed all have "pop" mentioned in their genres and never repeated.
```
You selected |G| to list |songs of a specific genre|.
******************************************
Enter genre:: pop
   TITLE: Soul Meets Body
  ARTIST: Death Cab for Cutie
   ALBUM: Plans
   GENRE: Indie Pop, Indie Rock
  RATING: Love!
RELEASED: July 16, 2005
FAVORITE: True
******************************************
   TITLE: Fake Love
  ARTIST: BTS
  LENGTH: 04:02
   GENRE: Hip Hop, Electro Pop, Korean Pop
  RATING: Neutral
RELEASED: May 18, 2018
FAVORITE: False
******************************************
   TITLE: Foil
  ARTIST: 'Weird Al' Yankovic
  LENGTH: 02:22
   ALBUM: Mandatory Fun
   GENRE: Pop, Parody
  RATING: Love!
RELEASED: July 15, 2014
FAVORITE: True
******************************************
::: Press Enter to continue
```
