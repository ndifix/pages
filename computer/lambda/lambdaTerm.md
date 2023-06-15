# λ項

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
