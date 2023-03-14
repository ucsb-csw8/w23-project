---
layout: default
title: Step 4 - "Add" option
nav_order: 40
---

# {{page.title}}

The functions needed (from Project Component labs of Week 7 - [LAB 7.20](https://learn.zybooks.com/zybook/UCSBCMPSCW8Winter2023/chapter/7/section/20)):
* `get_new_menu_dish()`
* `is_num()`
* `is_valid_name()`
* `is_valid_calories()`
* `is_valid_price()`
* `is_valid_is_vegetarian()`
* `is_valid_spicy_level()`

**Hint**: As a reminder: the function `get_new_menu_dish()` checks all of the values passed in.  As per the instructions in 
See the [LAB 7.20](https://learn.zybooks.com/zybook/UCSBCMPSCW8Winter2023/chapter/7/section/20)):

* If the length of the list is wrong, return the length of the list.
* If one particular field is invalid, return a tuple of its name and the value it had, e.g. `('price', '$xxx')` or
(`spicy_level`,`idk, maybe`).  

Note that this is not documented in the docstring for the function in [LAB 7.20](https://learn.zybooks.com/zybook/UCSBCMPSCW8Winter2023/chapter/7/section/20)) (it arguably should have been), but now it has been brought to your attention.

Add your solutions to **functions.py** file. Add your `assert` statements **tests.py**.

Example of asserts you could have in your **test file**:
```
assert is_valid_name("a") == False
assert is_valid_name("bo") == False
assert is_valid_name(42) == False
assert is_valid_name(["soup"]) == False
assert is_valid_name("soup") == True
```

# `print_dish()`
Define a new function `print_dish()` that will list an **individual** menu item.

```python
def print_dish(dish, spicy_scale_map, name_only=False):
    """
    param: dish (dict) - a dictionary object that is expected to contain the following keys:
            - "name": dish's name
            - "calories": calories for this dish
            - "price": price of this dish
            - "is_vegetarian": boolean whether this dish is for vegetarian
            - "spicy_level": integer that represents the level of spiciness
    param: spicy_scale_map (dict) - a dictionary object that is expected
            to have the integer keys that correspond to the "level of spiciness."
            values for each corresponding key are string description of the
            level of spiciness
    param: name_only (Boolean) - by default, set to False.
            If True, then only the name of the dish is printed.
            Otherwise, displays the formatted restaurant menues.
    returns: None; only prints the restaurant menu item
    """
```

Add the following branch to your **main program**; replace the ellipses with the appropriate values. See below for sample run outputs.
```python
    elif opt == 'A':
        add_helper(...)
```

```python

def add_helper(restaurant_menu_list, spicy_scale_map):
    continue_action = 'y'
    while continue_action == 'y':
        print("::: Enter each required field, separated by commas.")
        # * `name` : name of the dish
        #     * `calories`: number of calories per serving
        #     * 'is_vegetarian' : if the item is vegetarian
        #     * `price` : price of the item
        #     * 'spicy_level' : 1 - 4
        print("::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )")
        dish_data = input("> ")  # TODO: get and process the data into a list
        dish_values = dish_data.split(",")
        result_dict = get_new_menu_dish(..., spicy_scale_map)  # TODO: attempt to create a new dish for the menu
        if type(result_dict) == dict:
            restaurant_menu_list.append(...)  # TODO: add a new dish to the list of dish menus
            print(f"Successfully added a new dish!")
            print_dish(result_dict, spicy_scale_map)
        elif type(result_dict) == int:
            print(f"WARNING: invalid number of fields!")
            print(f"You provided {result_dict}, instead of the expected 5.\n")
        else:
            print(f"WARNING: invalid dish field: {result_dict}\n")

        print("::: Would you like to add another dish?", end=" ")
        continue_action = input("Enter 'y' to continue.\n> ")
        continue_action = continue_action.lower()
```


# Sample Program Flow

1. Below is a demo of adding an incorrect menu dish:

   ```
    You selected option A to > Add.
    ::: Enter each required field, separated by commas.
    ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
    > yum bowl, 100, 5.99, yes, 0
    WARNING: invalid dish field: ('spicy_level', '0')

   ```

2. Here is a demo of adding a different incorrect dishes:

   ```
    ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
    > um, 5, 5, no, 1
    WARNING: invalid dish field: ('name', 'um')
    ...

    ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
    > ,,,,,
    WARNING: invalid number of fields!
    You provided 6, instead of the expected 5.
    ...

    ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
    > sandwich
    WARNING: invalid number of fields!
    You provided 1, instead of the expected 5.

   ```

3. Finally, here's a demo of adding a new menu dish successfully:

   ```
    ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
    > Soup, 100, 5, yes, 1
    Successfully added a new dish!
    SOUP
    * Calories: 100
    * Price: 5.0
    * Is it vegetarian: yes
    * Spicy level: Not spicy

   ```

4. After successfully adding a new menu dish, you should be able to see it in the List menu option.

# Checkpoint 1

After finishing this step, you are ready to submit code for Checkpoint 1.

See the [Checkpoint 1 instructions](/w23-project/checkpoint1/) for more information
