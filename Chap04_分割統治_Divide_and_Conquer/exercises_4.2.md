## 4.2 行列積のためのStrassenのアルゴリズム

### 4.2-1
***
> 行列積
>
> $\begin{pmatrix} 1 & 3 \\ 7 & 5 \end{pmatrix}\begin{pmatrix} 6 & 8 \\ 4 & 2 \end{pmatrix}$
>
> をStrasenのアルゴリズムを用いて計算せよ. 計算過程を説明せよ. 

$S_1 = B_{12} - B_{22} = 8 - 2 = 6$

$S_2 = A_{11} + A_{12} = 1 + 3 = 4$

$S_3 = A_{21} + A_{22} = 7 + 5 = 12$

$S_4 = B_{21} - B_{11} = 4 - 6 = -2$

$S_5 = A_{11} + A_{22} = 1 + 5 = 6$

$S_6 = B_{11} + B_{22} = 6 + 2 = 8$

$S_7 = A_{12} - A_{22} = 3 - 5 = -2$

$S_8 = B_{21} + B_{22} = 4 + 2 = 6$

$S_9 = A_{11} - A_{21} = 1 - 7 = -6$

$S_{10} = B_{11} + B_{12} = 6 + 8 = 14$

$P_1 = A_{11} \cdot S_1 = 1 \times 6 = 6$

$P_2 = S_{2} \cdot B_{22} = 4 \times 2 = 8$

$P_3 = S_{3} \cdot B_{11} = 12 \times 6 = 72$

$P_4 = A_{22} \cdot S_4 = 5 \times -2 = -10$

$P_5 = S_{5} \cdot S_6 = 6 \times 8 = 48$

$P_6 = S_{7} \cdot S_8 = -2 \times 6 = -12$

$P_7 = S_{9} \cdot S_{10} = -6 \times 14 = -84$

$C_{11} = P_5 + P_4 - P_2 + P_6 = 48 - 10 - 8 - 12 = 18$

$C_{12} = P_1 + P_2 = 8 + 6 = 14$

$C_{21} = P_3 + P_4 = 72 - 10 = 62$

$C_{22} = P_5 + P_1 - P_3 - P_7 = 48 + 6 - 72 + 84 = 66$

$$\begin{pmatrix} 18 & 14 \\ 62 & 66 \end{pmatrix}$$

### 4.2-2
***
> Strasenのアルゴリズムの擬似コードを書け.


```python
def Matrix_product_strassen_sub(a, b, r_low, r_high, c_low, c_high):
    n = r_high - r_low
    if n == 1:
        return [[a[r_low][c_low] * b[r_low][c_low]]]
    mid = n // 2
    r_mid = (r_low + r_high) // 2
    c_mid = (c_low + c_high) // 2
    s = [[[0 for _ in range(mid)] for _ in range(mid)] for _ in range(10)]
    for i in range(mid):
        for j in range(mid):
            s[0][i][j] = b[r_low + i][c_mid + j] - b[r_mid + i][c_mid + j]
            s[1][i][j] = a[r_low + i][c_low + j] + a[r_low + i][c_mid + j]
            s[2][i][j] = a[r_mid + i][c_low + j] + a[r_mid + i][c_mid + j]
            s[3][i][j] = b[r_mid + i][c_low + j] - b[r_low + i][c_low + j]
            s[4][i][j] = a[r_low + i][c_low + j] + a[r_mid + i][c_mid + j]
            s[5][i][j] = b[r_low + i][c_low + j] + b[r_mid + i][c_mid + j]
            s[6][i][j] = a[r_low + i][c_mid + j] - a[r_mid + i][c_mid + j]
            s[7][i][j] = b[r_mid + i][c_low + j] + b[r_mid + i][c_mid + j]
            s[8][i][j] = a[r_low + i][c_low + j] - a[r_mid + i][c_low + j]
            s[9][i][j] = b[r_low + i][c_low + j] + b[r_low + i][c_mid + j]
    p = [[[0 for _ in range(mid)] for _ in range(mid)] for _ in range(7)]
    for i in range(mid):
        for j in range(mid):
            for k in range(mid):
                p[0][i][j] += a[r_low + i][c_low + k] * s[0][k][j]
                p[1][i][j] += s[1][i][k] * b[r_mid + k][c_mid + j]
                p[2][i][j] += s[2][i][k] * b[r_low + k][c_low + j]
                p[3][i][j] += a[r_mid + i][c_mid + k] * s[3][k][j]
                p[4][i][j] += s[4][i][k] * s[5][k][j]
                p[5][i][j] += s[6][i][k] * s[7][k][j]
                p[6][i][j] += s[8][i][k] * s[9][k][j]
    c = [[0 for _ in range(n)] for _ in range(n)]
    for i in range(mid):
        for j in range(mid):
            c[r_low + i][c_low + j] = p[4][i][j] + p[3][i][j] - p[1][i][j] + p[5][i][j]
            c[r_low + i][c_mid + j] = p[0][i][j] + p[1][i][j]
            c[r_mid + i][c_low + j] = p[2][i][j] + p[3][i][j]
            c[r_mid + i][c_mid + j] = p[4][i][j] + p[0][i][j] - p[2][i][j] - p[6][i][j]
    return c


def Matrix_product_strassen(a, b):
    n = len(a)
    return matrix_product_strassen_sub(a, b, 0, n, 0, n)
```

### 4.2-3
***
> $n$ が $2$ のベキではないときにも正しく働くように $n \times n$ 型行列の積を計算するStrasenのアルゴリズムを変更せよ. 変更を加えたアルゴリズムが $\Theta(n^{\lg 7})$ 時間で実行できることを示せ. 

入力行列を2のべき乗にパディングしてから指定されたアルゴリズムを実行することができます。次に大きな2のべき乗（これを \( m \) と呼びます）へのパディングは、2の各べき乗が互いに2の因子で異なるため、\( n \) の値を最大で2倍にするだけです。したがって、この実行時間は


$m^{\log 7} \leq (2n)^{\log 7} = 7n^{\log 7} = O(n^{\log 7})$

となり、そして

$m^{\log 7} \geq n^{\log 7} \in \Omega(n^{\log 7})$

を組み合わせると、実行時間は $\Theta(n^{\log 7})$ となります。

### 4.2-4
***
>  $ 3 \times3 $ 型行列の乗算が $ k $ 回の乗算(乗算の可換性は仮定しない)によって実現できることから,  $ n \times n $ 型行列の乗算が $ \Theta(n^{\lg7}) $ 時間で計算できることが帰結できる最大の $ k $ を求めよ. このアルゴリズムの実行時間を求めよ.

$T(n) = kT(n/3) + O(n^2)$

実行時間: $\Theta(n^{\log_3 7})$

$k \le 3^{\lg 7} \approx 21.84986222490514$

### 4.2-5
***
> V.Pan(パン)は $68 \times 68$ 型行列を $132,464$ 回の乗算を用いて行う方法, $70 \times 70$ 型行列を $143,640$ 回の乗算を用いて行う方法, $72 \times 72$ 型行列を $15,424$ 回の乗算を用いて行う方法を発見した. それぞれを分割統治行列積アルゴリズムの中で用いるとき, どの方法が最良の漸近的実行時間を実現するか. 最良のものをStrasenのアルゴリズムと比較せよ. 

$T_1 = \Theta(n^{\log_{68}132464}) = \Theta(n^{2.7951284873613815})$

$T_2 = \Theta(n^{\log_{70}143640}) = \Theta(n^{2.795122689748337})$

$T_3 = \Theta(n^{\log_{72}155424}) = \Theta(n^{2.795147391093449})$

$T_2 < T_1 < T_3 < \Theta(n^{\lg 7})$

### 4.2-6
***
> Strasenのアルゴリズムをサプルーチンに用いて $kn \times n$ 型行列と $n \times kn$ 型行列の積を計算するアルゴリズムの実行時間を解析せよ. 入力行列の順序を逆にするとき, 同じ質問に
答えよ.

$\Theta(k^2n^{\lg 7})$

逆順: $\Theta(kn^{\lg 7})$

### 4.2-7
***
> 3回の実数乗算を用いて複素数 $a + bi$ と $c + di$ の積が計算できることを示せ. アルゴリズムは入力として $a$, $b$, $c$, $d$ を取り, 実数部 $ac - bd$ と虚数部 $ad + bc$ を別々に出力しなければならない. 

$P_1 = a \cdot (c - d)$

$P_2 = b \cdot (c + d)$

$P_3 = d \cdot (a - b)$

実数部: $P_1 + P_3$

虚数部: $P_2 + P_3$
