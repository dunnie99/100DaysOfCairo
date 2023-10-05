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

## DAY 1 Variable and Immutability
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

## DAY 2 Constant and Variable Shadowing

Constants in #Cairo are declared using the "const" keyword, followed by name, its type, and the value.

They are like unchangeable facts ,that can be used within the scope which they were declared. You can only set them to values that don't change like numbers or text. e.g
const ONE_HOUR_IN_SECONDS: u32 = 3600;

Variable shadowing in #Cairo is like using the same name for different things in different places. Unlike "mut" which enforces the same variable type,  shadowing allows changing of a variable's value, or type within a more minor part of a code base.

The "let" keyword is used again when shadowing. e.g
let x = 2;
let x = x + 9;
Thus, It's like having a "magic eraser" for variables.


## DAY 3 Data Types

Every value has a data type that defines how it is used.
In #Cairo, there are two main data type subsets: scalars (with single values e.g felts, integers, and booleans ) and compounds (collections).

Cairo is statically typed, meaning it knows variable types at compile time and infers types based on values but uses casting when needed.
Casting is like a way to make data wear a different type for a little while so you can work with it in a different way.

## DAY 4 Felt252

In Cairo, when you don't specify a variable's data type, it defaults to a "field element" represented as "felt252." This means it's like an integer from 0 to a very large prime number, P.

When you do math operations (add, subtract, multiply), if the result goes beyond this range, it wraps around using modulo P.

## DAY 5 Felt252(contd...)

The key difference between regular integers division and #Cairo is that, In #Cairo, x/y is defined to always make (x / y) * y equal to x but may or may not always make (x / y) * y equal x in regular integers division.

So, if y divides x evenly, you get the expected result. But if otherwise, you might get an unexpected result e.g 1 / 2 in Cairo is (P+1)/2, not 0 or 0.5, to satisfy the equation (x / y) * y == x.


## DAY 6 Integers and Booleans.

An integer is a whole number e.g 1,2(no fraction). In using integer, we have to specify how much storage space to set aside to hold these numbers(type declaration) .

E.g boxes in a warehouse, the bigger the box, the larger the whole number that can be stored.
Integers are unsigned by default in cairo and using unsigned integers requires specifying the appropriate type precisely.

Boolean in #Cairo is one felt252 in size meaning it's the smallest possible data unit for representing true/false conditions.
I'm still trying to grasp the concept fully, if you have any pointers to help me understand this kindly share.hopefully Day 7 will be more enlightening.





