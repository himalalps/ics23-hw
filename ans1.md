# Answer X

## A1

## A2

## A3

1. `int`型的范围为$-2^{31}\sim2^{31}-1$，因此两个`int`型变量相减得到的结果范围也最多为$-2^{31}\sim2^{31}-1$，如果变量`a`比变量`b`大超过$2^{31}$，则`a - b`会溢出，结果为负数，此时会输出`a < b`.
2. `unsigned int`型取负数也是取反加一，不过结果会被作为`unsigned int` 看待，因此$-a$相当于$2^{32}-a$，不过有一个特殊的数`0`，其取负之后依然为`0`，因此如果`b = 0`，而`a`非零，就会输出`a < b`.

## A4

## A5

## A6

## A7

## A8

## A9

## A10