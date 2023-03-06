---
layout: default
title: Step 7 - "Show Average Price"  option
---

# {{page.title}}


New functions needed:
* `get_restaurant_expense_rating()`

For this menu item, in your main program, you will use the restaurant menu list. This part of your main program will call the function **`get_restaurant_expense_rating()`**.


```
def get_restaurant_expense_rating(restaurant_menu_list):
    """
    Computes the average price of all the items on the menu and display the expense rating of the restaurant.
    param: restaurant_menu_list - a list of restaurants and their dishes (list of dicts)
    
    returns: Nothing! This function only PRINTS out results.    
    """
```

## You are NOT allowed to use any `import` statements or outside library methods in `get_restaurant_expense_rating())`.
### You can only use "regular" Python methods for this function.

Here are some hints on how to go about this:
* You should collect all the menu items' prices for a given restaurant into one list.
* You've done calculating means (averages) from lists before...

```

# Sample Program Flow

Below is a demo of computing the average price of an item in a given restaurant menu:
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
> H
You selected option H to > Display restaurant expense rating .
Expense rating is : $$
 
```

