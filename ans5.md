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

- `.FILL` 用于存放一个 16 位的数据在它的地址。例如 `.FILL x1234` 将 `x1234` 存放到内存中
- `.BLKW` 用于预留多个字。例如 `.BLKW 3` 将在这个位置留下 3 个字，以便后续存放数据
- `.STRINGZ` 用于在连续的内存中存放字符串。例如 `.STRINGZ "Hello"` 将字符串 中的字符 ASCII 码存放到连续内存中，最后以 0 结尾

| Pseudo-op | 可自定义预留值 | 可占用多个字 |
| --------- | ------------- | ----------- |
| `.FILL`   | 是            | 否          |
| `.BLKW`   | 否            | 是          |
| `.STRINGZ`| 是            | 是          |

## A6

## A7

(a) `NOT R2, R1`
(b) `ADD R2, R2, #1`
(c) `BRz DONE`
(d) `ADD R0, R0, #1`

## A8

(a) 2
(b) z
(c) R3, R3
(d) R2, R2, #-1

```assembly
    .ORIG x3000
    LD R0, INP      ; Target
    ; Initialize
    AND R1, R1, #0  ; Result
    ADD R2, R1, #15 ; Loop var i
    ADD R3, R1, #2  ; 2^(16 - i), for AND (Source mask)
    ADD R4, R1, #1  ; 2^(15 - i), for ADD (Dest mask)
    AND R5, R5, #0  ; Temp result
    ; Main Loop
L   AND R5, R3, R0  ; Test bit
    BRz N           ; The bit is 0, skip add
    ADD R1, R1, R4  ; Add dest mask to result
N   ADD R3, R3, R3  ; L-shift source mask
    ADD R4, R4, R4  ; L-shift dest mask
    ADD R2, R2, #-1 ; Decr loop var
    BRp L
    ; End
    HALT
INP .FILL x1234
    .END
```

## A9

## A10
