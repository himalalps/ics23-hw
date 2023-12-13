# Answer 6

## A1

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

## A7

## A8

## A9

## A10
