#  Pointers
### and Pointers that point to Pointers, and Pointers that...
<sup>*chapter author : el*</sup>

> There may be reasons to switch out of computer science, but pointers isn't one of them.
> - Fred Swartz

![pointerstitle](https://user-images.githubusercontent.com/116419708/226108305-0ae3e8f7-2e94-49b5-855f-27c3a08a31c1.gif)

***DISCLAIMER: THIS CHAPTER WILL BE ENTIRELY IN C/C++***
<br>

  Ah, pointers. Pointers are definitely one of the most infamous topics when it comes to low-level programming. Because unlike its name, low-level programming requires
  a lot of *high-level* thinking. Anyways, pointers!
  
> Pointers are variables that hold addresses. Literally just that.

  Now what are addresses? You can think of them as your variable's last name. Multiple variables can have the same value but they will have unique addresses.
  As int holds numbers, pointers hold addresses. That is the main concept to understand here. You can get the value of a variable from the pointer, but you cannot get
  the pointer from the value. 



## TABLE OF CONTENTS: 
  - [DEREFERENCING](#DEREFERENCING)






## DEREFERENCING 

```
  // syntax 
  int *pointer_name;          // this holds an address of an int
  float *pointer_name;        // this holds an address of a float
                              // so on and so forth.
```
  
  - *You might be asking, if all we're doing is holding last names of values (their addresses), why do pointers need to have types?*
  
  That is a completely valid question. Addresses are always going to be in the format that is based on your computer. they can be in a 16-bit format or 8-bit.
  But it will always be the same length and format for your operating system. So, why do we need to differentiate the types when they're all going to be 
  similar anyway? The answer lies in the other functionality of a pointer.
  
  ***Dereferencing*** is not only quite a mouthful, but is actually pretty essential knowledge when it comes to low-level programming and working with pointers.
  
  ![image](https://user-images.githubusercontent.com/116419708/226109394-4f1ebb8e-1b16-439d-bb6c-48b7eeb62175.png)
  
  The syntax here might be confusing but to put it simply: the asterisk at assignment means that a pointer is created, while the asterisk beside the 
  declared pointer means we are getting the value *stored at* the address the pointer is holding. We are **__de__referencing** it. Or getting it from the reference.
  
  It's true that dereferencing in this example is quite obsolete as we can just get the value from the variable, but pointer dereferencing shines through when what
  you need isn't *just* the value, but the *variable* itself.
  
  What follows is a simple exchange between the main() and an add_five() function which takes an int and returns the value of that int added with 5.
  
```
  int add_five(int x){          // takes the value of x and returns an int
    return x + 5;
  }

  int main(){
    int num = 0;
    num = add_five(num);        // num is now equal to 5.
  }
```
  
  Easy right? But what if instead of returning a value to modify the num in main(), we could've just immediately changed it at the add_five() function?
  We can actually do that with pointers and dereferencing!
  
```
  void add_five(int *x){         // takes the ADDRESS of x and no longer has to return anything
    *x += 5;                     // num is now equal to 5
  }

  int main(){
    int num = 0;
    add_five(&num);              // the address of num is passed (which is of type int *)
  }
```
  
  Since we passed *the variable itself*, when we added 5 to its value (by dereferencing it first) in the add_five() function, it reflected on the original 
  num without having to return a value! We are no longer relying on returning values to change, well, values in main(), therefore we could theoretically 
  modify an infinite number of variables in main() with only **ONE** function!
  
```
  void add_five(int *x, int *y, int *z){         // takes the ADDRESSES of x, y, and z
    *x += 5;
    *y += 5;
    *z += 5;
  }

  int main(){
    int num = 0, num1 = 5, num2 = 3;
    add_five(&num, &num1, &num2);               // every number passed is now increased by 5
  }
```

![pointer example](https://user-images.githubusercontent.com/116419708/226110762-ebdc5b04-e957-41e7-acc6-ab9ddd303d0f.gif)
<sup>**everything we have done so far, with a little bit of c++ magic at the end**</sup>

  Dereferencing is so essential to pointer manipulation that C++ created a new function for the &, which makes it take the address of the passed variable, and then
  automatically dereference it whenever it's used in the function, aka all the confusing syntax stuff we did, all into one operator! That's insane!

  Moreover; to answer the question that started this section: pointers have types so that the program knows the memory it will allocate for when it is dereferenced.
  So, in that way, you can think of pointers as almost-variables— they have yet to hold value, but in order for whatever it is that's receiving them to properly
  store them, they must know what type of value they're about to get.
  
