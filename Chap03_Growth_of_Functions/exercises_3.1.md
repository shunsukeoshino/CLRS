## 3.1 漸近記法

### 3.1-1
***
> $f(n)$ と $g(n)$ を漸近的に非負の関数とする. $\Theta$ 記法の基本的な定義を用いて, $\max(f(n), g(n)) = \Theta (f(n) + g(n))$ であることを証明せよ.

$\Theta$ 記法の定義によれば、関数 $h(n)$ が $\Theta(g(n))$ であるためには、正の定数 $c_1, c_2$ および自然数 $n_0$ が存在し、全ての $n \geq n_0$ において次が成立する必要があります：

$$
c_1 g(n) \leq h(n) \leq c_2 g(n)
$$

この基準を使用して、$\max(f(n), g(n))$ が $\Theta(f(n) + g(n))$ であることを証明します。

#### 証明:

1. **下界 (Lower Bound)**:
   $\max(f(n), g(n))$ は常に $f(n)$ または $g(n)$ のいずれか大きい方の値を取るので、少なくとも $f(n)$ または $g(n)$ と等しいかそれ以上です。したがって、
   $$
   \max(f(n), g(n)) \geq \frac{1}{2}(f(n) + g(n))
   $$
   が成立します。ここで、$c_1 = \frac{1}{2}$ と設定します。

2. **上界 (Upper Bound)**:
   $\max(f(n), g(n))$ は $f(n) + g(n)$ よりも常に小さいか等しいです。なぜなら、最大値は合計値を超えることができないからです。したがって、
   $$
   \max(f(n), g(n)) \leq f(n) + g(n)
   $$
   が成立します。ここで、$c_2 = 1$ と設定します。

これらの条件から、全ての $n \geq n_0$（$n_0$ を適当に選ぶ）において、
$$
\frac{1}{2}(f(n) + g(n)) \leq \max(f(n), g(n)) \leq f(n) + g(n)
$$
が成立します。これにより、
$$
\max(f(n), g(n)) = \Theta(f(n) + g(n))
$$
が証明されます。

### 3.1-2
***
> 任意の実定数 $ a $ と実正定数 $ b>0 $ に対して $ (n+a)^b=\Theta(n^b) $ であることを示せ. 

関数 $h(n) = (n+a)^b$ が $\Theta(g(n))$、ここで $g(n) = n^b$、であるためには、正の定数 $c_1, c_2$ および自然数 $n_0$ が存在し、すべての $n \geq n_0$ において
$$
c_1 n^b \leq (n+a)^b \leq c_2 n^b
$$
が成立する必要があります。

**上限**: 
$$
(n+a)^b = n^b \left(1 + \frac{a}{n}\right)^b \approx n^b \left(1 + b \frac{a}{n}\right)
$$
上記から、定数 $c_2 > 1$ を選べば、$(n+a)^b \leq c_2 n^b$ が成立します。

**下限**: 
$$
(n+a)^b \geq n^b
$$
を使用し、定数 $c_1 = 1$ を選べば、$(n+a)^b \geq c_1 n^b$ が成立します。

これにより、十分大きな $n$ に対して $(n+a)^b = \Theta(n^b)$ が示されます。

### **【別解】**


$a$ は実定数で、$b > 0$ は実正定数です。$n^b$ に対する $(n+a)^b$ の振る舞いを比較します。

まず、次のような不等式を考えます：
$$
(n+a)^b = n^b \left(1 + \frac{a}{n}\right)^b
$$
ビネの公式または二項展開により、$\left(1 + \frac{a}{n}\right)^b$ は $n$ が大きくなるにつれて 1 に収束します。正確には、
$$
\left(1 + \frac{a}{n}\right)^b \sim 1 + b\frac{a}{n}
$$
であり、これは $n \to \infty$ で $1$ に収束するため、$(n+a)^b = \Theta(n^b)$ が成立します。

### 3.1-3
***
> 文「アルゴリズム $A$ の実行時間は少なくとも $O(n^2)$ である」が無意味である理由を説明せよ. 

$O$ 表記は上限（最悪の場合の境界）を意味します。したがって、「少なくとも $O(n^2)$」という表現は、「$n^2$ よりも速くないことが保証されている」と読むことができますが、これは意味がありません。

なぜなら、$O(n^2)$ は $n^2$ よりも悪くないという上限を示しているからです。

### 3.1-4
***
> $2^{n+1}=O(2^n)$ は成立するか? $2^{2n}=O(2^n)$ はどうか?

$2^{n+1} = 2 \cdot 2^n$ であり、これは $2^n$ の定数倍です。したがって、$2^{n+1} = O(2^n)$ は成立します。

一方で、$2^{2n} = (2^n)^2$ であり、これは $2^n$ の二乗です。従って、$2^{2n}$ は $2^n$ に対して指数関数的に増加するため、$2^{2n} = O(2^n)$ は成立しません。

### 3.1-5
***
> 定理3.1を証明せよ

### 【定理3.1】
任意の2つの関数 $f(n)$ と $g(n)$ に対して, $f(n)=\Theta(g(n))$ であるための必要十分条件は $f(n)=O(g(n)$ かつ $f(n)= \Omega(g(n))$ である. 

####  【$f(n)=\Theta(g(n))$ の必要十分条件の証明】

$f(n)=\Theta(g(n))$ であるとは、関数 $f(n)$ と $g(n)$ が同じ成長率を持つことを意味します。具体的には、正の定数 $c_1, c_2$ および自然数 $n_0$ が存在し、すべての $n \geq n_0$ において
$$
c_1 g(n) \leq f(n) \leq c_2 g(n)
$$
が成立することです。

**十分条件**: $f(n)=O(g(n))$ かつ $f(n)=\Omega(g(n))$ であれば、定義により、ある定数 $c_2$ と $n_1$ が存在して、$n \geq n_1$ に対して $f(n) \leq c_2 g(n)$ が成立します。また、$f(n)=\Omega(g(n))$ であるためには、ある定数 $c_1$ と $n_2$ が存在して、$n \geq n_2$ に対して $f(n) \geq c_1 g(n)$ が成立します。したがって、$n_0 = \max(n_1, n_2)$ として、すべての $n \geq n_0$ で上記の $\Theta$ の定義を満たします。

**必要条件**: $f(n)=\Theta(g(n))$ である場合、上記の定義から直接 $f(n)=O(g(n))$ および $f(n)=\Omega(g(n))$ が導かれます。

### 3.1-6
****
> アルゴリズムの実行時間が $\Theta(g(n))$ であるための必要十分条件は, その最悪実行時間が $O(g(n))$ であり, かつその最良実行時間が $\Omega(g(n))$ であることを証明せよ. 

$\Theta(g(n))$ は $g(n)$ によって正確に境界付けられることを意味します。つまり、ある正の定数 $c_1, c_2$ と十分に大きな $n$ が存在して、
$$
c_1 g(n) \leq T(n) \leq c_2 g(n)
$$
が成立します。これは、$T(n)$ が $O(g(n))$（$T(n) \leq c_2 g(n)$）および $\Omega(g(n))$（$T(n) \geq c_1 g(n)$）の両方であることを意味します。このことから、$\Theta(g(n))$ が $O(g(n))$ かつ $\Omega(g(n))$ であることが必要十分であることがわかります。

### 3.1-7
***
> $o(g(n)) \cap \omega(g(n))$ が空集合であることを証明せよ.

$o(g(n))$ は $g(n)$ よりも厳密に遅く増加する関数の集合を示し、$\omega(g(n))$ は $g(n)$ よりも厳密に速く増加する関数の集合を示します。明らかに、これら二つの性質は同時に成立することができません。

なぜなら、ある関数が $g(n)$ よりも厳密に速く増加しつつ、同時に厳密に遅く増加することは不可能だからです。従って、$o(g(n)) \cap \omega(g(n))$ は空集合です。

### 3.1-8
***
> 2つの引数 $m$ と $n$ が独立に異なる速度で無限大に発散する場合を含むように記法を拡張できる. 与えられた関数 $g(n,m)$ に対して, $O(g(n,m))$ によって関数の集合
>
> $O(g(n,m))= {f(n,m) : 正定数 c, n_0, m_0 が存在して, n \ge n_0 あるいは m \ge m_0 を満たすすべての n, m に対して 0 \le f(n,m) \le c g(n,m) を満たす}$
> 
> を表す. $\Omega(g(n,m))$ と $\Theta(g(n,m))$ について対応する定義を求めよ.

与えられた定義に基づき、$O(g(n,m))$ は次のように定義されます：
$$
O(g(n,m))= \{f(n,m) : \exists c > 0, n_0, m_0 \text{ で } n \ge n_0 \text{ または } m \ge m_0 \text{ を満たすすべての } n, m \text{ に対して } 0 \le f(n,m) \le c g(n,m)\}
$$

**$\Omega(g(n,m))$ の定義**:
$$
\Omega(g(n,m))= \{f(n,m) : \exists c > 0, n_0, m_0 \text{ で } n \ge n_0 \text{ または } m \ge m_0 \text{ を満たすすべての } n, m \text{ に対して } 0 \le c g(n,m) \le f(n,m)\}
$$

**$\Theta(g(n,m))$ の定義**:
$$
\Theta(g(n,m))= \{f(n,m) : \exists c_1 > 0, c_2 > 0, n_0, m_0 \text{ で } n \ge n_0 \text{ または } m \ge m_0 \text{ を満たすすべての } n, m \text{ に対して } c_1 g(n,m) \le f(n,m) \le c_2 g(n,m)\}
$$