# Answer 5

## A1

`.END` 不是一条指令，并不会显式地存放在内存中，只是在汇编语言中标识在哪里停止汇编的一个标识符，而相比起来，`HALT` 是一条指令，它会存放在内存中，当 LC-3 执行到这条命令时，会停机.

## A2

程序中 A 和 B 处存放的值会被当做命令执行，而 `A` 处的 OPCODE 为 1101，是保留的指令，因此会出错；要修正，只需将 `A` 和 `B` 移到 `HALT` 之后即可.

> 如果只将 `A` 移到后面，其实 `B` 处的指令也会报错，因为它是 `STI R7, xEF`，初始化时 x30F0 处的值为 x0000，位于 privilege 区域，不可写，会报错 Access Violation.

## A3

没有问题，因为每个模块会有自己的符号表，没有 `.EXTERNAL` 声明时，只会在自己模块的符号表内查找 `AGAIN`的地址，不会出现冲突.

## A4

1. x0FFF.
2. Yes.
3. Infinite loop. x0FFF interpreted as "BRnzp #-1".

Root cause: LC3 stores data and instructions together, so data might be interpreted as instructions.

Solution: Store data and instructions in separate. (Instruction memory + Data memory)

Comment: Your program will be very tricky if you utilize this behavior of LC3. If you use it well, you might create something amazing; However, it is most likely to cause more trouble than it's worth. However, do note that this may give rise to security issues. In this case, by controlling input data at DATA, one can execute a line of ANY assembly code!

## A5

## A6

## A7

(a) `NOT R2, R1`
(b) `ADD R2, R2, #1`
(c) `BRz DONE`
(d) `ADD R0, R0, #1`

## A8

## A9

## A10
