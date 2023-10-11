# Answer 2

## A1

首先从两个 $Y=1$ 的情况看出上半部分的图中 $A$ 和 $C$ 的位置，然后将 $C=0$ 对应的 $Y$ 填成 $1$，剩下的 $Y$ 填成 $0$，再由 $A=0,B=1,C=1,Y=0$ 得出图中下半部分的 $C$ 的位置，最后通过 $A=1,B=0,C=1,Y=0$ 得出图中下半部分的 $A$ 的位置。

<img src="./hw2/hw2-1-ans.png" style="zoom:50%;" />

|   A   |   B   |   C   |   Y   |
| :---: | :---: | :---: | :---: |
|   0   |   0   |   0   |   1   |
|   0   |   0   |   1   |   1   |
|   0   |   1   |   0   |   1   |
|   0   |   1   |   1   |   0   |
|   1   |   0   |   0   |   1   |
|   1   |   0   |   1   |   0   |
|   1   |   1   |   0   |   1   |
|   1   |   1   |   1   |   0   |

## A2

使用NAND可以得到如下三个基本的逻辑运算：

$$\rm NOT\ a\Leftrightarrow a\ NAND\ a$$
$$\rm a\ AND\ b\Leftrightarrow (a\ NAND\ b)\ NAND\ (a\ NAND\ b)$$
$$\rm a\ OR\ b\Leftrightarrow (a\ NAND\ a)\ NAND\ (b\ NAND\ b)$$

因此，NAND是逻辑完备的。

## A3

## A4

## A5

## A6

## A7

## A8

## A9

## A10
