# Code Readability
###  or Coding for Human Consumption

<br>

> "Doing it good is not enough, you have to look good while doing it."

![readabilityTITLE](https://user-images.githubusercontent.com/116419708/226084439-16528db0-46bd-4672-8857-efce7485d190.gif)

  Code readability is something that I find gets often overlooked when it comes to programming. This is a problem as readability is analogous
  to hand-writing, and if everyone's writing is unintelligble, then discourse, and even corrections, would be difficult to achieve.
  
> In order to code good, you have to *code* good.

  Coding has to be, and can be, fun. And the first step towards that is to write code that doesn't make you want to **OFF** yourself whenever you're reading it.
  _Code architecture is important_, so here are some opinionated takes I have on good programming practices, which you can take as code design guidelines.
  <br><br>
## BRACES AND INDENTS

  - When writing blocks of code (code within curly braces), there are 2 ways you can go about doing it, which I refer to as : **Inset** and **Offset**.
  
![insetoffset](https://user-images.githubusercontent.com/116419708/226085375-3c6dda98-0a15-442e-9e57-b2d36e902c74.gif)

  - I personally do not mind either. I prefer Offset bracing as I like avoiding the claustrophobic feel of words being packed into one tight space vertically.
    However, the main appeal of Inset bracing is the compact feel it will give your code. Ultimately, it's an entirely stylistic decision, just be consistent:
    do not alternate between either or they will look more like speedbumps for the reader instead of grouping operators.
  
![image](https://user-images.githubusercontent.com/116419708/226085554-ad69ee94-666c-4dea-9162-86b0f7b6b03c.png)

  - Lastly, remember to properly indent whenever you enter a code block, and that you can omit the curly braces for when your code block only has **ONE** statement.
    If you value stability over sleekness, it is much safer to put in the braces. Only if you are uncertain on whether or not that code block will expand in the future.
    A good rule to check for matching braces is to see if the statement that started your code block aligns/is in the same indentation further down with a 
    closing curly brace.
