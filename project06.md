---
layout: default
title: Step 6 - "Delete" option
---

# {{page.title}}


New functions needed:
* `delete_song()`

You will need to refer to the `delete_item()` function (from [LAB 8.14](https://learn.zybooks.com/zybook/UCSBCMPSCW8MatniFall2022/chapter/8/section/14)).
This is very similar (but not the same) as it was in the previous lab.

```
def delete_song(song_dict, songid):
    """
    param: song_dict - a dictionary of songs (dict of dict)
    param: songid (str) - a string that is expected to
            contain the key to a song dictionary (i.e. same as its unique ID)

    The function first checks if the dictionary of songs is empty.
    The function then validates the song ID to verify
    that the provided ID key can access an element from song_dict
    On success, the function saves the item's "title" from song_dict
    and returns that string ("title" value)
    after the item is deleted from song_dict.

    returns:
    If the input dictionary is empty, return 0.
    If the ID is not valid (i.e. not found in the song_dict), return -1.
    Otherwise, on success, the entire song is removed from song_dict
    and the function returns the title of the deleted song.
    """
```

Your main task is to figure out how to assemble the **main program** portion for correctly deleting an item. You can deduce this by going through the Sample Program Flow examples.

The main program portion should start off with:
```
    elif opt == 'D':
       continue_action = 'y'
       while continue_action == 'y':
    #TODO : the rest of it...
```

# Sample Program Flow

1. Deleting ALL songs. Note that the user can only do this by selecting "X" (only the upper case "X") and then by confirming with "Yes" (not "Y", not "yes", ...)

```
You selected option D to > Delete.
******************************************
      ID: 12332 |   TITLE: Cardigan
      ID: 14567 |   TITLE: Soul Meets Body
      ID: 78210 |   TITLE: Fake Love
      ID: 99105 |   TITLE: Foil
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
```

You can check that every song got deleted by next going to the main menu, and selecting "L"ist:
```
> L
You selected option L to > List.
WARNING: There is nothing to display!
::: Press Enter to continue
```
2. Deleting one song - example below shows what happens if the **wrong** song ID is used, but then the user is given another chance to delete and they use the **correct** song ID:

```
You selected option D to > Delete.
******************************************
      ID: 12332 |   TITLE: Cardigan
      ID: 14567 |   TITLE: Soul Meets Body
      ID: 78210 |   TITLE: Fake Love
      ID: 99105 |   TITLE: Foil
Which song would you like to delete?
X - Delete all songs at once
::: OR Enter the number corresponding to the song ID
::: OR press 'M' to cancel and return to the main menu.
> 12333
WARNING: |12333| is an invalid song ID!
::: Would you like to delete another song? Enter 'y' to continue.
> y
******************************************
      ID: 12332 |   TITLE: Cardigan
      ID: 14567 |   TITLE: Soul Meets Body
      ID: 78210 |   TITLE: Fake Love
      ID: 99105 |   TITLE: Foil
Which song would you like to delete?
X - Delete all songs at once
::: OR Enter the number corresponding to the song ID
::: OR press 'M' to cancel and return to the main menu.
> 12332
Success!
Deleted the song |Cardigan|
::: Would you like to delete another song? Enter 'y' to continue.
> n
::: Press Enter to continue
```

Note that the user CAN keep choosing to enter 'y' at the "Would you like to delete another song?..." prompt and be able to go back to the start of the delete menu choices. This would allow them to keep deleting songs one by one.

Again ,you can check that the song example from above (Cardigan) got deleted by next going to the main menu, and selecting "L"ist:
```
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
 TITLE: Soul Meets Body
 TITLE: Fake Love
 TITLE: Foil
::: Press Enter to continue
```

3. The "go back to the main menu" option (M):
```
You selected option D to > Delete.
******************************************
      ID: 14567 |   TITLE: Soul Meets Body
      ID: 78210 |   TITLE: Fake Love
      ID: 99105 |   TITLE: Foil
Which song would you like to delete?
X - Delete all songs at once
::: OR Enter the number corresponding to the song ID
::: OR press 'M' to cancel and return to the main menu.
> m
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
> 
```

4. Example of nothing gets deleted (i.e. you already deleted every song and now you select delete again).
```
> d
You selected option D to > Delete.
WARNING: There is nothing to delete!
::: Press Enter to continue
```

