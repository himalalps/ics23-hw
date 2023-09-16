# Homework 1

## T1

1. Convert these decimal numbers to **8-bit** 2's complement numbers:
    - -114
    - +81
2. Convert the following **8-bit** 2's complement numbers to decimal.
    - 0011 0010
    - 1111 1101

## T2

1. What's the smallest and largest number that can be represented by an **8-bit** 2's complement number? (Answer in decimal)
1. Try to determine the range that an **N-bit** 2's complement number can represent. (Answer in decimal)

## T3

The C code below reads two integers and prints out whether the first number is less than the second one. (The numbers input are guaranteed to be in the range of `int`.)

```c
#include <stdio.h>

int main(void) {
    int a, b;
    scanf("%d %d", &a, &b);
    if (a - b < 0) {
        printf("a < b\n");
    } else {
        printf("a >= b\n");
    }
    return 0;
}
```

1. Under what circumstances will the program print `a < b` while actually $a\geqslant b$?
2. What if we change the code to the following? (Also, the numbers input are guaranteed to be in the range of `unsigned int`.)

```c
#include <stdio.h>

int main(void) {
    unsigned int a, b;
    scanf("%d %d", &a, &b);
    if (-a > -b) {
        printf("a < b\n");
    } else {
        printf("a >= b\n");
    }
    return 0;
}
```

## T4

## T5

## T6

## T7

## T8

## T9

## T10

