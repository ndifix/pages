# ラムダ計算

この章ではラムダ計算について説明します。

## 定義1.1 λ項

λ項を以下のように定義する

1. 任意の変数 $x$ はλ項である。
1. $M$ がλ項、 $x$ が変数であるとき、 $(\lambda x.M)$ はλ項である。
1. $M$, $N$ が共にλ項のとき、 $(M\, N)$ はλ項である

ここで、

- $(\lambda x.M)$ を関数抽象、$(M\, N)$ を関数適用と呼ぶ。
- 関数抽象よりも関数適用の方が強い結合を持つ。
- $\lambda x.\lambda y.M$ は $\lambda xy.M$ と略記する。

つまり、
$\lambda x.(\lambda y.(f\, x))$ は $\lambda xy. f\, x$に等しい。

## 定義1.2 自由変数

λ項 $M$ の持つ自由変数の集合 $FV(M)$ を以下のように定義する

1. $FV(x) =$ { $x$ }
1. $FV(\lambda x.M) = FV(M)\backslash$ { $x$ }
1. $FV(M\,N) = FV(M) \cup FV(N)$

$FV(\lambda x.M)$ は { $x$ } を含まず、この場合 $x$ は束縛変数と呼ばれる。

## 定義1.3 α変換

$\lambda x.M$ について、 $x$ の $M$ における自由な出現を全て $M$ に現れない別の変数に置き換える操作をα変換という。

λ項 $M, N$ が同一またはα変換によって同一になる場合 $M \equiv N$ と書く。

### 同一視の例

$\lambda x.f\, x \equiv \lambda x.f\, x$  
$\lambda x.f\, x \equiv \lambda y.f\, y$  
$\lambda x.f\, x\, y \not\equiv \lambda y.f\, y\, y$  
$(\lambda x.x\, y)\, z \equiv (\lambda z.z\, y)\, z$  
$\lambda x.(\lambda x.x\, x) \equiv \lambda x.(\lambda y.y\, y)$

複数のλ項 $M_1, \cdots, M_n$ についてそれらの束縛変数と自由変数が重ならないと仮定しても一般性を失わない。この仮定を **BVC (Barendregt variable Convention)** という。

## 定義1.4 代入

任意のλ項 $M, N$ と変数 $x$ に対して、λ項 $M[x:=N]$ を以下のように定める

1. $x[x:=N] = N$
1. $y[x:=N] = y$ (ただし $x\not\equiv y$ )
1. $\lambda x.M[x:=N] = \lambda x.M$
1. $\lambda y.M[x:=N] = \lambda y.(M[x:=N])$ (ただし $x\not\equiv y$ かつ $y\not\in FV(N)$ )
1. $(M_1\, M_2) [x:=N] = (M_1[x:=N])\, (M_2[x:=N])$

## 定義1.5 β簡約

λ項上の二項関係 $\to_\beta$ を以下のように定義する

1. $(\lambda x.M)\, N \to_\beta M[x:=N]$
1. $M_1 \to_\beta M_2$ なら
    - $\lambda x.M_1 \to_\beta \lambda x.M_2$
    - $N\, M_1 \to_\beta N\, M_2$
    - $M_1\, N \to_\beta M_2\, N$

$M \to_\beta M'$ となる $M'$ が存在しない場合 $M$ はβ標準形という。

### 例

1. $(\lambda x.(\lambda y.y\, x))\, (\lambda z.w) \to_\beta \lambda y.y\, (\lambda z.w) \to_\beta \lambda z.w$
1. $(\lambda x.x\, x)\, (\lambda y.y\, y) \to_\beta (\lambda y.y\, y)\, (\lambda y.y\, y)$
1. $(\lambda x.f\, (x\, x))\, (\lambda y.g\, (y\, y)) \to_\beta f\, (\lambda y.g\, (y\, y))\, (\lambda y.g\, (y\, y))$
