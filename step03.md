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
*'. We will refer to it as `restaurant_menu_list`. This **list** will contain **dictionaries** with each menu item's information.

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

In this project, for the ease of testing, we will **hard-code** a list  of menu item information at the top of the **main program**, after the dictionary `the_menu`. We will refer to it as `restaurant_menu_list`. This is just an example dictionary containing 4 menu item information dictionaries that can be used to test our system as we develop it. You can add more of your own examples as longs as they adhere to the correct formats and types of the dictionary values.

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

* Create a variable to hold a nested dictionary of menu item information data (dictionaries) at the top of your **main program**. We will refer to it as `restaurant_menu_list`.

* Additionally, you need to add two more dictionaries to your **main program**:
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

* Next, add the following code to your **main program** to implement the listing of the menu items - you do not need to change it as shown below.
  * Note that there are new functions `list_helper()`, `get_selection()` that needs to be implemented and that is _also_ given to you after the code below.

```python
    elif opt == 'L':
        list_helper(list_menu, restaurant_menu_list, spicy_scale_map)
```

* In your **functions.py**, copy the `list_helper` and `get_selection()` functions given below - you will use these functions as-is. These functions are central to many of the menu options this program can perform. We have an option in the function parameters (`go_back`) that can be used if the user changes their mind and wants to return to the main menu.

```python

def list_helper(list_menu, restaurant_menu_list, spicy_scale_map):
    if restaurant_menu_list == {}:
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

* NOW: Define 2 new functions: `print_dish()`, `print_restaurant_menu()`. 

1. List an **individual** menu item.

```python
def print_dish(dish, spicy_scale_map, name_only=False):
    # TODO : is spicy_scale_map used in this function?
    """
    restaurant_menu (dict) - a dictionary object that is expected to contain the following keys:
            - "dish": dish's name
            - "calories": calories for this dish
            - "price": price of this dish
            - "is_vegetarian": boolean whether this dish is for vegetarian
            - "spicy_level": integer that represents the level of spiciness
    param: spicy_scale_map (dict) - a dictionary object that is expected
            to have the integer keys that correspond to the "level of spiciness."
            values for each corresponding key are string description of the 
            level of spiciness
    param: name_only (Boolean) - by default, set to False.
            If False, then only the name of the dish is printed.
            Otherwise, displays the formatted restaurant menues.
    returns: None; only prints the restaurant menu
    """
    # TO-DO: print some or all information of one menu item (dict),
    #              depending on the options in the parameters
    #    You have to ensure that you use f-strings with the following padding settings:
    #              pad your string labels with 9 spaces and justify right.
    #    To see what these should look like, see further below for example runs.
```

2. List all or some of the menu items stored in the restaurant_menu list. 

```python
def print_restaurant_menu(restaurant_menu, spicy_scale_map, name_only, show_idx, start_idx, vegetarian_only):
    """
    restaurant_menu (list) - a list object that is expected
            to have the dictionaries for each dish that the restaurant 
            offers.
    param: spicy_scale_map (dict) - a dictionary object that is expected
            to have the integer keys that correspond to the "level of spiciness."
    param: name_only (Boolean)
            If True, then only the name of the dish is printed.
            Otherwise, displays the formatted restaurant menu.
    param: show_idx (Boolean)
            If False, then the index of the menu is not displayed.
            Otherwise, displays the "{idx + start_idx}." before the
            dish name.
    param: start_idx (int)
            an expected starting value for idx that
            gets displayed for the first dish, if show_idx is True.
    param:  vegetarian_only (Boolean)
            By default, prints all dishes, regardless of their
            is_vegetarian status ("yes/no" field status).
            Otherwise, it displays only the dishes with
            "is_vegetarian" status as "yes.
    returns: None; only prints the restaurant menu
    """
   # Go through all the dishes in the restaurant menu:
    print("*"*42)
    for ...: 
        # if vegetarian_only is True and the dish is not vegetarian, skip
        if vegetarian_only == True:
            if ..... :
                .....
        # if the index of the task needs to be displayed (show_idx is True), print dish index only
        if show_idx == True:  
            print(.....)
        # if name_only is False
        print_dish(...)

    Helper functions:
    - print_dish() to print individual menu items
    """
```
Make sure that:
* the `vegetarian_only` field correctly displays either all menu items (setting is False - the default) or **only** menu items that are vegetarian (setting is True), depending on what was selected by the user in the main program. If none of the menu items are marked as vegetarian, then nothing is printed.

# Sample Program Flows for "List" Menu Options

1. Assuming the restaurant menu list that's hard-coded above, below is a sample program output for listing `complete menu`.

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

2. Below is another sample program output for listing V (vegetarian menu items only).

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

