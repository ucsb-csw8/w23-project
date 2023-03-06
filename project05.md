---
layout: default
title: Step 5 - "Edit" option
---

# {{page.title}}

New functions needed:
* `update_helper()`
* `is_valid_index()`
* `update_menu_dish()`

Add the following branch to your **main program**
```
    elif opt == 'U':
        update_helper(restaurant_menu_list, spicy_scale_map)
```

Define a new function update_helper() as follows, replacing the ellipses with the appropriate values:
```

def update_helper(restaurant_menu_list, spicy_scale_map):
    continue_action = 'y'
    while continue_action == 'y':
        if ... == ...: #TODO
            print("WARNING: There is nothing to update!")
            break
        print("::: Which dish would you like to update?")
        print_restaurant_menu(restaurant_menu_list, spicy_scale_map, name_only=True, show_idx=True, start_idx=1)
        print("::: Enter the number corresponding to the dish.")
        user_option = input("> ")
        if ...: #TODO - check to see if the number is valid
            dish_idx = int(user_option) - 1
            subopt = get_selection("update", restaurant_menu_list[dish_idx], to_upper=False, go_back=True)
            if subopt == 'M':  # if the user changed their mind
                break
            print(f"::: Enter a new value for the field |{...}|") # TODO
            field_info = input("> ")
            result = update_menu_dish(...) #TODO
            if type(result) == dict:
                print(f"Successfully updated the field |{...}|:") # TODO
                print_dish(result, ...)  # TODO
            else:  # update_menu_dish() returned an error
                print(f"WARNING: invalid information for the field |{...}|!") # TODO
                print(f"The menu was not updated.")
        else:  # is_valid_index() returned False
            print(f"WARNING: |{...}| is an invalid dish number!") # TODO

        print("::: Would you like to update another menu dish?", end=" ")
        continue_action = input("Enter 'y' to continue.\n> ")
        continue_action = continue_action.lower()
        # ---------------------------------------------------------------
 ```

Define two new functions `is_valid_index` and `update_menu_dish()` to edit the menu dictionary appropriately:

```
def is_valid_index(idx, in_list, start_idx=0):
    """
    param: idx (str) - a string that is expected to
            contain an integer index to validate
    param: in_list - a list that the idx indexes
    param: start_idx (int) - by default, set to 0;
            an expected starting value for idx that
            gets subtracted from idx for 0-based indexing

    The function checks if the input string contains
    only digits and verifies that (idx - start_idx) is >= 0,
    which allows to retrieve an element from in_list.

    returns:
    - True, if idx is a numeric index >= start_idx
    that can retrieve an element from in_list.
    - False if idx is not a string that represents an
    integer value, if int(idx) is < start_idx,
    or if it exceeds the size of in_list.
    """
```

```
def update_menu_dish(restaurant_menu_list, idx, spicy_scale_map, field_key, field_info, start_idx=0):
    """
    param: restaurant_menu_list (list) - a menu that contains
            a list of dishes
    param: idx (str) - a string that is expected to contain an integer
            index of a restaurant in the input list
    param: spicy_scale_map (dict) - a dictionary that contains the mapping
            between the integer spiciness value (key) to its representation
            (e.g., key 1 might map to the priority value "non spicy")
            Needed if "field_key" is "priority" to validate its value.
    param: field_key (string) - a text expected to contain the name
            of a key in the info_list[idx] dictionary whose value needs to
            be updated with the value from field_info
    param: field_info (string) - a text expected to contain the value
            to validate and with which to update the dictionary field
            info_list[idx][field_key]. The string gets stripped of the
            whitespace and gets converted to the correct type, depending
            on the expected type of the field_key.
    param: start_idx (int) - by default, set to 0;
            an expected starting value for idx that
            gets subtracted from idx for 0-based indexing
    The function first calls one of its helper functions
    to validate the idx and the provided field.
    If validation succeeds, the function proceeds with the update.
    return:
    If info_list is empty, return 0.
    If the idx is invalid, return -1.
    If the field_key is invalid, return -2.
    If validation passes, return the dictionary info_list[idx].
    Otherwise, return the field_key.
    Helper functions:
    The function calls the following helper functions:
    - is_valid_index()
     Depending on the field_key, it also calls:
-    - is_valid_name()
-    - is_valid_calories()
-    - is_valid_price()
-    - is_valid_is_vegetarian()
-    - is_valid_spicy_level()
    """
```

# Sample Program Workflow

Below is a demo of editing with an incorrect value (bad rating value):
```
You selected option U to > Edit.
::: Which dish would you like to update?
------------------------------------------
1. BURRITO
2. RICE BOWL
3. MARGHERITA
------------------------------------------
::: Enter the number corresponding to the dish.
> 1
::: What field would you like to update?
name - burrito
calories - 500
price - 12.9
is_vegetarian - yes
spicy_level - 2
::: Enter your selection or press 'm' to return to the main menu
> spicy_level
You selected |spicy_level| to update |2|.
::: Enter a new value for the field |spicy_level|
> 42
WARNING: invalid information for the field |spicy_level|!
The menu was not updated.
::: Would you like to update another menu dish? Enter 'y' to continue.
>
```

This is a demo of editing that same field correctly:
```
You selected option U to > Edit.
::: Which dish would you like to update?
------------------------------------------
1. BURRITO
2. RICE BOWL
3. MARGHERITA
------------------------------------------
::: Enter the number corresponding to the dish.
> 1
::: What field would you like to update?
name - burrito
calories - 500
price - 12.9
is_vegetarian - yes
spicy_level - 3
::: Enter your selection or press 'm' to return to the main menu
> spicy_level
You selected |spicy_level| to update |3|.
::: Enter a new value for the field |spicy_level|
> 1
Successfully updated the field |spicy_level|:
BURRITO
* Calories: 500
* Price: 12.9
* Is it vegetarian: yes
* Spicy level: Not spicy

::: Would you like to update another menu dish? Enter 'y' to continue.
>
```
