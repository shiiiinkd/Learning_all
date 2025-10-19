

## 学んだこと
set関数とsetを使わない重複のない配列の準備

## 問題内容
整数 n と、数列 a_1, ... , a_n が与えられます。  
  
数列 a から重複した要素をすべて削除し、残った要素を昇順かつ半角スペース区切りで出力してください。


## 模範解答
```python
#setを使わない解法
n = int(input())
a = list(map(int,input().split()))
a.sort()
unique = []
for i in range(n):
    if i == 0 or a[i] != a[i-1]: #基本的に連続した配列を比較するときはi-1を参照するのがいい
        
        unique.append(a[i])

print(*unique)

#setを用いた解法
n = int(input())
a = list(map(int, input().split()))

a.sort()

unique = set(a) # a = set(a)

print(*unique)
```