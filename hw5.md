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

## T4

Your friend has just written a simple program intended to calculate complements, which is as follows:

```assembly
.ORIG   x3000
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

## T8

## T9

## T10

