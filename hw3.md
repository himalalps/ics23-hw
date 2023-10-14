# Homework 3

## T1

Suppose a 32-bit instruction takes the following format:

| OPCODE |  SR   |  DR   |  IMM  |
| :----: | :---: | :---: | :---: |
|        |       |       |       |

If there are 64 opcodes and 56 registers, what is the range of values that can be represented by the immediate (IMM)? Assume IMM is a 2's complement value.

## T2

An LC-3 program is stored in memory locations `x3000` to `x3005`. Note that the branch instruction in memory location `x3002` has an unspecified PCoffset9, denoted as **X**.

| Address | Instruction          |
| :-----: | :------------------- |
| `x3000` | 0101 000 000 1 00000 |
| `x3001` | 0001 000 000 1 00010 |
| `x3002` | 0000 011 **X**       |
| `x3003` | 0001 000 000 1 00011 |
| `x3004` | 0001 000 000 1 00001 |
| `x3005` | 1111 0000 0010 0101  |

The program starts executing with `PC = x4000`.

Your job: In the table below, for each value of **X**, answer the question: "Does the program halt?" (Yes or No). If your answer is "Yes", answer the question: "What value is stored in `R0` immediately after the instruction at `x4004` completes execution?" If your answer is "No", put a dash in the column labeled "Value stored in `R0`".

|   **X**   | Does the program halt? | Value stored in `R0` |
| :-------: | :--------------------: | :------------------: |
| 000000010 |                        |                      |
| 000000001 |                        |                      |
| 000000000 |                        |                      |
| 111111111 |                        |                      |
| 111111110 |                        |                      |

## T3

After these two instructions execute:
The next instruction to execute will be the instruction at x3039 if what?

| Address |         Value         |
| :-----: | :-------------------: |
|  x3000  | 0001 000 001 0 00 010 |
|  x3031  |  0000 011 000000111   |

## T4

Suppose we changed the LC-3 to have only four registers instead of 8. Fewer registers is in general a bad idea since it means loading from memory and storing to memory more often, but we can still ask the question: would there be any benefit to reducing the number of registers? For each of the following, answer yes or no, and explain your answer.

1. If we keep the basic format of all instructions as they currently are (and keep each instruction 16 bits), is there any benefit for operate (0001, 0101, 1001) instructions, if we reduce the number of registers to 4?
2. Is there any benefit for load (0010) and store (0011) instructions, if we reduce the number of registers to 4?
3. Is there any benefit for conditional branch (0000) instructions, if we reduce the number of registers to 4?

## T5

## T6

## T7

## T8

## T9

## T10

