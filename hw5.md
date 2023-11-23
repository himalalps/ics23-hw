# Homework 5

## T1

What is the purpose of the `.END` pseudo-op? How does it differ from the `HALT` instruction?

## T2

The following program has an error in it. What is the error? How would you fix it?

```assembly
    .ORIG x3000
A   .FILL xDEAD
B   .FILL xBEEF
    LD R0, A
    ST R0, B
    HALT
    .END
```

## T3

Suppose you write two separate assembly language modules that you expect to be combined by the linker. Each module uses the label `AGAIN`, and neither module contains the pseudo-op `.EXTERNAL AGAIN`. Is there a problem using the label `AGAIN` in both modules? Why or why not?

## T4

Your friend has just written a simple program intended to calculate complements, which is as follows:

```assembly
.ORIG x3000
    ; Simple program that should calculate complement of DATA and store the result back
    LD R2, DATA
    NOT R2, R2
    ADD R2, R2, #1
    ST R2, DATA
    DATA .FILL xF001 ; <- Put your data here
.END
```

However, it does not seem to be reliable for some reason...

Questions:

1. What's the complement of xF001 in hex?
2. Will the program store the complement to DATA?
3. What will happen afterwards? Why?

> Open questions (Answer if you like, but it **WILL NOT** be graded):
> What's the root cause of this phenomenon? How can we prevent this from happening?

## T5

## T6

## T7

It is often useful to find the midpoint between two values. **For this problem, assume A and B are both even numbers, and A is less than B.** For example, if A = 2 and B = 8, the midpoint is 5. The following program finds the midpoint of two even numbers A and B by continually incrementing the smaller number and decrementing the larger number. You can assume that `A` and `B` have been loaded with values before this program starts execution.

Your job: Insert the missing instructions.

```assembly
    .ORIG x3000
    LD R0,A
    LD R1,B
X   ________________ (a)
    ________________ (b)
    ADD R2,R2,R1
    ________________ (c)
    ADD R1,R1,#-1
    ________________ (d)
    BRnzp X
DONE ST R1,C
    TRAP x25
A   .BLKW 1
B   .BLKW 1
C   .BLKW 1
    .END
```

## T8

## T9

## T10

