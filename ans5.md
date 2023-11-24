# Answer 5

## A1

`.END` 不是一条指令，并不会显式地存放在内存中，只是在汇编语言中标识在哪里停止汇编的一个标识符，而相比起来，`HALT` 是一条指令，它会存放在内存中，当 LC-3 执行到这条命令时，会停机.

## A2

队列的定义特征主要包括以下几点：

1. 先进先出（FIFO）原则：队列中的元素从队尾（rear）进入，从队头（front）出来，最先加入队列的元素将是最先被移除的。
2. 线性结构：队列是一种线性结构，元素之间是一对一的关系，每个元素有且仅有一个前驱和一个后继（除了队头和队尾的特殊元素）。
3. 操作限定：队列的操作主要限定在队头和队尾进行，包括入队（enqueue）操作在队尾添加元素，出队（dequeue）操作在队头移除元素。

## A3

程序中 A 和 B 处存放的值会被当做命令执行，而 `A` 处的 OPCODE 为 1101，是保留的指令，因此会出错；要修正，只需将 `A` 和 `B` 移到 `HALT` 之后即可.

> 如果只将 `A` 移到后面，其实 `B` 处的指令也会报错，因为它是 `STI R7, xEF`，初始化时 x30F0 处的值为 x0000，位于 privilege 区域，不可写，会报错 Access Violation.

## A4

没有问题，因为每个模块会有自己的符号表，没有 `.EXTERNAL` 声明时，只会在自己模块的符号表内查找 `AGAIN`的地址，不会出现冲突.

## A5

1. x0FFF.
2. Yes.
3. Infinite loop. x0FFF interpreted as "BRnzp #-1".

Root cause: LC3 stores data and instructions together, so data might be interpreted as instructions.

Solution: Store data and instructions in separate. (Instruction memory + Data memory)

Comment: Your program will be very tricky if you utilize this behavior of LC3. If you use it well, you might create something amazing; However, it is most likely to cause more trouble than it's worth. However, do note that this may give rise to security issues. In this case, by controlling input data at DATA, one can execute a line of ANY assembly code!

## A6

- `.FILL` 用于存放一个 16 位的数据在它的地址。例如 `.FILL x1234` 将 `x1234` 存放到内存中
- `.BLKW` 用于预留多个字。例如 `.BLKW 3` 将在这个位置留下 3 个字，以便后续存放数据
- `.STRINGZ` 用于在连续的内存中存放字符串。例如 `.STRINGZ "Hello"` 将字符串 中的字符 ASCII 码存放到连续内存中，最后以 0 结尾

| Pseudo-op | 可自定义预留值 | 可占用多个字 |
| --------- | ------------- | ----------- |
| `.FILL`   | 是            | 否          |
| `.BLKW`   | 否            | 是          |
| `.STRINGZ`| 是            | 是          |

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

### 1

```
PUSH A  -> A
PUSH B  -> B, A
POP     -> A (B is removed)
PUSH C  -> C, A
POP     -> A (C is removed)
PUSH D  -> D, A
PUSH E  -> E, D, A
PUSH F  -> F, E, D, A
POP     -> E, D, A (F is removed)
PUSH G  -> G, E, D, A
POP     -> E, D, A (G is removed)
POP     -> D, A (E is removed)
POP     -> A (D is removed)
PUSH H  -> H, A
```

### 2

最多的时候是执行`PUSH F`后或者`PUSH G`后，总共有4个

### 3

```
PUSH I -> H, A, I
POP    -> A, I (H is removed)
PUSH J -> A, I, J
PUSH K -> A, I, J, K
POP    -> I, J, K (A is removed)
PUSH L -> I, J, K, L
POP    -> J, K, L (I is removed)
POP    -> K, L (J is removed)
POP    -> L (K is removed)
POP    -> (Empty) (L is removed)
PUSH M -> M
POP    -> Queue after operation: (Empty) (M is removed)
```

## A10

```assembly
; 假设栈顶指针存储在R6中，栈的元素存储在内存中

; PEEK函数实现
PEEK:   ST R7, SAVE_R7          ; 保存R7的值
        LD R7, STACK_POINTER    ; 加载栈顶指针到R7
        BRZ UNDERFLOW           ; 如果R7为0，则跳转到栈下溢错误处理
        LDR R0, R7, #0          ; 将栈顶的值加载到R0中（不修改栈）
        LD R7, SAVE_R7          ; 恢复R7的原始值
        RET                     ; 返回到调用函数

; 栈下溢错误处理
UNDERFLOW: LEA R0, UNDERFLOW_MSG ; 加载错误信息地址到R0
           PUTS                 ; 输出错误信息
           HALT                 ; 停止程序

; 数据定义
SAVE_R7:   .BLKW #1            ; 用于保存R7的值
STACK_POINTER: .FILL R6         ; 栈顶指针（示例）
UNDERFLOW_MSG: .STRINGZ "Stack underflow error\n"
```

