## 2.1 挿入ソート

### 2.1-1
***
> 図2.2を手本にして, 配列 $A =〈31,41,59,26,41,58〉$ 上での INSERTION-SORTの動作を説明せよ.


```python
def Insertion_sort(A):
    for j in range(1, len(A)):
        key = A[j]
        i = j-1
        while i >= 0 and A[i] > key:
            A[i+1] = A[i]
            i = i-1
        A[i+1] = key

        # 各ループの最後に, 挿入したkeyの値と挿入後の配列Aを表示させれば良い
        print('key =',key, A)
```


```python
A = [31, 41, 59, 26, 41, 58]
Insertion_sort(A)
```

    key = 41 [31, 41, 59, 26, 41, 58]
    key = 59 [31, 41, 59, 26, 41, 58]
    key = 26 [26, 31, 41, 59, 41, 58]
    key = 41 [26, 31, 41, 41, 59, 58]
    key = 58 [26, 31, 41, 41, 58, 59]


### 2.1-2
***
> INSERTION-SORT手続きは非減少順でソートする. これを書き換えて非増加順でソートするようにせよ.


```python
def Insertion_sort(A):
    for j in range(1, len(A)):
        key = A[j]
        i = j-1

        # 条件式を変更して、挿入するkeyの方が大きければ前に持っていくようにすれば良い
        while i >= 0 and A[i] < key:
            A[i+1] = A[i]
            i = i-1
        A[i+1] = key
```


```python
A = [31, 41, 59, 26, 41, 58]
Insertion_sort(A)
print(A)
```

    [59, 58, 41, 41, 31, 26]


### 2.1-3
***
> 以下の**探索問題**(searching problem)を考えよう.
<br>**入力**: 長さ $n$ の数列 $A = (a_1,a_2, . . . ,a_n〉$ とある値 $v$.
<br>**出力**: $v=A[i]$ となる添字 $i$, または $v$ が $A$ の中に存在しないときは特別な値 $NIL$.
<br>**順次探索**(linear search)の擬似コードを書け. 順次探索は $v$ を探しながら列を順に走査するアルゴリズムである. ループ不変式を用いて, このアルゴリズムの正当性を証明せよ.
<br>このループ不変式が必要とされる3つの性質を満たすことを確認せよ.


```python
def Linear_search(A, v):
    for i in range(len(A)):
        if A[i] == v:
            return i
    return 'NIL'
```


```python
A = [31, 41, 59, 26, 41, 58]
Linear_search(A, 40)
```




    'NIL'



* 初期条件: $i = 0$ の時, $A[i] == v$ ならば $i$ を返し,そうでなければ $i += 1$ になるので正しい.
* ループ内条件: $i = k$ までの成立を仮定すると, $i = k+1$ の時に $A[k+1] == v$ ならば $k+1$ を返し, そうでなければ $i += 1$ になるので正しい. 
* 終了条件: ループ終了時, $i = len(A)$ で $A[len(A)] == v$ ならば $len(A)$ を返し, そうでなければ $NIL$ を返すので正しい.

### 2.1-4
***
> 2つの $n$ 要素配列 $A$ と $B$ に蓄えられた2つの $n$ ビットの2進数の和を求める問題を考える. この2つの整数の和は2進数として $(n+1)$ 要素配列 $C$ に蓄える.
<br>この問題を形式的に記述し, 2つの整数の和を求める擬似コードで記せ.


```python
def Binary_addition(A, B):
    n = len(A)
    C = [0 for _ in range(n+1)]
    carry = 0
    for i in reversed(range(n)):
        C[i+1] = A[i] + B[i] + carry
        if C[i+1] > 1:
            C[i+1] -= 2
            carry = 1
        else:
            carry = 0
    C[i] = carry
    return C
```


```python
A = [0, 1, 1, 0, 1]
B = [1, 1, 0, 0, 1]
Binary_addition(A, B)
```




    [1, 0, 0, 1, 1, 0]


