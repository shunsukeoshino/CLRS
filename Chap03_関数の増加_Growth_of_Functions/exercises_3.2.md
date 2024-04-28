## 3.2 標準的な記法と一般的な関数

### 3.2-1
***
> $f(n)$ と $g(n)$ が単調増加関数ならば, $f(n)+g(n)とf(g(n)$ も単調増加関数であることを示せ.  $f(n)$ と $g(n)$ がさらに非負ならば,  $f(n) g(n)$ が単調増加であることを示せ. 

* $f(n) + g(n)$

    $n \le m$
    
    $f(n) \le f(m)$ and $g(n) \le g(m)$
    
    $f(n) + g(n) \le f(m) + g(m)$


* $f(g(n))$

    $n \le m$
    
    $f(n) \le f(m)$
    
    $g(f(n)) \le g(f(m))$


* $f(n) \cdot g(n)$

    $n \le m$
    
    $f(n) \le f(m)$ and $g(n) \le g(m)$
    
    $f(n) \cdot g(n) \le f(m) \cdot g(m)$

### 3.2-2
***
> 式(3.16)を証明せよ.

## $a^{log_{b}c}=a^{\frac{log_{a}c}{log_{a}b}}=c^{\frac{1}{log_{a}b}}=c^{log_{b}a}$

### 3.2-3
***
> 式(3.19)を証明せよ. また, $n! = \omega(2^n)$ と $n!=o(n^n)$ を証明せよ.

### 【式(3.19)】
$\lg(n!)=\Theta(n \lg n)$

* $\lg(n!)=\Theta(n \lg n)$

    **スターリングの近似公式**
    
    $\lg(n!) = \lg(\sqrt{2 \pi n}\left (\frac{n}{e}\right )^n e^{\alpha n})$ $=\lg(\sqrt{2 \pi n}) + \lg(\left (\frac{n}{e}\right )^n) + \lg (e^{\alpha n})$ $=\Theta(\lg \sqrt{n}) + \Theta(n\lg n) + \Theta(n)$ $=\Theta(n\lg n)$

* $n! = \omega(2^n)$

    $n!=n \cdot (n-1) \cdot \cdots \cdot 1 \ge 4 \cdot 2 \cdot \cdots \cdot 2 \cdot 1 = 2^n$

* $n!=o(n^n)$

    $n!=n \cdot (n-1) \cdot \cdots \cdot 1 \le n \cdot n \cdot \cdots \cdot n = n^n$

### 3.2-4
***
> ★関数 $\left \lceil \lg n \right \rceil!$ は多項式的に限定されているか?　関数 $\left \lceil \lg \lg n \right \rceil!$ はどうか?

* $\left \lceil \lg n \right \rceil!$

    $\left \lceil \lg n \right \rceil!$ $= \sqrt{2 \pi \lg n}\left (\frac{\lg n}{e}\right )^{\lg n} e^{\alpha \lg n}$ $= \Theta((\lg n)^{\lg n})$
    
    $\lg \left \lceil \lg n \right \rceil!$ $= \Theta(\lg n \lg \lg n)$
    
    $\lg n^p$ $=\Theta(\lg n)$
    
    $\Theta(\lg n \lg \lg n) > \Theta(\lg n)$
    
    $\therefore$ 限定されていない.
    
* $\left \lceil \lg \lg n \right \rceil!$
    
    $\left \lceil \lg \lg n \right \rceil!$ $= \Theta((\lg\lg n)^{\lg \lg n})$
    
    $\lg \left \lceil \lg \lg n \right \rceil!$ $= \Theta(\lg \lg n \lg \lg \lg n)$ $=o(\lg^2\lg n)$
    
    $\because$ $\lg^bn=o(n^a)$
    
    $\therefore$ $o(\lg^2\lg n)$ $=o(\lg n)$, は限定されている.

### 3.2-5
***
> ★関数 $\lg (\lg^{\ast}n)$ と $\lg^{\ast}(\lg n)$ ではどちらが漸近的に大きいか? 

$\lg (\lg^{\ast} (2^m))$ and $\lg^{\ast}(\lg (2^m))$

$\lg (1 + \lg^{\ast}m)$ and $\lg^{\ast}m$

$\because$ $\lg (x)$ < $x$

$\lg^{\ast}(\lg n)$ は $\lg (\lg^{\ast}n)$ よりも漸近的に大きくなる。

### 3.2-6
****
> 黄金比 $\phi$ とその共役 $\hat{\phi}$ は共に方程式 $x^2=x+1$ を満たすことを示せ.

$\phi = \frac{1 + \sqrt{5}}{2}$

$\phi^2=\frac{6+2\sqrt{5}}{4}=\frac{1 + \sqrt{5}}{2} + 1 = \phi + 1$

$\hat{\phi} = \frac{1 - \sqrt{5}}{2}$

$\hat{\phi}^2=\frac{6-2\sqrt{5}}{4}=\frac{1 - \sqrt{5}}{2} + 1 = \hat{\phi} + 1$

### 3.2-7
***
> 帰納法を用いてi番目のフィポナッチ数が等号
> 
> $$F_i=\frac{\phi^{i}-\hat{\phi^i}}{\sqrt{5}}$$
> 
> を満たすことを証明せよ. ただし, $\phi$ は黄金比, $\hat{\phi}$ はその共役である. 

$F_0=0$, $\frac{\phi^{0}-\hat{\phi^0}}{\sqrt{5}}=0$

$F_1=1$, $\frac{\phi-\hat{\phi}}{\sqrt{5}}=1$

$F_{i-2}=\frac{\phi^{i-2}-\hat{\phi^{i-2}}}{\sqrt{5}}$,  $F_{i-1}=\frac{\phi^{i-1}-\hat{\phi^{i-1}}}{\sqrt{5}}$ とする

$F_i=F_{i-2}+F_{i-1}=\frac{1}{\sqrt{5}}(\phi^{i-2}-\hat{\phi^{i-2}} + \phi^{i-1}-\hat{\phi^{i-1}})$

3.2-6より, 

$\phi^{i-2} + \phi^{i-1} = \phi^{i-2}(1+\phi) = \phi^{i-2}\phi^2 = \phi ^ i$

$\therefore$ $F_i=\frac{\phi^{i}-\hat{\phi^i}}{\sqrt{5}}$

### 3.2-8
***
> $k \ln k = \Theta(n)$ ならば $k = \Theta(n / \ln n)$ であることを示せ. 

$c_1n \le k \ln k \le c_2n$

$\ln (c_1n) \le \ln(k \ln k) \le \ln (c_2n)$

$\ln c_1 + \ln n \le \ln k + \ln \ln k \le \ln c_2 + \ln n$

$\because$ $\ln k + \ln \ln k \le 2\ln k \ge \ln c_1 + \ln n$

$\therefore$ $\frac{\ln k}{\ln n} \ge \frac{1}{2}$

$\because$ $\ln k + \ln \ln k \ge \ln k \le \ln c_2 + \ln n$

$\therefore$ $\frac{\ln k}{\ln n} \le 1$

$\because$ $c_1n \le k \ln k \le c_2n$

$\therefore$ $\frac{c_1 n}{\ln n} \le \frac{k \ln k}{\ln n} \le \frac{c_2 n}{\ln n}$

$\therefore$ $\frac{c_1 n}{\ln n} \le \frac{k \ln k}{\ln n} \le k$ and $\frac{c_2 n}{\ln n} \ge \frac{k \ln k}{\ln n} \ge \frac{1}{2}k$

$\therefore$ $c_1\frac{n}{\ln n} \le k \le (2c_2)\frac{n}{\ln n}$

$\therefore$ $k = \Theta(n / \ln n)$
