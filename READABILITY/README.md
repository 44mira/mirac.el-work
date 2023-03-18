# Code Readability
###  or Coding for Human Consumption

<br>

> "Doing it good is not enough, you have to look good while doing it."

![readabilityTITLE](https://user-images.githubusercontent.com/116419708/226084439-16528db0-46bd-4672-8857-efce7485d190.gif)

  Code readability is something that I find gets often overlooked when it comes to programming. This is a problem as readability is analogous
  to hand-writing, and if everyone's writing is unintelligible, then discourse, and even corrections, would be difficult to achieve.
  
> In order to code good, you have to *code* good.

  Coding has to be, and can be, fun. And the first step towards that is to write code that doesn't make you want to **OFF** yourself whenever you're reading it.
  _Code architecture is important_, so here are some opinionated takes I have on good programming practices, which you can take as code design guidelines.
  <br><br>
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
    Recall that true or false can be also represented as 0 and 1 in pretty much all programming languages, so a good shorthand for checking for zero or not zero,
    is to just put the expression into the condition as is. (x != 0) is equal to simply (x), and (x == 0) is equal to (!x).
  




[^1]: [Why You Shouldn't Nest Your Code by Code Aesthetic](https://youtu.be/CFRhGnuXG-4)

