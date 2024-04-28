## 4.1 最大部分配列問題

### 4.1-1
***
> $A$ のすべての要素が負のときFIND-MAXIMUM-SUBARRAYは何を返すか?


```python
def Find_max_crossing_subarray(A, low, mid, high):
    left_sum = -10000
    sum = 0

    for i in range(mid, low-1, -1):
        sum += A[i]
        if sum > left_sum:
            left_sum = sum
            max_left = i

    
    right_sum = -10000
    sum = 0

    for j in range(mid+1, high+1):
        sum += A[j]
        if sum > right_sum:
            right_sum = sum
            max_right = j

    return (max_left, max_right, left_sum+right_sum)
```


```python
A = [13, -3, -25, 20, -3, -16, -23, 18, 20, -7, 12, -5, -22, 15, -4, 7]
Find_max_crossing_subarray(A, 0, (len(A)-1)//2, len(A)-1)
```




    (7, 10, 43)




```python
def Find_maximum_subarray(A, low, high):
    if high == low + 1:
        return (low, low, A[low])
    if low >= high:
        return -1, -1, -1e100
        
    mid = (low + high) // 2        
    left_low, left_high, left_sum = Find_maximum_subarray(A, low, mid)
    right_low, right_high, right_sum = Find_maximum_subarray(A, mid, high)
    cross_low, cross_high, cross_sum = Find_max_crossing_subarray(A, low, mid, high)        

    if left_sum >= right_sum and left_sum >= cross_sum:
        return left_low, left_high, left_sum
        
    elif right_sum >= left_sum and right_sum >= cross_sum:
        return right_low, right_high, right_sum
        
    else:
        return cross_low, cross_high, cross_sum
```


```python
A = [13, -3, -25, 20, -3, -16, -23, 18, 20, -7, 12, -5, -22, 15, -4, 7]
Find_maximum_subarray(A, 0, len(A)-1)
```




    (7, 10, 43)




```python
A = [-13, -3, -25, -20, -3, -16, -23, -18, -20, -7, -12, -5, -22, -15, -4, -7]
Find_maximum_subarray(A, 0, len(A)-1)
```




    (1, 1, -3)



* $A$ のすべての要素が負のとき：(最小のインデックス, 最小のインデックス, Aの中の最小値)を返す。

### 4.1-2
***
> 総当り法を用いて最大部分配列問題を解く擬似コードを書け. この擬似コードの実行時間は $\Theta(n^2)$ でなければならない. 


```python
def Find_maximum_subarray_round_robin(A):
    sums = [0]
    for a in A:
        sums.append(sums[-1] + a)
        print(sums)
    max_sum = -1e100
    left_index = -1
    right_index = -1
    for i in range(len(A)):
        for j in range(i, len(A)):
            if sums[j + 1] - sums[i] > max_sum:
                max_sum = sums[j + 1] - sums[i]
                left_index = i
                right_index = j
    return left_index, right_index, max_sum
```


```python
A = [13, -3, -25, 20, -3, -16, -23, 18, 20, -7, 12, -5, -22, 15, -4, 7]
find_maximum_subarray(A)
```




    (7, 10, 43)



* ※sums[j + 1] - sums[i]はA[i]からA[j+1]までの値の合計という意味

### 4.1-3
***
> 最大部分配列問題を解く総当りアルゴリズムと再帰アルゴリズムを計算機上で実現せよ. 再帰アルゴリズムと総当りアルゴリズムの性能が逆転(交差)する最小の問題サイズ $n_0$ を調べよ. 次に, 再帰アルゴリズムの基底をサイズが $n_0$ 以下ならば総当りアルゴリズムを用いるように変更せよ. この変更によって交点の位置は変化するか?

* 特になし

### 4.1-4
***
> 最大部分配列問題の定義を変更して空の部分配列も解として許すようにする. ここで, 空の部分配列の要素の和は0と定義する. 今まで紹介してきた空の部分配列を解として認めないアルゴリズムを, 空の部分配列も解として認めるように変更する方法を示せ. 


```python
def Find_maximum_subarray(A, low, high):
    if A == []:
        return 0
    
    if high == low + 1:
        return (low, low, A[low])
    if low >= high:
        return -1, -1, -1e100
        
    mid = (low + high) // 2        
    left_low, left_high, left_sum = Find_maximum_subarray(A, low, mid)
    right_low, right_high, right_sum = Find_maximum_subarray(A, mid, high)
    cross_low, cross_high, cross_sum = Find_max_crossing_subarray(A, low, mid, high)        

    if left_sum >= right_sum and left_sum >= cross_sum:
        return left_low, left_high, left_sum
        
    elif right_sum >= left_sum and right_sum >= cross_sum:
        return right_low, right_high, right_sum
        
    else:
        return cross_low, cross_high, cross_sum
```


```python
A = []
Find_maximum_subarray(A, 0, len(A)-1)
```




    0



### 4.1-5
***
> 以下のアイデアに基づいて, 最大部分配列問題を解く非再帰的な線形時間アルゴリズムを設計せよ. 配列の左端から開始し, 発見した最大部分配列を保持しながら右方向に処理を進める. $A[1 \dots j]$ の最大部分配列が分かっているとする. $A[1 \dots j+1]$ の最大部分配列は, ($A[j + 1]$ を含まず) $A[1 \dots j]$ の最大部分配列と等しいか, ($A[j+1]$ を含み)ある $1 \le i \le j + 1$ に対して $A[i \dots j+1]$ と書けるかどちらかである. 後者の形の部分配列の中で和が最大のものは, 添字 $j$ で終了する部分配列の中で和が最大のものを保持していれば, 定数時間で決定できる.


```python
def find_maximum_subarray(A):
    max_sum = -1e100
    max_left, max_right = -1, -1
    sum = 0
    last_left = 0
    for i in range(len(A)):
        sum += A[i]
        if sum > max_sum:
            max_sum = sum
            max_left = last_left
            max_right = i
        if sum < 0:
            sum = 0
            last_left = i + 1
        
    return max_left, max_right, max_sum
```


```python
A = [13, -3, -25, 20, -3, -16, -23, 18, 20, -7, 12, -5, -22, 15, -4, 7]
find_maximum_subarray(A)
```




    (7, 10, 43)


