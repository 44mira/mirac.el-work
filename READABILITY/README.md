# Code Readability
###  or Coding for Human Consumption
<sup>*chapter author : el*</sup>
<br>

> "Doing it good is not enough, you have to look good while doing it."

![readabilityTITLE](https://user-images.githubusercontent.com/116419708/226084439-16528db0-46bd-4672-8857-efce7485d190.gif)

  Code readability is something that I find gets often overlooked when it comes to programming. This is a problem as readability is analogous
  to hand-writing, and if everyone's writing is unintelligible, then discourse, and even corrections, would be difficult to achieve.
  
> In order to code good, you have to *code* good.

  Coding has to be, and can be, fun. And the first step towards that is to write code that doesn't make you want to **OFF** yourself whenever you're reading it.
  _Code architecture is important_, so here are some opinionated takes I have on good programming practices, which you can take as code design guidelines.
  <br><br>
## TABLE OF CONTENTS:
  - [BRACES AND INDENTS](README.md#braces-and-indents)
  - [NESTING AND CONDITIONS](README.md#nesting-and-conditions)
  - [NAMING AND CONSTANTS](README.md#naming-and-constants)
  - [SPACING AND COMMENTS](README.md#spacing-and-comments)
  - [ONELINERS AND TERNARY OPERATORS](README.md#oneliners-and-ternary-operators)
  
## BRACES AND INDENTS

  - When writing blocks of code (code within curly braces), there are 2 ways you can go about doing it, which I refer to as : **Inset** and **Offset**.
  
![insetoffset](https://user-images.githubusercontent.com/116419708/226085375-3c6dda98-0a15-442e-9e57-b2d36e902c74.gif)

  - I personally do not mind either. I prefer Offset bracing as I like avoiding the claustrophobic feel of words being packed into one tight space vertically.
    However, the main appeal of Inset bracing is the compact feel it will give your code. 
  - Ultimately, it's an entirely stylistic decision, just be consistent: do not alternate between either or they will look more like speedbumps
    for the reader instead of grouping operators.
  
```
int main()
{
    int x, y;
    cin >> x >> y;

    if (x > y)
        swap(x,y);

    for (int i = 0; i<5; i++){
        x = x + y;

        if (x > y)
            swap(x,y);

        cout << x;
    }
    
    return 0;
}
```
  - Lastly, remember to properly indent whenever you enter a code block, and that you can omit the curly braces for when your code block only has **ONE** statement.
    If you value stability over sleekness, it is much safer to put in the braces, if you are uncertain on whether or not that code block will expand in the future.
  - A good rule to check for matching braces is to see if the statement that started your code block aligns/is in the same indentation further down with a 
    closing curly brace.
<br><br>
## NESTING AND CONDITIONS

  - Avoid overly nesting your code.[^1]
  
  ![earlyreturn](https://user-images.githubusercontent.com/116419708/226088447-dada514b-1c8a-44ed-bc82-3f47eb65a6c3.gif)
  
  - Getting rid of nesting can be a matter of identifying early returns (if-else clauses that can be negated by swapping the if and the else), and/or extracting
    deeply nested code and putting them into their own seperate function.
    
```

int get_year_value(int year)
{
    /* returns value of the year (leap year or not), for faster code. */
    if (year % 4)
        return 365;
    return 366;
    
}

int get_age(int bday_m, int bday_d, int bday_y, int targ_m, int targ_d, int targ_y)
{
    ...
    while (targ_y > bday_y)
    {
        diff += get_year_value(bday_y); 
        bday_y++;
    }
    ...
}
```
<sup>***note how the if condition for getting year_value is put onto a seperate function as to not nest the code***</sup>

  - Moreover, always remember that control flow operators (if-else, while loops, basically anything that requires a condition) take in boolean, or true or false.
  - Recall that true or false can be also represented as 0 and 1 in pretty much all programming languages, so a good shorthand for checking for zero or not zero,
    is to just put the expression into the condition as is. (x != 0) is equal to simply (x), and (x == 0) is equal to (!x).
<br><br>
## NAMING AND CONSTANTS

  - Always use brief and concise names[^2], and only choose between **camelCase** or **snake_case**: 
  
![case](https://user-images.githubusercontent.com/116419708/226089997-7d0c61f4-8071-405d-b1a0-b3b4ab607319.gif)

  - Avoid using single character names, with exceptions to for loops 'int i' or Python's _ throwaway variable. *Be descriptive*, you will have to interpret your code
    multiple times over before you finally finish your project, do yourself a favor and make your variable names have less brain power cost.
  - Moreover, please use constants. Avoid hard-coding values, and/or repeating long chains of method calls.

![consts](https://user-images.githubusercontent.com/116419708/226090837-07d44b02-5cc6-405c-9dd8-f665f440ff2d.gif)

  - Constants, or consts, are quite often overlooked as they just get overshadowed by variables, however; the security and readability that they provide
    are actually quite unparalleled. 
    
```
  const SIZE = 5;
  int array[SIZE];
```

  - In this example, refactoring/changing the code to handle an array of a different size than 5 is much less expensive (energy and time-wise) to do, especially
    if there are other instances in the code that utilize the size of the array.
<br><br>
## SPACING AND COMMENTS

  - Space your code in *paragraphs* (lines that are relevant to eachother) to reduce the visual noise of packed letters.

![comments](https://user-images.githubusercontent.com/116419708/226095454-0708e941-b2f9-4e87-b967-248c7de83eec.gif)

  - Moreover, write documentation for your code. This is one of the best ways to improve understandability for other people who read your code.
  - BUT, whenever you are writing comments, be sure to write *WHY* your code does something, and not *WHAT* it does. The code itself should be sufficient in
    showing what it is doing, due to its procedural (being a sequence of instructions) nature.
  - An exemption to this rule are Docstrings, or the main comments that describe your function. All of your functions must have a docstring, paired with concise
    function names. Not only does this benefit your readability, it also shows up as a short description whenever you hover over one of your function calls.
    
    ![image](https://user-images.githubusercontent.com/116419708/226097627-5d9b5ba9-e87b-4bac-974c-51479756f2a4.png)
    
    <br><br>
    
## ONELINERS AND TERNARY OPERATORS
  
  - Though it is quite tempting to always go for less lines, readability suffers the longer your lines get. So don't be shy, use up more lines!

![oneliner](https://user-images.githubusercontent.com/116419708/226096782-3e237c0f-ce6d-412c-ab85-38c3b0f1c2c9.gif)

  - Though it doesn't hurt to come up with very line-efficient algorithms, there has to be a balance with the compactness and readability of your code.
  - Moreover; ternary operators are very satisfying to read, but it has diminishing returns the longer you chain it.
  - A good rule of thumb is whenever your ternary operator _chains at least once_, you are better off using if-else statements.

```
  /* ans can be "yes", "no", or "maybe" */
  
  int decision = (ans == "yes") ? 1 : (ans == "no") ? 0 : -1;   // what the hell is happening?
  
  int decision;   // oohh
  if (ans == "yes")
    decision = 1;
  else if (ans == "no")
    decision = 0;
  else
    decision = -1;
```

> **The less mental gymnastics the reader has to go through to understand your code, means the better your readability is.**

<br><br>

[^1]: [Why You Shouldn't Nest Your Code by Code Aesthetic](https://youtu.be/CFRhGnuXG-4)
[^2]: [Naming Things in Code by Code Aesthetic](https://youtu.be/-J3wNP6u5YU)

