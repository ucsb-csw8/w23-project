---
layout: default
title: Step 3 - "List" option
---

# {{page.title}}



# What is "menu information"?

In this project, **one menu items's information** is a **dictionary** object that is guaranteed to have the following keys:

* `"name"`: a string with the menu item's name.
* `"calories"`: an integer with the number of calories in the menu item.
* `"price"`: a float with the menu item's price using the format 00.00.
* `"is_vegetarian"`: a string with value "yes" or "no" for if the menu item is vegetarian.
* `"spicy_level"`: an integer from 1 to 4, representing the menu item's spice level.

Here is an example of what a dictionary with a **single menu item's information** could look like:

```python
{
    "name": "burrito",
    "calories": 500,
    "price": 12.90,
    "is_vegetarian": "yes",
    "spicy_level": 2
}
```

In this project, for the ease of testing, we will **hard-code** a list of menu item information at the top of the **main program**, after the dictionary `the_menu`. We will refer to it as `restaurant_menu_list`. Below is just an example list containing the menu item information dictionaries that can be used to test our system as we develop it. We encourage you to add more of your own examples as long as they adhere to the correct formats and types of the dictionary values.

```python
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

First, create a variable `restaurant_menu_list` to hold the list of menu items (stored as as list of dictionaries, as shown above) at the top of your **main program**. We will refer to it as `restaurant_menu_list`.

Additionally, you need to add two more variables to your **main program**:
* `list_menu` will contain the "List" menu sub-options
* `spicy_scale_map` will contain the mapping of the spicy_level values, as integers, to a string for the name of the spice level

```python

    list_menu = {
        "A": "complete menu",
        "V": "vegetarian dishes only",
    }

    spicy_scale_map = {
        1: "Not spicy",
        2: "Low key spicy",
        3: "Hot",
        4: "Diabolical",
    }
```

Next, add the following code to your **main program** to implement the listing of the menu items - you do not need to change it.

Note that there are new functions `list_helper()`, `get_selection()` that are _also_ given to you after the code below.

```python
    elif opt == 'L':
        list_helper(list_menu, restaurant_menu_list, spicy_scale_map)
```

In your **functions.py**, copy the `list_helper` and `get_selection()` functions given below - you will use these functions as-is. These functions are central to many of the menu options this program can perform. We have an option in the function parameters (`go_back`) that can be used if the user changes their mind and wants to return to the main menu.

```python

def list_helper(list_menu, restaurant_menu_list, spicy_scale_map):
    if len(restaurant_menu_list) == 0:
        print("WARNING: There is nothing to display!")
        # Pause before going back to the main menu
        input("::: Press Enter to continue")
    else:
        subopt = get_selection("List", list_menu)
        if subopt == 'A':
            print_restaurant_menu(restaurant_menu_list, spicy_scale_map, show_idx=True, start_idx=1)
        elif subopt == 'V':
            print_restaurant_menu(restaurant_menu_list, spicy_scale_map, show_idx=True, start_idx=1, vegetarian_only=True)

######## LIST OPTION ########

def get_selection(action, suboptions, to_upper=True, go_back=False):
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
        print(f"::: What field would you like to {action.lower()}?")
        for key in suboptions:
            print(f"{key} - {suboptions[key]}")
        if go_back:
            selection = input(f"::: Enter your selection "
                              f"or press 'm' to return to the main menu\n> ")
        else:
            selection = input("::: Enter your selection\n> ")
        if to_upper:
            selection = selection.upper()  # to allow us to input lower- or upper-case letters
        if go_back and selection.upper() == 'M':
            return 'M'

    print(f"You selected |{selection}| to",
          f"{action.lower()} |{suboptions[selection]}|.")
    return selection
```

# Add the printing function

## `print_restaurant_menu()`

The function `print_restaurant_menu()` will list all or some of the menu items stored in the `restaurant_menu_list`. 

Use the implementation from [LAB 7.19](https://learn.zybooks.com/zybook/UCSBCMPSCW8Winter2023/chapter/7/section/19).

```python
def print_restaurant_menu(restaurant_menu, spicy_scale_map, name_only=False, show_idx=True, start_idx=0, vegetarian_only=False):
    """
    param: restaurant_menu (list) - a list object that holds the dictionaries for each dish
    param: spicy_scale_map (dict) - a dictionary object that is expected
            to have the integer keys that correspond to the "level of spiciness."
    param: name_only (Boolean)
            If False, then only the name of the dish is printed.
            Otherwise, displays the formatted dish information.
    param: show_idx (Boolean)
            If False, then the index of the menu is not displayed.
            Otherwise, displays the "{idx + start_idx}." before the
            dish name, where idx is the 0-based index in the list.
    param: start_idx (int)
            an expected starting value for idx that
            gets displayed for the first dish, if show_idx is True.
    param:  vegetarian_only (Boolean)
            If set to False, prints all dishes, regardless of their
            is_vegetarian status ("yes/no" field status).
             If set to True , display only the dishes with
            "is_vegetarian" status set to "yes".
    returns: None; only prints the restaurant menu
    """
   # Go through the dishes in the restaurant menu:
    for ...: 
        # if vegetarian_only is True and the dish is not vegetarian, skip
        if vegetarian_only and ...:
            ..... 

        # if the index of the task needs to be displayed (show_idx is True), print dish index only
        if show_idx == True:  
            print(.....)

        # print the name of the dish

        # if name_only is False
        if not name_only:
            print(.....)
            print(.....)
            print(.....)
            print(.....)
    """
```

# Notes 

Make sure that the `vegetarian_only` field correctly displays either all menu items (setting is False - the default) or **only** menu items that are vegetarian (setting is True), depending on what was selected by the user in the main program. 

If none of the menu items are marked as vegetarian, then nothing is printed.

# Sample Program Flows for "List" Menu Options

1.  Assuming the restaurant menu list that's hard-coded above, below is a sample program output for listing `complete menu`.

    ```
    ==========================
    What would you like to do?
    L - List
    A - Add
    U - Edit
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
    ::: Press Enter to continue
    ```

2.  Below is another sample program output for listing V (vegetarian menu items only).

    ```
    You selected |V| to list |vegetarian dishes only|.
    ------------------------------------------
    1. BURRITO
    * Calories: 500
    * Price: 12.9
    * Is it vegetarian: yes
    * Spicy level: Low key spicy

    ------------------------------------------
    ::: Press Enter to continue
    ```

