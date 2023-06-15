# ラムダ計算

この章ではラムダ計算について説明します。

## 定義1.1 λ項

λ項を以下のように定義する

1. 任意の変数 $x$ はλ項である。
1. $M$ がλ項、 $x$ が変数であるとき、 $(\lambda x.M)$ はλ項である。
1. $M$, $N$ が共にλ項のとき、 $(M\ N)$ はλ項である

ここで、

- $(\lambda x.M)$ を関数抽象、 $(M\ N)$ を関数適用と呼ぶ。
- 関数抽象よりも関数適用の方が強い結合を持つ。
- $\lambda x.\lambda y.M$ は $\lambda xy.M$ と略記する。

つまり、
$\lambda x.(\lambda y.(f\ x))$ は $\lambda xy. f\ x$に等しい。

## 定義1.2 自由変数

λ項 $M$ の持つ自由変数の集合 $FV(M)$ を以下のように定義する

1. $FV(x) =$ { $x$ }
1. $FV(\lambda x.M) = FV(M)\backslash$ { $x$ }
1. $FV(M\ N) = FV(M) \cup FV(N)$

$FV(\lambda x.M)$ は { $x$ } を含まず、この場合 $x$ は束縛変数と呼ばれる。

## 定義1.3 α変換

$\lambda x.M$ について、 $x$ の $M$ における自由な出現を全て $M$ に現れない別の変数に置き換える操作をα変換という。

λ項 $M, N$ が同一またはα変換によって同一になる場合 $M \equiv N$ と書く。

### 同一視の例

$\lambda x.f\ x \equiv \lambda x.f\ x$  
$\lambda x.f\ x \equiv \lambda y.f\ y$  
$\lambda x.f\ x\ y \not\equiv \lambda y.f\ y\ y$  
$(\lambda x.x\ y)\ z \equiv (\lambda z.z\ y)\ z$  
$\lambda x.(\lambda x.x\ x) \equiv \lambda x.(\lambda y.y\ y)$

複数のλ項 $M_1, \cdots, M_n$ についてそれらの束縛変数と自由変数が重ならないと仮定しても一般性を失わない。この仮定を **BVC (Barendregt variable Convention)** という。

## 定義1.4 代入

任意のλ項 $M, N$ と変数 $x$ に対して、λ項 $M[x:=N]$ を以下のように定める

1. $x[x:=N] = N$
1. $y[x:=N] = y$ (ただし $x\not\equiv y$ )
1. $\lambda x.M[x:=N] = \lambda x.M$
1. $\lambda y.M[x:=N] = \lambda y.(M[x:=N])$ (ただし $x\not\equiv y$ かつ $y\not\in FV(N)$ )
1. $(M_1\ M_2) [x:=N] = (M_1[x:=N])\ (M_2[x:=N])$

## 定義1.5 β簡約

λ項上の二項関係 $\to_\beta$ を以下のように定義する

1. $(\lambda x.M)\ N \to_\beta M[x:=N]$
1. $M_1 \to_\beta M_2$ なら
    - $\lambda x.M_1 \to_\beta \lambda x.M_2$
    - $N\ M_1 \to_\beta N\ M_2$
    - $M_1\ N \to_\beta M_2\ N$

$M \to_\beta M'$ となる $M'$ が存在しない場合 $M$ はβ標準形という。

### 例

1. $(\lambda x.(\lambda y.y\ x))\ (\lambda z.w) \to_\beta \lambda y.y\ (\lambda z.w) \to_\beta \lambda z.w$
1. $(\lambda x.x\ x)\ (\lambda y.y\ y) \to_\beta (\lambda y.y\ y)\ (\lambda y.y\ y)$
1. $(\lambda x.f\ (x\ x))\ (\lambda y.g\ (y\ y)) \to_\beta f\ (\lambda y.g\ (y\ y))\ (\lambda y.g\ (y\ y))$

## 定理1.1 チャーチ・ロッサーの定理

任意のλ項 $M, N_1, N_2 について、空でもよいβ簡約の有限列 $M \to_\beta \cdots \to_\beta N_1$ と $M \to_\beta \cdots \to_\beta N_2$ が存在するとき、あるλ項 $N$ が存在して、空でもよいβ簡約の列 $N_1 \to_\beta \cdots \to_\beta N$ と $N_2 \to_\beta \cdots \to_\beta N$ が存在する。

この定理から以下の命題が従う。

## 命題1.1 β正規形の一意性

任意のβ項 $M$ は高々1つのβ正規形を持つ。

## 定義1.6 自然数

自然数を以下のように定義する

- $0$ は $c_0 \equiv \lambda f.\lambda x. x$ として定める。
- $succ$ は $\lambda m.\lambda f.\lambda x.f\ (m\ f\ x)$ として定める

このとき  
$c_1$  
$\equiv succ\ c_0$  
$\equiv (\lambda m.\lambda f.\lambda x.f\ (m\ f\ x))\ (\lambda f.\lambda x. x)$  
$\to_\beta \lambda f.\lambda x.f\ (((\lambda g.\lambda y. y)\ f)\ x)$  
$\to_\beta \lambda f.\lambda x.f\ (\lambda y. y\ x)$  
$\to_\beta \lambda f.\lambda x.f\ x$  

$c_2$  
$\equiv succ\ c_1$  
$\equiv succ\ \lambda f.\lambda x.f\ x$  
$\equiv \lambda m.\lambda f.\lambda x.f\ (m\ f\ x)\ (\lambda f.\lambda x.f\ x)$  
$\to_\beta \lambda f.\lambda x.f\ ((\lambda g.\lambda y.g\ y)\ f\ x)$  
$\to_\beta \lambda f.\lambda x.f\ ((\lambda y.f\ y)\ x)$  
$\to_\beta \lambda f.\lambda x.f\ (f\ x)$  

したがって $c_n \equiv \lambda f.\lambda x.f\ (f\cdots (f\ x))$ となる。

この表現方法をチャーチ・エンコーディングという。

## 定義1.7 算術関数・論理式

以下のように関数を定める

- $sub := \lambda n.\lambda f.\lambda x.n\ (\lambda g.\lambda h.h\ (g\ f))\ (\lambda y.x)\ (\lambda y.y)$
- $add := \lambda m.\lambda n. \lambda f.\lambda x.m\ f\ (n\ f\ x)$
- $mul := \lambda m.\lambda n.\lambda f.\lambda x.m\ (n\ f)\ x$
- $true := \lambda x.\lambda y.x$
- $false := \lambda x.\lambda y.y \equiv c_0$
- $and := \lambda p.\lambda q. p\ q\ false$
- $or := \lambda p.\lambda q. p\ true\ q$
- $not := \lambda p. p\ false\ true$
- $if := \lambda p.\lambda x.\lambda y. p\ x\ y$

### 計算例

$sub\ c_0$  
$\equiv (\lambda n.\lambda f.\lambda x.n\ (\lambda g.\lambda h.h\ (g\ f))\ (\lambda y.x)\ (\lambda y.y))\ (\lambda f.\lambda x. x)$  
$\to_\beta \lambda f.\lambda x.(\lambda f.\lambda x. x)\ (\lambda g.\lambda h.h\ (g\ f))\ (\lambda y.x)\ (\lambda y.y)$  
$\to_\beta \lambda f.\lambda x.(\lambda x. x)\ (\lambda y.x)\ (\lambda y.y)$  
$\to_\beta \lambda f.\lambda x.(\lambda y.x)\ (\lambda y.y)$  
$\to_\beta \lambda f.\lambda x.x$  
$\equiv c_0$

$sub\ c_1$  
$\equiv (\lambda n.\lambda f.\lambda x.n\ (\lambda g.\lambda h.h\ (g\ f))\ (\lambda y.x)\ (\lambda y.y))\ (\lambda f.\lambda x.f\ x)$  
$\to_\beta \lambda f.\lambda x.(\lambda f.\lambda x.f\ x)\ (\lambda g.\lambda h.h\ (g\ f))\ (\lambda y.x)\ (\lambda y.y)$  
$\to_\beta \lambda f.\lambda x.(\lambda x.(\lambda g.\lambda h.h\ (g\ f))\ x)\ (\lambda y.x)\ (\lambda y.y)$  
$\to_\beta \lambda f.\lambda x.(\lambda g.\lambda h.h\ (g\ f))\ (\lambda y.x)\ (\lambda y.y)$  
$\to_\beta \lambda f.\lambda x.(\lambda h.h\ (\lambda y.x)\ f)\ (\lambda y.y)$  
$\to_\beta \lambda f.\lambda x.(\lambda y.y)\ (\lambda y.x)\ f$  
$\to_\beta \lambda f.\lambda x.(\lambda y.x)\ f$  
$\to_\beta \lambda f.\lambda x.x$  
$\equiv c_0$

## 定義1.8 不動点コンビネータ

以下の性質を持つλ項 $M$ を不動点コンビネータという。すなわち  
$M\ g \to_\beta \cdots \to_\beta g\ (M\ g)$

### 例 Yコンビネータ

$Y := \lambda f.(\lambda x.f\ (x\ x))\ (\lambda x.f\ (x\ x))$
をYコンビネータという。実際、  
$Y\ g$  
$\equiv \lambda f.(\lambda x.f\ (x\ x))\ (\lambda x.f\ (x\ x))\ g$  
$\to_\beta (\lambda x.g\ (x\ x))\ (\lambda x.g\ (x\ x))$  
$\to_\beta g\ ((\lambda x.h\ (x\ x))\ (\lambda x.h\ (x\ x)))$  
$\leftarrow_\beta g\ (Y\ g)$

これは広義の不動点コンビネータになっている。

### 例 Θコンビネータ

$\Theta := (\lambda x.\lambda y.y\ (x\ x\ y))\ (\lambda x.\lambda y.y\ (x\ x\ y))$ は

$\Theta\ g$  
$\equiv (\lambda x.\lambda y.y\ (x\ x\ y))\ (\lambda x.\lambda y.y\ (x\ x\ y))\ g$  
$\to_\beta (\lambda y.y\ ((\lambda x.\lambda y.y\ (x\ x\ y))\ (\lambda x.\lambda y.y\ (x\ x\ y))\ y))\ g$  
$\to_\beta g\ ((\lambda x.\lambda y.y\ (x\ x\ y))\ (\lambda x.\lambda y.y\ (x\ x\ y))\ g)$  
$\equiv g\ (\Theta\ g)$
