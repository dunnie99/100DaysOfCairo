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








































