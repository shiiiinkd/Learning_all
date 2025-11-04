

## 学んだこと：実数探索と整数探索の実装の違い
- `実数探索なら while left < right は使わない
- `探索範囲は解を挟むようにとる（左側はOK,右側はNG：left = 0, right = max(a) + 1.0）
  `つまり左側は必ず条件を満たすように、右側は条件最大値を１超えるように設定すると安全に探索
- `計算量から逆算し、おおよその繰り返しの目安を設定する（今回for...range(100),right = 10001）

## 問題内容
n 本のパイプがあり、長さはそれぞれ A_1, A_2, ..., A_n です。今、n 本のパイプから k 本の同じ長さのパイプを切り出すことを考えます。パイプを切って分割することはできますが、つなげることはできません。

パイプの切り方を工夫した結果、切り出すことができるパイプの長さの最大値を答えてください。

答えは整数になるとは限りません。相対誤差または絶対誤差が 10^-6 (0.000001) 以下であれば正解とみなされます。

## 自分の解答
```python
import sys
input = sys.stdin.readline
# from bisect import bisect_left

n,k = map(int,input().split())
a = list(map(int,input().split()))
a.sort() # 今回は不要

def lower_bound(a,n,k):
    left = sum(a) // k 
    right = sum(a) // k + 1
    count = 0 # ここで宣言はよくない
    
    while left < right and count != k: 
    # 実数探索の場合はwhileだと一致しない可能性が高く無限ループに陥る可能性が高いためNG
    # 整数探索 → while,実数探索 → forで回数制限
        mid = (left + right) / 2
         
        # print(left,right)
        # print(mid,count)
        for i in range(n):
            count += a[i] // mid
        
        if count < k:
            right = mid + 0.000001 #+ 0.000001は不要。
            # 整数探索だとleft = midでループが止まる可能性があるが、実数探索では必ず割り切れ,
            # 収束が保証されているため不要
        elif count > k:
            left = mid 
        count = 0 # ループの頭で宣言すればここにに書かなくてもよくなる
        
    return left
print(lower_bound(a,n,k))
```


### 改良コード（Paizaの模範解答を参考）
```python
# 改良コード
import sys
input = sys.stdin.readline

n,k = map(int,input().split())
a = list(map(int,input().split()))

def max_length(a,n,k):
    left = 0 
    right = max(a) + 1.0 # right = 10001よりも安全
    
    for _ in range(100):
        mid = (left + right) / 2
        count = 0

        for i in range(n):
            count += a[i] // mid # int(a[i] // mid)とすると明示的で堅い（動作はOK）
            
        if count < k:
            right = mid 
        elif count >= k:
            left = mid 
            
    return left
print(max_length(a,n,k))
```

## 模範解答
```python
# Paizaの模範解答（優秀）
n, k = map(int, input().split())
A = list(map(int,input().split()))

left, right = 0, 10001
for _ in range(100):
    mid = (left + right) / 2
    num_of_pipes = 0
    for a in A:
        num_of_pipes += a // mid

    if num_of_pipes < k:
        right = mid
    else:
        left = mid

print(left)
```

```python
# chatGPTの模範解答（自分とPaizaの方針とはかなり離れているためあまり参考にならない）
import sys
input = sys.stdin.readline

n, k = map(int, input().split())
a = list(map(int, input().split()))

def can(x: float) -> bool:
    # 長さ x のパイプを k 本以上作れるか
    if x == 0.0:
        return True
    cnt = 0
    for v in a:
        cnt += int(v // x)
        if cnt >= k:
            return True
    return False

ok = 0.0                      # 可能側（0は常に可能として扱う）
ng = max(a) + 1.0             # 不可能側（最大長より長いのは不可能）

for _ in range(100):          # 誤差1e-6を十分満たす反復回数
    mid = (ok + ng) / 2.0
    if can(mid):
        ok = mid
    else:
        ng = mid

print(f"{ok:.10f}")
```