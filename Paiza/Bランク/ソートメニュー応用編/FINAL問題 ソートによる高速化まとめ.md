

## 学んだこと
a.sort() と sorted(a)の違い、破壊的かどうか
a.sort() → 破壊的ソート
sorted(a) → 一時的なソート（元の配列はソートされない）
## 問題内容
N 要素の数列 A が与えられます。次の 2 つの操作をおこなうプログラムを作成してください。  
  
・ update(k, x): 列の先頭から k 番目の値を x に変更する。  
・ get(k): 数列 A の中から大きい順で k 番目の値を出力する。

## 自分の解答
```python
n,q = map(int,input().split())
a = list(map(int,input().split()))
query = [input().split() for i in range(q)]

for i in range(q):
    if query[i][0] == "get":
        b = sorted(a,reverse = True)
        ix = int(query[i][1])
        print(b[ix-1])

    elif query[i][0] == "update":
        ix = int(query[i][1])
        a[ix-1] = int(query[i][2])
```

## 模範解答
```python
n, q = map(int, input().split())
a = list(map(int, input().split()))

for i in range(q):
    query = input().split()
    if query[0] == "update":
        k, x = map(int, query[1:])
        a[k - 1] = x
    elif query[0] == "get":
        k = int(query[1])
        print(sorted(a, reverse=True)[k - 1])
```