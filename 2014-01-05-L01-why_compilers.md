# Assignment for next class:
* To read: 1.1-1.5, 8.4, 8.5, 9.1
* See slides: Look at source/generated/optimized code for bubblesort

# Why study compilers?
* Good case study of software engineering for complex problems
  * Complicated system prone to bugs—how to slay complexity?
  * When building a metatool, you must think about how others build/use programs
* Combination of theory and practice
* Everyone uses compilers—large ramifications since they impact all programs
* Complex systems that are good to understand due to wide use

## Challenges

* Compilers take in any valid program—complex, infinite input space
* At the same time, strict and difficult objectives:

## Objectives

1. Always produce correct code. Most important
2. Performance of compiler
3. Performance/size of code
4. Detect some errors
5. Flexibility and configurability (different targets...)
6. Reasonable amount of effort to put into implementing the compiler to suit the above

# Defining the right problem: SQL Injection example

* How to write a tool that determines if a program is vulnerable to SQL injection?
  * trace variables that end up in `executeQuery()` calls
  * determine if those variables come from user input
  * at the core, this is **pointer analysis**: Determining if query argument equals (or is derived
      from) user input
  * at the core, this is undecidable—can only do conservative heuristics.
* One solution: write a compiler from vulnerable program's language to an intermediate language,
    PQL (Program Query Language); then convert that into a data-flow language, **datalog**.
  * **Flow-insensitive pointer analysis**: take all statements in program, create a graph of
      relationships of all accessible data in the program, repeatedly run until nothing changes
      anymore. Good technique since the input is unbounded in flow, data available... conservative
      approximation to ignore flow
  * **Context-(in)sensitive** call graphs: When a function is called, do you assume that variables
      are independent of one another or just make the assumption that they are the same? Inferring
      the context for every function call (context-sensitive) has exponential growth of possible
      values for assigned variables. But sacrificing that means you're probably going to get wrong
      answers...
    * If you think of the call graph as a **binary decision diagram** (BDD), you can represent the
	exponential complexity in a compact way.

# Overall goal of compilers:

* You have a high level goal in your actual program
* Map that program to a mathematical abstraction, and use that math to solve your problem
    abstractly
* Apply your findings back to the programs
* Question: **How do you design the right mathematical model and algorithms?**
