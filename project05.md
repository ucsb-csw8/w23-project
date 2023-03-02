---
layout: default
title: Step 5 - "Edit" option
---

# {{page.title}}

New functions needed:
* `edit_song()`


Add the following branch to your **main program**; replace the ellipses with the appropriate values:
```
    elif opt == 'E':
        continue_action = 'y'
        while continue_action == 'y':
            if ... == {}: # TODO
                print("WARNING: There is nothing to edit!")
                break
            print("::: Song list:")
            print_songs(all_songs, rating_map, title_only = True, showid = True)
            print("::: Enter the song ID you wish to edit.")
            user_option = input("> ")
            if ...: # TODO - check to see if that ID is in the song dictionary
                subopt = get_selection("edit", all_songs[user_option], to_upper = False, go_back = True)
                if subopt == 'M': # if the user changed their mind
                    break
                print(f"::: Enter a new value for the field |{...}|") # TODO
                field_info = input("> ")
                result = edit_song(all_songs, user_option, rating_map, subopt, field_info, ...) #TODO
                if type(result) == dict:
                    print(f"Successfully updated the field |{...}|:")  # TODO
                    print_song(result, ...)  # TODO
                else: # edit_song() returned an error
                    print(f"WARNING: invalid information for the field |{...}|!")  # TODO
                    print(f"The song was not updated.")
            else: # song ID is incorrect/invalid
                print(f"WARNING: |{...}| is an invalid song ID!")  # TODO
                           
            print("::: Would you like to edit another song?", end=" ")
            continue_action = input("Enter 'y' to continue.\n> ")
            continue_action = continue_action.lower()      
            # ----------------------------------------------------------------
```

Define a new function `edit_song()` to edit the song dictionary appropriately:
```
def edit_song(song_dict, songid, rating_map, field_key, field_info, allkeys):
    """
    param: song_dict (dict) - dictionary of all songs
    param: songid (str) - a string that is expected to contain the key of
            a song dictionary (same value as its unique id)
    param: rating_map (dict) - a dictionary object that is expected
            to have the integer keys that correspond to the "rating"
            integer values stored in the song; the stored value is displayed 
            for the rating field, instead of the numeric value.
    param: field_key (string) - a text expected to contain the name
            of a key in the song dictionary whose value needs to 
            be updated with the value from field_info
    param: field_info (string) - a text expected to contain the value
            to validate and with which to update the dictionary field
            song_dict[field_key]. The string gets stripped of the
            whitespace and gets converted to the correct type, depending
            on the expected type of the field_key.
    param: allkeys (key_list) - a key_list of all keys in the song dictionary.

    The function first calls some of its helper functions
    to validate the provided field.
    If validation succeeds, the function proceeds with the edit.

    return:
    If song_dict is empty, return 0.
    If the field_key is not a string, return -1.
    If the remainder of the validation passes, return the dictionary song_dict[songid].
    Otherwise, return the field_key.

    Helper functions:
    The function calls the following helper functions depending on the field_key:
    - is_valid_title()
    - is_valid_time()
    - is_valid_date()
    - is_valid_uid()
    """
```

# Sample Program Workflow

Below is a demo of editing with an incorrect value (bad rating value):

```
You selected option E to > Edit.
::: Song list:
******************************************
      ID: 12332 |   TITLE: Cardigan
      ID: 14567 |   TITLE: Soul Meets Body
      ID: 78210 |   TITLE: Fake Love
      ID: 99105 |   TITLE: Foil
::: Enter the song ID you wish to edit.
> 78210
::: What would you like to edit?
title - Fake Love
artist - BTS
length - 04:02
album - 
genre - ['hip hop', 'electro pop', 'Korean pop']
rating - 3
released - 05/18/2018
favorite - False
uid - 78210
::: Enter your selection or press 'M' to return to the main menu
> rating
You selected |rating| to edit |3|.
::: Enter a new value for the field |rating|
> 22
WARNING: invalid information for the field |rating|!
The song was not updated.
::: Would you like to edit another song? Enter 'y' to continue.
> 
```

This is a demo of adding that same rating correctly:

```
You selected option E to > Edit.
::: Song list:
******************************************
      ID: 12332 |   TITLE: Cardigan
      ID: 14567 |   TITLE: Soul Meets Body
      ID: 78210 |   TITLE: Fake Love
      ID: 99105 |   TITLE: Foil
::: Enter the song ID you wish to edit.
> 78210
::: What would you like to edit?
title - Fake Love
artist - BTS
length - 04:02
album - 
genre - ['hip hop', 'electro pop', 'Korean pop']
rating - 3
released - 05/18/2018
favorite - False
uid - 78210
::: Enter your selection or press 'M' to return to the main menu
> rating
You selected |rating| to edit |3|.
::: Enter a new value for the field |rating|
> 2
Successfully updated the field |rating|:
 TITLE: Fake Love
  ARTIST: BTS
  LENGTH: 04:02
   GENRE: Hip Hop, Electro Pop, Korean Pop
  RATING: Dislike
RELEASED: May 18, 2018
FAVORITE: False
******************************************
::: Would you like to edit another song? Enter 'y' to continue.
> 
```