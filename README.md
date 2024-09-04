# Project 1 @ CSC 201B Fall 2024: Binary Search Tree

## Pledged Work Policy

This is a ___Pledged Work___ assignment.  This means that the work you submit for grading ___must___ be your team's work product.  
You may not submit the work of others
outside of your team , or the modification of work of others
outside of your team.
You certainly may talk with each other about general problems.  For example, you may talk to someone about "What does it mean when the compiler says there is a semicolon missing on line 20", or "I can not get my assignment template to download from GitHub, what did you do?".  However, you may not engage in "Could you send me a copy of your work so I can see how to get started?".  You may get full and detailed assistance from me, the Graduate Teaching Assistant, and the TAs in the Computer Science Center.  If you have any question about the appropriateness of assistance, do not hesitate to consult with me.

If I believe you have violated our ___Pledge Work___ agreement, I will pursue this matter through the college Honor Council.

## Overview

Database software typically comprises two essential components: an interface for user interaction and a data structure for storing data and supporting various functions. This project involves the creation of a program that manages a Binary Search Tree (BST).

In this project, you will implement: 

1. A generic BST with iterator interface.
2. A parser capable of reading and processing input commands.
3. A BST that can accommodate user-defined data types.

## Invocation and I/O Files:

The name of the program is `Proj1` ( provided with a `main` method in`Proj1.java` ). 

You are encouraged to run and debug code in **IntelliJ IDEA**. Also, the program can be invoked from the command-line as:

```shell
java Proj1 {command-file}
```

For Parts 1 and 2, your program will read a series of commands from the input file `input.txt` and generate the output file  `result.txt`, which will be used for grading.


## 1. **Generic BST with Iterator Interface**

In this part, you will construct **a generic and iterable Binary Search Tree (BST)**.  

First, create a `Node` class with **Comparable interface** to represent nodes of the BST. Each node should encompass a value, references to both left and right subtrees, along with necessary utility methods as instructed in file `Node.java`.

Then, develop a `BST` class to manage the structure of BST. Please finish the implementation in file `BST.java`.

Make sure these operations of BST are handled in a general way that does not require the BST to understand the type of its elements. For example, the `value` in `Node` may be a user-defined data structure with `Comparable` interface, necessitating the use of `compareTo() ` method for comparison.

## 2. **Parse Input Commands**

Your program will read a series of commands from the input file, with one command per line. The commands are free-format in that any number of spaces may come before, between, or after the command name and its parameters.

You're going to implement `process()` ,`operate_BST() `, and `writeToFile()` methods in `Parser` class for this part.

In `process()` method, you will read the command file line by line, remove redundant spaces, ignore blank lines, to handle different input formatting. 

Then, you need to split each line into string array `command`, then create your  `operate_BST(String[] command)` method to test your BST. 

After this, use the `writeToFile()` method to write your BST result into `result.txt`. In the `writeToFile()` method, you're asked to open the specified file (create it if it doesn't exist), append a new line at the end of the file, and write the output  (`String content`).

The `BST` class shall support the following commands. (Check example commands in the provided input file):

+ `insert val`: 

  Insert a new `Node` with value of `val` into BST. Write `insert <val>` to `result.txt`.

  ```
  ## sample input.txt
  insert 23
  
  ## sample result.txt
  insert 23
  ```

+ `search val`: 

  Searches the BST to find out if a node with value `val` exists.

  If found, return the `Node`, and write `found <val>` to `result.txt`, otherwise return `null` and write `search failed` to `result.txt`.

  ```
  ## sample input.txt
  search 23
  search 114
  
  ## sample result.txt
  found 23
  search failed
  ```

+ `remove val`:

  Removes a node with value `val` from the BST, return this node, and write `removed <val>` to `result.txt`. If the value does not exist in the tree, return `null` and write `remove failed` to `result.txt`.

  ```
  ## sample input.txt
  remove 23
  remove 114
  
  ## sample result.txt
  removed 23
  remove failed
  ```

+ `print`:

   Implement an iterator in class `BST`, and print out elements in the BST in ascending order to  `result.txt`. 

  ```
  ## sample input.txt
  print
  ## sample result.txt
  2 3 44 214
  ```
  
+ invalid command:

   Write `Invalid Command` to `result.txt`. 
   
   ```
   ## sample input.txt
   Hello CSC201B
   
   ## sample result.txt
   Invalid Command
   ```

Note that you need to **implement an iterator** interface that enables the iterator to traverse all nodes in the BST in ascending order. 

## 3. My Square

For this part of the lab, you adapt the program to work more generically. You will have to find your own data set from an online repository such as [https://www.kaggle.com/](https://www.kaggle.com/). The data set you choose has only three requirements: 1) it must be in a text file in CSV format, 2) it must have between 100 and 100,000 entries, and 3) it must be meaningful in some way to you. You will create a class for the data in your dataset. You will read from the dataset and fill a BST with objects of your custom class.

\begin{enumerate}
    \item Download your own dataset
    \item Create a well written class to store each record from your dataset. The members of this class must include all attributes in your dataset. This class must contain the following methods beside the default, parametrized, and copy constructors:
    \begin{quote}
    @Override\\
    String toString(){}; \\
    \end{quote}
    The method toString() returns a String version of the information stored in the class.  

    \item Create one arrayList to store the objects of your class. 
    \item Read each row in your dataset and store it in an object of your customized class type and then add it to the arrayList.
    \item Implement comparator interface in another customized class to compare 2 objects based on a numerical attribute.

You are going to create a **Comparable** `MySquare ` class in MySquare.java as your own datatype in order to check your BST's support for generic classes. 

The `MySquare` class need to contain those variables: the upper left corner of the square `x:int, y:int` ,  the name of square `name:String` , and side length of the square  `sideLength:int`.

You will compare two squares by comparing the size of their areas.

Try to create a new BST from your own created comparable `MySquare` datatype to check the BST's support for user-defined data types.

You will be encouraged to create another new method in `Parser` for operating BST with `MySquare` nodes. The provided method  `operate_BST(String[] command)` will be only tested by BST with integer nodes, which is also defined in `Parser.java` at line 7: `private BST<Integer> mybst = new BST<>();`. To be more specific, you can implement your operations on BST with `MySquare` nodes as follows:

1. Create a new BST with `MySquare` nodes by:  `private  BST<MySquare> BST_mysquare = new BST<>();` 
2. Create a new method `operate_BST_mysquaree()` in `Parser` class. This method will also be called by method `process()`, and received parameters `command`.
3. Finish your implementation for `operate_BST_mysquaree()` in similar structure of `operate_BST()`, but you're operating the other BST `BST_mysquare` here.

## Submission:

You should submit a compressed .zip archive to Canvas. The .zip file should be named as `Proj1_GroupNumber.zip`and contain files: `Proj1.java`, `BST.java`, `Node.java`, `Parser.java`, `MySquare.java`.

## Rubric (100 points in total):

+ Part 1 BST: 30 points in total
  + Commenting and Code Style: 10 points 
  + Implementation: 20 points
+ Part 2 Parser: 50 points in total
  + Commenting and Code Style: 10 points 
  + Implementation: 20 points
  + Correctness (Test cases): 20 points 
+ Part 3 MySquare: 20 points in total
  + Commenting and Code Style: 10 points 
  + Implementation: 10 points

*In order to get full points of Commenting and Code Style, you need to add comments to every methods and head comments for each file (providing file description, author, date, and acknowledgement).



*/∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗*

∗ @*file: filename. java*

*∗ @description: This program implements . . .*

*∗ @author: Your Name*

*∗ @date: January 20 , 2024*

*∗ @acknowledgement : worked with XXX*

*∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗∗/*
