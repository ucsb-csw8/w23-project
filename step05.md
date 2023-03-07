---
layout: default
title: Step 5 - "Add" option
---

# {{page.title}}

New functions needed:
* `get_new_menu_dish()`
* `print_dish()`
* `is_valid_name()`
* `is_valid_calories()`
* `is_valid_price()`
* `is_valid_is_vegetarian()`
* `is_valid_spicy_level()`

Add the following branch to your **main program**; replace the ellipses with the appropriate values. See below for sample run outputs.
```python
    elif opt == 'A':
        continue_action = 'y'
        while continue_action == 'y':
			print("::: Enter each required field, separated by commas.")
			print("::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )")
			# TODO: Get user inputs for the dish information
			# * `name` : name of the dish
			# * `calories`: number of calories per serving
			# * 'is_vegetarian' : if the item is vegetarian
			# * `price` : price of the item
			# * 'spicy_level' : 1 - 4
			result = get_new_menu_dish(...) # TODO: attempt to create a new dish for the menu
			if type(result_dict) == dict:
				... # TODO: add a new dish to the list of dish menus
				print(f"Successfully added a new dish!")
				print_dish(result, ...)
			elif type(result_dict) == int:
				print(f"WARNING: invalid number of fields!")
				print(f"You provided {result}, instead of the expected 5.\n")
			else:
				print(f"WARNING: invalid dish field: {result}\n")
			print("::: Would you like to add another dish?", end=" ")
			continue_action = input("Enter 'y' to continue.\n> ")
			continue_action = continue_action.lower()
			# ----------------------------------------------------------------
```

In your **functions file**, define `get_new_menu_dish()` that takes 2 parameters: a list of fields to check for a new dish, a dictionary that indicates spicy scale of a dish. See more details below.
```python
def get_new_menu_dish(..., ...,): 
    """
	Validate each parameter starting from "name" and until "spicy_level"
	If one of them fails, return a tuple containing the name of the incorrect parameter and its value
	e.g., ("name", "Mu") if "name" is not 3-25 characters long
	or ("is_vegetarian", "none") if that field is not set to boolean.
	If all validations pass, return the dictionary with the dish fields
	correctly set to the parameters.
    """
```
The function **returns** different types of values, _depending on whether it succeeds or fails_.

## Validations

The function has to first validate some things

* The entire input list has to be made up of strings. 
   * If one element of them is invalid, then `get_new_menu_dish()` has to return a tuple containing the error message string `"type"` and the value of the invalid element.

* The `name` value has to be a string that's at least 3 characters long and at most 25 characters long. The function calls the helper function `is_valid_name()` to check this. 
   * This helper function returns a Boolean value. 
   * If the value is invalid, then `get_new_menu_dish()` has to return a tuple containing the message string `"name"` and the invalid `name` value.

* The `calories` value has a string that is expected to be an integer to represent calories of the dish. The function calls the helper function `is_valid_calories()` to check this. 
   * This helper function returns a Boolean value. 
   * If the value is invalid, then `get_new_menu_dish()` has to return a tuple containing the message string `"calories"` and the invalid `calories` value.

* The `price` value has a string that contains a float number to represent the price of the dish. The function calls the helper function `is_valid_price()` to check this.
   * This helper function returns a Boolean value.
   * If the value is invalid, then `get_new_menu_dish()` has to return a tuple containing the message string `"price"` and the invalid `price` value.``

* The `is_vegetarian` value has to be a string that either "yes" or "no". The function calls the helper function `is_is_valid_vegetarian()` to check this.
   * This helper function returns a Boolean value.
   * If the value is invalid, then `get_new_menu_dish()` has to return a tuple containing the message string "is_vegetarian" and the invalid `is_vegetarian` value. 

* The `spicy_level` value has to be a string that is a digit contained in `spicy_scale_map`. 
   * If the value is invalid, then `get_new_menu_dish` has to return a tuple containing the message string `"spicy_level"` and the invalid `spicy_level` value.

## Creating a new dictionary item

Once validation is taken care of, then the values passed into `get_new_menu_dish()` through its list parameter, must be added as values to a **new** dictionary with the 5 menu item keys (i.e. "name", "calories", "price", etc...)

* **Important**: make sure when you add these values that they are added as the correct data type.
* The new dictionary gets **returned** at the conclusion of this process.

The first input parameter is a **list** of all needed menu item dictionary values stored **as strings**: 
   * The order of the fields is ** name, calories, price, is_vegetarian, spicy_level.**
   * If the provided field values are valid, return a new dictionary:

```python
{
    "name": ...,  # str
    "calories": ..., # int
    "price": ...  # float
    "is_vegetarian": ...,  # str
    "spicy_level": ...    # int
}
```

Note that  `get_new_menu_dish()` relies on several helper functions that validate different dish fields. 
The helper functions will need to be added first, before defining `get_new_menu_dish()`.

⚠️ Pay close attention to the number of parameters and their types!

Example of asserts you could have in your **test file**:
```
assert type(dish['name']) is str
assert len(dish['name']) >= 3 and len(dish['name']) <= 25
assert type(dish['price']) is float
```


# Sample Program Flow

1. Below is a demo of adding an incorrect menu dish:

   ```
   ::: Enter a menu option
   > A
   > You selected option A to > Add.
   ::: Enter each required field, separated by commas.
   ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
   > burrito, 500, 12.9, false, 3
   WARNING: invalid dish field: ('is_vegetarian', 'false')
   
   ::: Would you like to add another dish? Enter 'y' to continue.
   > 
   ```

2. Here is a demo of adding a different incorrect menu dish:

   ```
   ::: Enter a menu option
   > A
   > You selected option A to > Add.
   ::: Enter each required field, separated by commas.
   ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
   > burrito, 500, 12.9, yes, 10
   WARNING: invalid dish field: ('spicy_level', '10')
      
   ::: Would you like to add another dish? Enter 'y' to continue.
   >
   ```

3. Finally, here's a demo of adding a new menu dish successfully:

   ```
   ::: Enter a menu option
   > A
   > You selected option A to > Add.
   ::: Enter each required field, separated by commas.
   ::: name of the dish, calories, price, is it vegetarian ( yes | no ), spicy_level ( 1-4 )
   > rice bowl, 400, 14.9, no, 3

   Successfully added a new dish!
   RICE BOWL
   * Calories: 400
   * Price: 14.9
   * Is it vegetarian: no
   * Spicy level: Hot

   ::: Would you like to add another dish? Enter 'y' to continue.
   >
   ```

4. After successfully adding a new menu dish, you should be able to see it in the List menu option. For example:

   ```
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
   1. RICE BOWL
   * Calories: 400
   * Price: 14.9
   * Is it vegetarian: no
   * Spicy level: Hot

   ------------------------------------------ 
   ::: Press Enter to continue
   ```

