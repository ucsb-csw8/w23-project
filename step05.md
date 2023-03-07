---
layout: default
title: Step 5 - "Delete" option
---

# {{page.title}}


New functions needed:
* `delete_dish()`

Refer to the `delete_item()` function (from [LAB 8.14](https://learn.zybooks.com/zybook/UCSBCMPSCW8Winter2023/chapter/8/section/14)) to see how to implement the function below.
This is very similar (but not the same) as it was in the Week 8 lab.

```python
def delete_dish(in_list, idx, start_idx=0):
    """
    param: in_list - a list from which to remove a dish
    param: idx (str) - a string that is expected to
            contain a representation of an integer index
            of a dish in the provided list
    param: start_idx (int) - by default, set to 0;
            an expected starting value for idx that
            gets subtracted from idx for 0-based indexing
    The function first checks if the input list is empty.
    The function then calls is_valid_index() to verify
    that the provided index idx is a valid positive
    index that can access an element from in_list.
    On success, the function saves the dish from in_list
    and returns it after it is deleted from in_list.
    returns:
    If the input list is empty, return 0.
    If idx is not of type string, return None.
    If is_valid_index() returns False, return -1.
    Otherwise, on success, the function returns the element
    that was just removed from the input list.
    Helper functions:
    - is_valid_index()
    """
```


The main program portion should contain:
```python
    elif opt == 'D':
        restaurant_menu_list = delete_helper(restaurant_menu_list, spicy_scale_map)
```

Complete the `delete_helper` given to you below: 
```python
def delete_helper(restaurant_menu_list, spicy_scale_map):
    continue_action = 'y'
    while continue_action == 'y':
        if not restaurant_menu_list:
            print("WARNING: There is nothing to delete!")
            break
        print("Which dish would you like to delete?")
        print("Press A to delete the entire menu for this restaurant, M to cancel this operation")
        print_restaurant_menu(restaurant_menu_list, spicy_scale_map, name_only=True, show_idx=True, start_idx=1)
        user_option = input("> ")
        if user_option == "A" or user_option == "a":
            print(f"::: WARNING! Are you sure you want to delete the entire menu ?")
            print("::: Type Yes to continue the deletion.")
            user_option = input("> ")
            if user_option == ...:
                restaurant_menu_list = ...
                print(f"Deleted the entire menu.")
            else:
                print(f"You entered '{...}' instead of Yes.")
                print("Canceling the deletion of the entire menu.")
            break
        elif user_option == 'M' or user_option == 'm':
            break
        result = delete_dish(restaurant_menu_list, user_option, 1)
        if type(result) == dict:
            print("Success!")
            print(f"Deleted the dish |{result['name']}|")
        elif result == 0:  # delete_item() returned an error
            print("WARNING: There is nothing to delete.")
        elif result == -1:  # is_valid_index() returned False
            print(f"WARNING: |{user_option}| is an invalid dish number!")

        print("::: Would you like to delete another dish?", end=" ")
        continue_action = input("Enter 'y' to continue.\n> ")
        continue_action = continue_action.lower()
    return restaurant_menu_list

```

# Sample Program Flow

1.  Deleting ALL dishes. Note that the user can only do this by selecting "A" (only the upper case "A") and then by confirming with "Yes" (not "Y", not "yes", ...)

    ```
    ::: Enter a menu option
    > D
    You selected option D to > Delete.
    Which dish would you like to delete?
    Press A to delete the entire menu for this restaurant, M to cancel this operation 
    ------------------------------------------
    1. BURRITO
    2. RICE BOWL
    3. MARGHERITA
    ------------------------------------------
    > A
    ::: WARNING! Are you sure you want to delete the entire menu ?
    ::: Type Yes to continue the deletion.
    > Yes
    Deleted the entire menu.
    ::: Press Enter to continue
    ```

    You can check that every dish got deleted by next going to the main menu, and selecting "L"ist:

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
    ------------------------------------------
    ::: Press Enter to continue
    ```

2.  Deleting one dish - example below shows what happens if the **wrong** dish ID is used, but then the user is given another chance to delete and they use the **correct** dish ID:

    ```
    ::: Enter a menu option
    > D
    You selected option D to > Delete.
    Which dish would you like to delete?
    Press A to delete the entire menu for this restaurant, M to cancel this operation 
    ------------------------------------------
    1. BURRITO
    2. RICE BOWL
    3. MARGHERITA
    ------------------------------------------
    > 4
    WARNING: |4| is an invalid dish number!
    ::: Would you like to delete another dish? Enter 'y' to continue.
    > y
    Which dish would you like to delete?
    Press A to delete the entire menu for this restaurant, M to cancel this operation 
    ------------------------------------------
    1. BURRITO
    2. RICE BOWL
    3. MARGHERITA
    ------------------------------------------
    > 1
    Success!
    Deleted the dish |burrito|
    ::: Would you like to delete another dish? Enter 'y' to continue.
    > n
    ::: Press Enter to continue
    ```

    Note that the user CAN keep choosing to enter 'y' at the "Would you like to delete another dish?..." prompt and be able to go back to the start of the delete menu choices. This would allow them to keep deleting dishs one by one.

    Again, you can check that the dish example from above (burrito) got deleted by going to the main menu, and selecting "L"ist:

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

    2. MARGHERITA
    * Calories: 800
    * Price: 18.9
    * Is it vegetarian: no
    * Spicy level: Low key spicy

    ------------------------------------------
    ::: Press Enter to continue
    ```

3.  Example when nothing gets deleted (i.e. you already deleted every dish and now you select delete again).

    ```
    ::: Enter a menu option
    > D
    You selected option D to > Delete.
    WARNING: There is nothing to delete!
    ::: Press Enter to continue
    ```

