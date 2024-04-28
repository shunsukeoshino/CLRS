## 4.3 漸化式を解くための置換え法

### 4.3-1
***
> $T(n) = T(n-1) + n$ の解が $O(n^2)$ であることを示せ.

$T(n) \le cn^2$ と仮定.

$$
\begin{array}{lll}
T(n) & \le & \displaystyle c(n-1)^2 + n  \\
     &   = & \displaystyle cn^2 - 2cn + c + n \\
     &   = & \displaystyle cn^2 -(2cn - c - n) \\
     & \le & \displaystyle cn^2
\end{array}
$$

### 4.3-2
***
> $T(n) = T(\left \lceil n / 2 \right \rceil) + 1$ の解が $O(\lg n)$ であることを示せ.

$T(n) \le c\lg n$ と仮定.

$$
\begin{array}{llll}
T(n) & \le & \displaystyle c\lg(\left \lceil n / 2 \right \rceil) + 1 & \\
     & \le & \displaystyle c\lg(n / 2) + 1 & \\
     &  =  & \displaystyle c\lg(n) - c\lg(2) + 1 & \\
     & = & \displaystyle c\lg(n) - c + 1 & \\
     & \le & \displaystyle c\lg(n) & \displaystyle (c \ge 1)
\end{array}
$$

### 4.3-3
***
> $T(n) = 2T(\left \lfloor n / 2 \right \rfloor) + n$ の解が $O(n \lg n)$ であることを説明した. この漸化式の解が $\Omega(n \lg n)$ でもあることを示し, 解が $\Theta(n \lg n)$  であると結論せよ.

$T(n) = 2T(\left \lfloor n / 2 \right \rfloor) + n$ の解が $O(n \lg n)$ より, $T(n) \le cn \lg n$ $(c \ge 1)$

$T(n) \ge cn \lg n$ と仮定.

$$
\begin{array}{llll}
T(n) & \ge & \displaystyle 2c\left \lfloor n / 2 \right \rfloor\lg(\left \lfloor n / 2 \right \rfloor)+n & \\
     & \ge & \displaystyle cn\lg(n / 2)+n & \\
     &  =  & \displaystyle cn\lg n - cn\lg 2 + n & \\
     &  =  & \displaystyle cn\lg n - cn + n & \\
     & \ge & \displaystyle cn\lg n & (c \le 1)
\end{array}
$$

よって, $c = 1$　として, $n \lg n \le T(n) \le n \lg n$　が成り立つことから,  $T(n) = \Theta(n \lg n)$ 

### 4.3-4
***
> 異なった帰納法仮定を用いれば, 帰納的証明に対する境界条件を調整しなくても, 漸化式(4.19)に対する境界条件 $T(1)=1$ に伴う難しさを克服できることを示せ. 

漸化式(4.19)：$T(n) = 2T(\left \lfloor n / 2 \right \rfloor) + n$

$T(n) \le cn \lg n + n$ と仮定.

$$
\begin{array}{llll}
T(n) & \le & \displaystyle 2(c\left \lfloor n / 2 \right \rfloor\lg (\left \lfloor n / 2 \right \rfloor) + \left \lfloor n / 2 \right \rfloor) + n & \\
     & \le & \displaystyle cn\lg (n / 2) + 2n & \\
     & = & \displaystyle cn\lg n - cn + 2n & \\
     & \le & \displaystyle cn\lg n + n &
\end{array}
$$

$n = 1$ のとき, $T(n) = 0 + 1 = 1$ より成立.

### 4.3-5
***
> マージソートに対する“正確”な漸化式(4.3)の解が $\Theta(n\lg n)$ であることを示せ.

漸化式(4.3): $$T(n)=\left\{\begin{matrix}  \Theta(1)  & \text{n = 1のとき}\;  \\ T(\left \lceil n / 2 \right \rceil) + T(\left \lfloor n / 2 \right \rfloor) + \Theta(n) & \text{n > 1のとき}\;\end{matrix}\right.$$

4.3-3より, $T(n) = T(\left \lceil n / 2 \right \rceil) + T(\left \lfloor n / 2 \right \rfloor) + n$ は $O(n \lg n)$ であり, $\Omega(n \lg n)$ でもあるということがわかる.

したがって, $T(n) = \Theta(n\lg n)$

### 4.3-6
***
>  $T(n)=2T(\left \lfloor n/2 \right \rfloor + 17) + n$ の解が $O(n \lg n)$ であることを示せ. 

$T(n) \le cn\lg n$ と仮定.

$$
\begin{array}{llll}
T(n) & \le & \displaystyle 2c(\left \lfloor n / 2 \right \rfloor + 17)\lg (\left \lfloor n / 2 \right \rfloor + 17) + n & \\
     & \le & \displaystyle c(n + 34)\lg (n / 2 + 17) + n & \\
     & ≈ & \displaystyle cn\lg (n / 2) + n & (n は大きい) \\
     & \le & \displaystyle cn\lg n &
\end{array}
$$

### 4.3-7
***
> 第4.5節のマスター法を用いると, 漸化式 $T(n)=4T(n/3)+n$ の解が $T(n)=\Theta(n^{\log_34})$ であることが証明できる. 仮定 $T(n) \le n^{\log_34}$ を用いた置換え法に基づく証明が破綻することを示せ. この仮定から低次の項を適切に引くことで, 置換え法に基づく証明を完成させよ. 

$T(n) \le cn^{\log_34}$ と仮定.

$$
T(n) \le cn^{\log_34}+n
$$

$T(n) \le cn^{\log_34} - an$ と仮定.

$$
\begin{array}{llll}
T(n) & \le & \displaystyle cn^{\log_34} + (1 - \frac{4}{3})n & \\
     & \le & \displaystyle cn^{\log_34} - an & (a \ge 3)
\end{array}
$$

### 4.3-8
***
> 第4.5節のマスター法を用いると, 漸化式 $T(n)=4T(n/2)+n$ の解が $T(n)=\Theta(n^2)$ であることが証明できる. 仮定 $T(n)=cn^2$ を用いた置換え法に基づく証明が破綻することを示せ. この仮定から低次の項を適切に引くことで, 置換え法に基づく証明を完成させよ. 

$T(n) \le cn^2$ と仮定.

$$
T(n) \le cn^2+n
$$

$T(n) \le cn^2 - an$ と仮定.

$$
\begin{array}{llll}
T(n) & \le & cn^2 + (1 - 2a)n & \\
     & \le & cn^2 - an & (a \ge \frac{1}{3})
\end{array}
$$

### 4.3-9
***
> 変数変換によって漸化式 $T(n)=3T(\sqrt{n}) + \lg n$ を解け. 解は漸近的にタイトでなければならない. 値が整数かどうかは気にしないこと. 

$n=2^m$ と変数変換すると,

$T(2^m)=3T(2^{m/2}) + m$

さらに $S(m) = T(2^m)$ とすると,

$S(m) = 3S(m/2)+m$

$S(m) = \Theta(m^{\lg 3})$

よって, $T(n) = S(m) = S(\lg n)$ より,

$T(n) = \Theta((\lg n)^{\lg 3})$
