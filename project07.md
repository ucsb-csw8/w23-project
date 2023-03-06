---
layout: default
title: Step 7 - "Show stats"  option
---

# {{page.title}}


New functions needed:
* `do_stats()`

For this menu item, in your main program, you will use the repeating "continue_action" method used in other menu items. This part of your main program will call the function **`do_stats()`**.


```
def do_stats(menu_dict, opt):
    """
    param: menu_dict - a dictionary of menu (dict of dict)
    param: opt (str) - an option from the menu
    to do one of the following statistical calculations:
        "A" - find the mean (average) of all menu ratings values
        "B" - find the median of all menu ratings values
        "C" - find the standard deviation of all menu ratings values
        "D" - print out a histogram of all menu ratings values
        
    Helpful hint: see example on top of page in
    zyBook Ch. 8.4 to see how to do mean and stddev calculations.

    returns: Nothing! This function only PRINTS out results.    
    """
```

## You are NOT allowed to use any `import` statements or outside library methods in `do_stats()`.
### You can only use "regular" Python methods for this function.

Here are some hints on how to go about this:
* You should collect all the menus' ratings into one list.
* You've done calculating means (averages) from lists before...
* You have a great example of how to calculate a standard deviation of numbers in a list in Chapter 8.4 of your zyBook.
* For median calculation, here's a general algorithm:
   * If you have a list of numbers, sort them first.
   * If you have an odd number of entries in the list, the median is the one in the middle.
      * Example: the median in [1,1,2,3,4] is 2
   * If you have an even number of entries in the list, the median is the average of the 2 middle ones.
      * Example: the median in [1,1,2,3] is 1.5
* A histogram is a plot of how often every value in the list appears. 
    * For **this** histogram, if you have a list of numbers like this, for example:  **[0,1,1,1,2,4,4,5,5,5,5]**, you are expected to print something like this (note that each `*` represents a count for that number in the list):
```
0 *
1 ***
2 *
3
4 **
5 ****
```

# Sample Program Flow

Below is a demo of all 4 statistical computations as driven by the menu:
```
> m
You selected option M to > Show statistical data on.
::: What would you like to show statistical data on?
A - Mean value of all menu ratings
B - Median value of all menu ratings
C - Standard Deviation value of all menu ratings
D - Histogram of all menu ratings
::: Enter your selection
> a
You selected |A| to show statistical data on |mean value of all menu ratings|.
The mean value of all ratings is: 4.25
::: Would you like to get different statistics? Enter 'y' to continue.
> y
::: What would you like to show statistical data on?
A - Mean value of all song ratings
B - Median value of all song ratings
C - Standard Deviation value of all song ratings
D - Histogram of all song ratings
::: Enter your selection
> b
You selected |B| to show statistical data on |median value of all song ratings|.
The median value of all ratings is: 4.50
::: Would you like to get different statistics? Enter 'y' to continue.
> y
::: What would you like to show statistical data on?
A - Mean value of all song ratings
B - Median value of all song ratings
C - Standard Deviation value of all song ratings
D - Histogram of all song ratings
::: Enter your selection
> c
You selected |C| to show statistical data on |standard deviation value of all song ratings|.
The standard deviation value of all ratings is: 0.83
::: Would you like to get different statistics? Enter 'y' to continue.
> y
::: What would you like to show statistical data on?
A - Mean value of all song ratings
B - Median value of all song ratings
C - Standard Deviation value of all song ratings
D - Histogram of all song ratings
::: Enter your selection
> d
You selected |D| to show statistical data on |histogram of all song ratings|.
1 
2 
3 *
4 *
5 **
::: Would you like to get different statistics? Enter 'y' to continue.
> 
```

