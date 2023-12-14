# Answer 6

## A1

1. 因为是中断服务，所以 `R7` 中并不保存返回地址，而 `RET` 会跳转到 `R7` 保存的地址，因此在中断服务中直接使用 `RET` 会跳转到错误的位置

2. 直接调用 `RET` 并没有恢复在中断服务中被保存下来的 Processor Status Register，因而并没有从特权模式恢复到用户模式，之前的状态码也没有被恢复

3. `RET` 也不涉及对栈的操作，但从中断服务恢复，应该要恢复栈指针

## A2

## A3

## A4

## A5

1. `WAIT`, `LETTER`, `CONTINUE`, `GETCHAR`, `-65`, `17`
2. R0 << 4, so that we can add the next value to the result.
3. It is not necessary. Dirty data will get shifted out.

Full code:

```assembly
HEX_INPUT
    ST R1, SAVE_R1  ; R1 = Constant 1
    ST R2, SAVE_R2  ; R2 = Constant 2
    ST R3, SAVE_R3  ; R3 = Chars left (counter)
    ST R4, SAVE_R4  ; R4 = Keyboard status / Current char / Value represented by char
    LD R1, C1
    LD R2, C2
    AND R3, R3, #0
    ADD R3, R3, #4
    AND R0, R0, #0  ; R0 stores our result
GETCHAR
    ; R0 << 4
    ADD R0, R0, R0
    ADD R0, R0, R0
    ADD R0, R0, R0
    ADD R0, R0, R0
WAIT
    LDI R4, KBSR    ; Check keyboard status
    BRzp WAIT       ; KBSR[15] = 0, no char available, wait
    LDI R4, KBDR    ; Get KBDR
    ADD R4, R4, R1  ; Check if it is a letter
    BRzp LETTER     ; Got a capital letter
    ADD R4, R4, R2  ; Not a letter -> digit
    BR CONTINUE
LETTER
    ADD R4, R4, #10 ; Add 10 so that A -> 10
CONTINUE
    ADD R0, R0, R4  ; Add to result
    ADD R3, R3, #-1 ; Decr counter
    BRp GETCHAR     ; Wait for another char
    ; Restore regs
    LD R1, SAVE_R1
    LD R2, SAVE_R2
    LD R3, SAVE_R3
    LD R4, SAVE_R4
    RET
; Data
C1      .FILL #-65  ; -ord("A")
C2      .FILL #17   ; ord("A") - ord("0")
KBSR    .FILL xFE00
KBDR    .FILL xFE02
SAVE_R1 .BLKW 1
SAVE_R2 .BLKW 1
SAVE_R3 .BLKW 1
SAVE_R4 .BLKW 1
```

## A6

1. `H3ll0_W0r1d!`
2. $18*2=36$ bytes. (Each instruction takes 2 bytes; don't forget the `\0` at the end of the string.)

## A7

1. It might reads an input character more than once.
2. It might overwrite an input character before it is processed.
3. The first scenario is more likely to happen, because CPU is much faster than human input.

## A8

## A9

## A10
