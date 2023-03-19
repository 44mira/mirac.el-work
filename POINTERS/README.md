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
  - [DEREFERENCING](#dereferencing)
  - [ARRAYS AND ARITHMETIC](#arrays-and-arithmetic)
  - [MALLOC aka MEMORY FREESTYLE](#malloc-aka-memory-freestyle)
<br><br><br>





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
  
  <br>
  
## ARRAYS AND ARITHMETIC
  
> Arrays are just pointers to *contiguous* data

  Recall that variables are just memory addresses that hold values/data. Now pointers are also just memory addresses that happen to hold _other_ memory addresses.
  With this specific idea, we can generalize memory addresses as _containers_ for values in our program.
  
  - So what does it mean to say that *"Arrays are pointers to contiguous data?"*

  Memory addresses are selected at, for simplicity's sake, random and are not arranged at any order. Except for *arrays.*
  Arrays are stored in addresses that are *consecutive* to each other, in memory arrays. Going back to the analogy on addresses being last names,
  you can think of arrays as people with the same last name, they are all closely related to each other. Which means if you find a way to move *forward* 
  by one address, you would essentially be traversing the array by one index. 
  
  - However, memory addresses do not necessarily occupy just one byte, besides the address for a char, and varies on the data type's size.
  So to move *forward* in an integer array, you would essentially have to go forward by FOUR (int size is 4 bytes) bytes in memory.
  BUT, we do not have to worry about that right now, as pointer arithmetic (C's way of navigating addresses) already deals with this for us.
  
  ![pointersarray](https://user-images.githubusercontent.com/116419708/226114818-20aaa354-bf83-4954-9413-5ef5ed376a59.gif)
  
> Arrays are special pointers that hold the address of the element in their 0th index.

  What this means, is that with careful addition and subtraction, we can traverse through an array of elements! 

```
  int arr[] = {0, 13, 22, 34, 45};    // creation of array
  
  for (int i = 0; i < 5; i++) {
    *(arr+i) += 5;                    // add 5 to every element of the array
  }
```
<sup>**the last index of the array will be located at (array_pointer + array_length-1) because the first index is at ( array_pointer + 0 )**</sup>

  This knowledge is especially useful when passing arrays as arguments of a function, as the function itself just decays from int[] to (int \*) (in this example)
  which means it loses its identity as an array (it will no longer know its size) and turns into a normal pointer, that just happens to be next to other pointers.
  Which is why in C it is common to pass an array along with its size.
  
```
  void halve_array(int *arr, int size){ 
    for (int i = 0; i < size; i++)
      *(arr+i) /= 2;                      // halves every element of the array
  }
```
  
  <br>
  
## MALLOC aka MEMORY FREESTYLE

> C/C++ is not a *memory-safe* language.

  And in this section we will find out why that's the case.
  
```
  char *word = (char*) malloc (sizeof (*word) * size);
```
  
  If you have dealt with pointers beforehand, you may recognize this syntax. Or kinda remember seeing it somewhere. So let us take the right-side of the assignment apart.
  
  - **malloc**
      - this is a function in C (you have to include <stdlib.h> in your program, however it is built-in in C++), that *allocates memory* for this particular pointer.
        - What it means to allocate memory, is that it *reserves* spaces in memory for your pointer to use, in whatever way you might want to.
      - This is essentially giving your pointer keys to a particular spot in the *heap* memory (you can think of heap memory as memory specifically for reservations like these)
  - **sizeof**;
      - this is an *operator* (like + and -) in C/C++ that returns the bytes occupied or being used by the variable that follows it.
  - **(sizeof (\*word) \* size);
      - these are the arguments being passed onto the malloc()
      - Recall that memory addresses do not necessarily occupy only one byte, so we have to get the size of the pointer, and then multiply it with the number of
        addresses we would like to *reserve*.
  - **(char\*)**
      - Lastly, malloc() returns a pointer of the type void (void\*), which is basically it saying : "Alright, here's your spots, but I have no idea what cars you'll
        be parking here. And in this *type-cast* (conversion of a type to another), we are telling the program, "Hey, the spots we reserved are for *these* type of
        cars."
      - And like in real life, in C, the program doesn't really care what type your cars are but it is a good habit to build, as in C++, your compiler will flag
        this lack of type-casting as an error, as it is *extremely* unsafe to just be tossing stuff into the *void* without knowing what it's for.
        
  So what's happening in our previous expression is like saying : "Hey, program, we would like to reserve **size** spots for our char\* cars."
  
  Here's another example of that expression :
  
```
  int *nums = (int*) malloc (sizeof (*nums) * 5);
```
<sup>***allocating* 5 int addresses for our nums pointer**</sup>
  
  Now that you understand malloc, I would now like to congratulate you for creating a *memory leak!*
  
![pointermalloc](https://user-images.githubusercontent.com/116419708/226160489-c813dc76-60eb-4989-a278-7bd246c6cf0c.gif)
  
  I sometimes refer to memory allocation as ***memory freestyle*** only because C/C++ will let you directly access memory, and trust you to not mess things up.
  You are quite literally, creating variables from scratch. But because you created them, you also have to be the one to clean up after them when they're done.
  Allocated memory has to be freed by the programmer to avoid the aforementioned issue of *memory leaks*, which is, to put simply, when your program is still taking
  up memory that it doesn't really use.
  
  Another issue you might, or might have already, encounter is *segmentation fault*. This is when your program tries to access memory it hasn't allocated yet.
  This is a problem because, as the C documentation tries to sugarcoat it, we have no idea what it will do. It is *undefined* behavior.[^1] Sometimes your compiler
  will catch your seg faults (when you try to write into undefined addresses), sometimes it *won't* (mess up your print statements), this is particularly dangerous.
  
```
  int *nums = (int*) malloc (sizeof(*nums) * 3);
  *(nums+5) = 15;                         // Segmentation Fault, may or may not be raised by your compiler, but you are writing in an undefined address
```

  ![image](https://user-images.githubusercontent.com/116419708/226161293-5ee6182a-e717-43f8-a8bb-3810fd4a1826.png)
  
> C makes it easy to shoot yourself in the foot; C++ makes it harder, but when you do it blows your whole leg off.
> - Bjarne Stroustrup

<sup>**very popular quote about c/c++ memory safety**</sup>

<br>

[^1]: [How to cause a segmentation fault](https://kb.iu.edu/d/aqsj#:~:text=A%20segfault%20occurs%20when%20a,in%20a%20read%2Donly%20segment.)
  
