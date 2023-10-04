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

## DAY 2