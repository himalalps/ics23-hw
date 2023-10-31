# Homework 4

## T1

Recall the machine busy example from Example 2.11 in Section 2.6.7. Assuming the BUSYNESS bit vector is stored in R2, we can use the LC-3 instruction `0101 011 010 1 00001` (`AND R3, R2, #1`) to determine whether machine 0 is busy or not. If the result of this instruction is 0, then machine 0 is busy.

1. Write an LC-3 instruction that determines whether machine 2 is busy.
2. Write an LC-3 instruction that determines whether both machines 2 and 3 are busy.
3. Write an LC-3 instruction that determines whether all of the machines are busy.
4. Can you write an LC-3 instruction that determines whether machine 6 is busy? Is there a problem here?

## T2

Suppose the following LC-3 program is loaded into memory starting at location x30FF.

| Address |        Value        |
| :-----: | :-----------------: |
|  x30FF  | 1110 0010 0000 0001 |
|  x3100  | 0110 0100 0100 0010 |
|  x3101  | 1111 0000 0010 0101 |
|  x3102  | 0001 0100 0100 0001 |
|  x3103  | 0001 0100 1000 0010 |

If the program is executed, what is the value in R2 at the end of execution?

## T3

The LC-3 ISA contains the instruction `LDR DR, BaseR, offset`. After the instruction is decoded, the following operations (called microinstructions) are carried out to complete the processing of the `LDR` instruction:

```
MAR <- BaseR + SEXT(offset6) ; set up the memory address
MDR <- Memory[MAR] ; read mem at BaseR + offset
DR <- MDR ; load DR
```

Suppose that the architect of the LC-3 wanted to include an instruction `MOVE DR, SR` that would copy the memory location with address given by `SR` and store it into the memory location whose address is in `DR`.

1. The `MOVE` instruction is not really necessary since it can be accomplished with a sequence of existing LC-3 instructions. What sequence of existing LC-3 instructions implements (also called "emulates") `MOVE R0,R1`? (You may assume that no other registers store important values.)
2. If the `MOVE` instruction were added to the LC-3 ISA, what sequence of microinstructions, following the decode operation, would emulate `MOVE DR,SR`?

## T4

## T5

## T6

## T7

## T8

## T9

## T10

`R0` and `R1` contain 16-bit bit vectors. The program below determines if rotating `R1` left by $n$ bits produces the same bit vector that is in `R0`. If yes, the program stores the value $n$ in M[x3020]. If not, the program stores $-1$ to M[x3020].

Rotating left a bit vector by one bit consists of left shifting the bit vector one bit, and then loading into bit[0] the bit that was shifted out of bit[15].

For example, rotating left **111**1000011110000 by 3 bits produces 1000011110000**111**.

Your job: Complete the program below by supplying the missing instructions so it stores $n$ in location M[x3020] if rotating left `R1` by $n$ bits produces the bit vector in `R0`, and store $-1$ if it is not possible to produce the bit vector of `R0` by rotating left `R1`. You are required to only use four registers: `R0`, `R1`, `R2`, and `R3`.

> Hint: The highest bit determines whether a 2's complement is positive or negative.

| Address |         Value         |
| :-----: | :-------------------: |
|  x3000  |  1001 000 000 111111  |
|  x3001  | 0001 000 000 1 00001  |
|  x3002  | 0101 010 010 1 00000  |
|  x3003  | 0001 011 000 0 00 001 |
|  x3004  |                       |
|  x3005  | 0001 010 010 1 00001  |
|  x3006  |                       |
|  x3007  |  0000 010 000000111   |
|  x3008  | 0101 001 001 1 11111  |
|  x3009  |  0000 100 000000010   |
|  x300A  | 0001 001 001 0 00 001 |
|  x300B  |  0000 111 111110111   |
|  x300C  |                       |
|  x300D  |                       |
|  x300E  |  0000 111 111110100   |
|  x300F  | 0101 010 010 1 00000  |
|  x3010  | 0001 010 010 1 11111  |
|  x3011  |                       |
|  x3012  |  1111 0000 0010 0101  |
