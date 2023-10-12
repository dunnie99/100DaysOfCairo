# 100DaysOfCairo

## Introduction

Welcome to my hundred (100) days of diving into #STARKNET CAIRO. 


## Table of Contents
- [100 Days Of Cairo](#100-days-of-cairo)
    - [Introduction](#introduction)
    - [Table of Contents](#table-of-contents)
    - [StarkWare, StarkEx, Starknet](#starkware-starkex-starknet)
    -[Cairo Programming Language](#cairo-programming-language)
        -[Day1](#day1)

## StarkWare, StarkEx, Starknet


## Cairo Programming Language

## DAY 1 Variable and Immutability.
In Cairo, memory is treated as immutable by default, meaning once you store something in a memory cell,you can't change it directly. Variables in Cairo follow this immutability rule by default, which means once you assign a value to a variable, you can't change it. This is because changing values that are supposed to be constant can lead to eeror in code.

```
    use debug::PrintTrait;
    fn main() {
        let x = 5;
        x.print();
        x = 6;
        x.print();
    }
```

Above main() code will throw an error of "error: Cannot assign to an immutable variable.
```
  --> lib.cairo:5:5
        x = 6;  
         ^***^"
```

However, Cairo allows you to make variables mutable if you need to change their values. When you declare a variable as mutable using the mut keyword, it means that you can change the value it holds, but you still can't directly overwrite the memory cell itself. Instead, the memory address the variable points to can be updated to a new memory cell with the new value.

So, in simple terms, variable mutation in Cairo Assembly involves a kind of trick where you don't directly change what's inside the container; you create a new container with the updated data, and the type of the container doesn't change.

## DAY 2 Constant and Variable Shadowing.

Constants in #Cairo are declared using the ```const``` keyword, followed by name, its type, and the value.

They are like unchangeable facts ,that can be used within the scope which they were declared. You can only set them to values that don't change like numbers or text. e.g
```
const ONE_HOUR_IN_SECONDS: u32 = 3600;
```
Variable shadowing in #Cairo is like using the same name for different things in different places. Unlike ```mut``` which enforces the same variable type,  shadowing allows changing of a variable's value, or type within a more minor part of a code base.

The ```let``` keyword is used again when shadowing. e.g
```
let x = 2;
let x = x + 9;
```
Thus, It's like having a ```magic eraser``` for variables.


## DAY 3 Data Types.

Every value has a data type that defines how it is used.
In #Cairo, there are two main data type subsets: scalars (with single values e.g ```felts, integers, and booleans``` ) and compounds (collections).

Cairo is statically typed, meaning it knows variable types at compile time and infers types based on values but uses casting when needed.
Casting is like a way to make data wear a different type for a little while so you can work with it in a different way.

## DAY 4 Felt252.

In Cairo, when you don't specify a variable's data type, it defaults to a ```field element``` represented as "felt252." This means it's like an integer from 0 to a very large prime number, P.

When you do math operations (add, subtract, multiply), if the result goes beyond this range, it wraps around using modulo P.

## DAY 5 Felt252(contd...).

The key difference between regular integers division and #Cairo is that, In #Cairo, x/y is defined to always make ```(x / y) * y equal to x``` but may or may not always make ```(x / y) * y equal x``` in regular integers division.

So, if y divides x evenly, you get the expected result. But if otherwise, you might get an unexpected result e.g 
```
1 / 2 in Cairo is (P+1)/2, not 0 or 0.5, to satisfy the equation (x / y) * y == x.
```


## DAY 6 Integers and Booleans.

An integer is a whole number e.g ```1,2(no fraction)```. In using integer, we have to specify how much storage space to set aside to hold these numbers(type declaration) .

E.g  
```Boxes in a warehouse, the bigger the box, the larger the whole number that can be stored.```

Integers are unsigned by default in Cairo and using unsigned integers requires specifying the appropriate type precisely.

Boolean in Cairo is one felt252 in size meaning it's the smallest possible data unit for representing true/false conditions.
I'm still trying to grasp the concept fully, if you have any pointers to help me understand this kindly share.hopefully Day 7 will be more enlightening.

## DAY 7 Boolean Type.

In Cairo, boolean values are typically one bit in size. This means they can have only two possible values: true or false.
Having boolean values occupy just one bit of memory is efficient, as it doesn't require much storage space. It's also a good fit for representing binary choices, where something can be either "on" (true) or "off" (false).
Imagine a switch that can be either ```ON ( true) or OFF (false)```. This switch is so tiny that it takes up just one tiny bit of space in memory.

That's how big a boolean is in Cairo – it's as small as it can be, like a little switch that's either on or off.


## DAY 8 Short String.
In Cairo, there isn't a type just for words or sentences (strings) like we have in some other programming languages. Instead, Cairo uses something called a ```short string```.

A short string is a bunch of letters or characters that are stored inside  ```felt252```. Think of a ```felt252``` as a container that can hold a lot of 1s and 0s.
there's a rule with short strings: they can't be too long.
Dunnie

They can have at most 31 characters. This rule makes sure that the short string can fit neatly inside a single "felt" (which is 252 bits, or 31 bytes).


## DAY 9 Type Casting.
Cairo has two ways of converting a type of data into another.
```try_into```: Use when it is not sure if the data can be converted safely. It's like trying to fit a big item into a smaller container.  When using ```try_into```, you get an ```Option<T>``` that allows for a check if the conversion succeeded, by unwrapping.
 E.g
 ```
let my_u8: u8 = my_felt252.try_into().unwrap();
```

```into```: Use when conversion is sure to work safely. It's like changing an item into a different shape that can definitely hold everything from the original item.

To do the conversion, you write ```var.into()``` or ```var.try_into()``` and specify the new data type. 
E.g
```
let my_u16: u16 = my_u8.into();
```

## DAY 10 Tuple and Unit Type.

A tuple is like a bag that can hold different types of things in #Cairo. you make a tuple by putting values inside parentheses, separated by commas. They have a fixed size i.e can't get bigger or smaller once you make them.

Values inside a tuple can have different types.
```
fn main() {
    let tup: (u32, u64, bool) = (10, 20, true);
}
```
A unit type is like an empty bag; it has only one value, which is an empty tuple ```()```. It doesn't take up any space in memory. Unit is used when you need to indicate that something happened, but you don't need to carry any data with it.

## DAY 11 Review.

For the past two days, I've been working on starkling exercises  on variables and operations. Faced some blockers, but I'm hoping to make more progress.


## DAY 12 Functions and Parameter.
In #Cairo, the ```fn``` keyword is used when creating a function.
functions are given names using lowercase letters and underscores, like ```my_function```. They are defined with parentheses ```()``` for potential parameters and curly braces ```{}``` to contain the code they execute.To use a function, its name is called, followed by parentheses like ```my_function()```.
Functions can take some data called "parameters" to work with.

Parameters are like instructions or data given to the function, defined in the parentheses when a function is created. When a ```fn``` is called, the specific values for those parameters are provided.
For example, ```fn add(x: u32, y: u32)``` means the function add can take two numbers, ```x and y```.
So, functions are like tasks, and parameters are the details you give to those tasks.



## DAY 13 Functions Return Values
Functions can process data and also give us back some data. When a function gives back data, we say it "returns" a value.
In #Cairo, we declare the type of the return value using an arrow '->' followed by the type, E.g, 
```
fn add(x: u32, y: u32) -> u32.
```
The return value of a function is usually the result of the last expression in its body. So, we don't have to explicitly say "return," it just knows that the last thing calculated is what should be given back.
E.g, if a function has 2 as the last thing it does, it returns 2.

NB : Do not to put a semicolon (;) at the end of the line when returning a value. Else, it becomes a statement, not an expression, and that can cause an error.
i.e
```x + 1 is an expression that returns a value, but x + 1; with a semicolon becomes a statement and doesn't return anything.```
Cairo is smart enough to know what the answer is without us saying "return" explicitly and don't put semicolons at the end of an expression, or it might cause errors.

## DAY 14 Control Flow (IF/ELSE).
Two basic tools for control flow are ```if``` expressions and loops. An ```if``` expression helps make decisions in cairo, "If this condition is true, do this; otherwise, do something else."
It starts with the word "if" followed by a condition in parentheses, and the code to run if the condition is true inside curly braces ```{}```. An ```else``` part can also be added with different code to run if the condition is false.

```E.g: Let's say a variable number = 3. we can use an "if" expression to check if number is equal to 5. If it is, print "condition was true," otherwise, print "condition was false."```

There can be more than one condition by using ```else if``` after the initial ```if```.
It's like saying, "If this condition is true, do this;

otherwise, if another condition is true, do something else."
```E.g: number = 3, check if it's 12, if not, check if it's 3```, and so on. Cairo stops checking as soon as it finds a true condition.

NB: The condition must be a yes-or-no question (true or false). Cairo executes only the first true condition in an ```if-else if``` chain.


## DAY 15 Control Flow (LOOPS).

Sometimes, we want a piece of code to run over and over. Cairo provides a simple way to do this with a loop.
The ```loop``` keyword tells Cairo to keep running a block of code
i.e ```use it to create a loop that runs forever or until a certain condition is met.```
For instance, you can have a loop that counts from 0 to 10 and prints "again!" each time.
Most loops have a stop condition to prevent them from running forever, like using the ```break``` statement to exit the loop when the condition is met.


## DAY 16 Control Flow (Controlling Loop Execution:).
The ```continue``` statement is used to skip the rest of the code in an iteration and move to the next one. i.e, we can skip printing when a certain condition is met.

Loops can also return values and to pass a value out of the loop, we use the ```break``` statement with a value. This value will be returned when the loop stops, and can be used later in the code.
That's how to make code repeat tasks and even return results from loops in Cairo.


## DAY 17 Arrays

An ```array``` is like a one-way street where we can only add new things at the end and remove things from the front. Also once something is placed in the array, it cannot be changed but can read what's stored in it.

When creating an ```array```, we specify the type of data it will hold, like specifying whether it will hold ```bool``` or ```felt252```.
Adding items to the array is like placing a new item at the end of the line, and removing items from the array is taking out the first item in the line.

In Cairo programming, we cannot change what's already in the array, only keep adding new items to the end and taking out items from the front. Reshuffling the order without altering the contents.

## DAY 18 Reading Array.

An array is like a list of items and we can use two methods to read this list.
1. get(): This method checks if an element is in the list at a specific position. It returns the element if it does exist else, returns none. It doesn't cause errors if the position is empty.

2. at(): This method directly gives what's in the list at a specific position. But if the element is not there, it panics(can cause errors).
Basically, if you use get(), you're being careful. If you use at(), you're saying, "I'm sure it's there."

len():  returns nunber of element.
is_empty(): It checks if the array is empty and returns true or false.
Span: is like taking a picture of the array which you can't change. It's useful to keep the array safe and make sure it doesn't get tampered with. A array can be turned into a span by calling ```span()``` on it.

## DAY 19 Dictionaries.

Cairo provides a special kind of data structure called ```Felt252Dict<T>```, which is like a map in other programming languages. It involves having a collection of pairs, where each pair has a unique key and when we need to overwrite a memory, even though you can't really change the memory in Cairo.

1. To add something to a dictionary, you use insert(key, value). E.g writing a word and its meaning in a dictionary.

2. To get something from a dictionary, you use get(key). E.g looking up a word to find its meaning in a dictionary.


## DAY 20  Felt252Dict Entries.

Let's take Felt252Dict<T> as a list of records, and each record has three pieces of information:

1. Key: This is a label for the value in the dictionary, like a word in a real dictionary. 
2. Previous Value: This is the value associated with the key before any changes.
3. New Value: This is the new value associated with the key after changes.
So, every time we do something with Felt252Dict<T>, like reading, updating, or writing, a new record is created to remember what happened.

How Entries Work:

When we read from the dictionary, an entry is created with the same previous and new values because nothing changed.
When a new value is inserted, an entry is created with the new value that is being added and the previous value is the last thing that was there (or zero if it's the first time).


## DAY 21 Squashing Dictionaries

To make sure a program that uses Felt252Dict<T> is correct, we need to check that the dictionary hasn't been tampered with illegally during runtime by "squashing the dictionary." This basically means reviewing each dictionary entry, and making sure that access to the dictionary remains constant while executing the program.

Squashing Process: It involves checking entries in the dictionary with the same key and verifying that the new value for the 'i-th' entry matches the previous value for the 'i+1-th' entry. If any value in the dictionary changes illegally, the squashing process will fail during runtime.

NB: Felt252Dict<T> does not support all types, and some complex types like arrays and structs are not directly supported.

To work with these types, we can wrap them using a type called Nullable<T>




























