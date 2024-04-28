## 4.6 マスタ一定理の証明

### 4.6-1
***
> ★ $b$ が任意の実数ではなく正整数である場合について, 式(4.27)の $n_j$ の簡単で正確な式を求めよ. 

$$
n_j=\left \lceil \frac{n}{b^j} \right \rceil
$$

### 4.6-2
***
> ★ $k \ge 0$ とする. $f(n)=\Theta(n^{\log_ba}\lg^kn)$ ならば, マスター漸化式は解 $T(n)=\Theta(n^{\log_ba}\lg^{k+1}n)$ を持つことを示せ. $b$ のベキ乗だけに解析を限定してもよい. 

$$
\begin{align*}
g(n) &= \sum_{j=0}^{\log_b n - 1} a^j f(n/b^j) \\
f(n/b^j) &= \Theta\left( \left(\frac{n}{b^j}\right)^{\log_b a} \lg^k\left(\frac{n}{b^j}\right)\right)\\
g(n) &= \Theta \left( \sum_{j=0}^{\log_b n - 1} a^j \left(\frac{n}{b^j}\right)^{\log_b a} \lg^k \left(\frac{n}{b^j}\right) \right) = \Theta(A)\\
A &= \sum_{j=0}^{\log_b n - 1} a^j \left(\frac{n}{b^j}\right)^{\log_b a} \lg^k \frac{n}{b^j} = n^{\log_b a} \sum_{j=0}^{\log_b n - 1} \left( \frac{a}{b^{\log_b a}} \right)^j \lg^k \frac{n}{b^j}\\
n^{\log_b a} B &= \lg^k \frac{n}{d} = (\lg n - \lg d)^k = \lg^k n + o(\lg^k n)\\
B &= \sum_{j=0}^{\log_b n - 1} \lg^k \frac{n}{b^j} = \sum_{j=0}^{\log_b n - 1} \left( \lg^k n - o(\lg^k n) \right) = \log_b n \lg^k n + \log_b n \cdot o(\lg^k n) = \Theta(\log_b n \lg^k n)\\
\Theta(\log_b n \lg^k n) &= \Theta(\lg^{k+1} n)\\
g(n) &= \Theta(A) = \Theta(n^{\log_b a} B) = \Theta\left(n^{\log_b a} \lg^{k+1} n\right)\\
\end{align*}
$$

### 4.6-3
***
> ★マスタ一定理の場合3を規定する条件は次の意味で冗長であることを証明せよ. すなわち, ある定数 $c < 1$に対して正則性 $af(n/b) \le cf(n)$ が成立するならば, $f(n)=\Omega(n^{\log_ba+\epsilon})$ を満たすある定数 $\epsilon > 0$ が存在する. 


$\quad k = \frac{a}{c} > a$ において, $f(bn) \geq kf(n) \quad $

$\Rightarrow f(b^i) \geq k^i f(1)$


$\quad n = b^i \text{ かつ } i = \log_b n$ のとき, $f(n) \geq k^{\log_b n} f(1)$

$\frac{\log_b n}{\log_b k} = \frac{n^{\log_b k}}{n^{\log_b a}} \text{ で,} \log_b k \geq \log_b a \text{ より, } \log_b k = \log_b a + \epsilon$

