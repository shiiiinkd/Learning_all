

## 学んだこと
keyを使用した任意の列に注目したソート、lambda、タプル

## 問題内容
整数 n, m, k と n 行 m 列の表 a が与えられます。以下の条件をすべて満たすように、 a を行単位でソートしてください。  
  
・ a の k 列目が昇順になっている  
・ a の k 列目の値が等しい 2 つの行では、 a の 1 列目の値が昇順になっている  
・ a の k 列目 と a の 1 列目から i 列目までのすべての値が等しい 2 つの行では、 a の i + 1 列目の値が昇順になっている ( 1 ≦ i ≦ m - 1 )


## 模範解答
```python
#ChatGPTの模範解答（key,lambda,tuple)
n, m, k = map(int, input().split())
k -= 1

a = []
for _ in range(n):
    row = list(map(int, input().split()))
    a.append(row)
    
a.sort(key=lambda x:(x[k],x[:k],x[k + 1:])) #(a,b,c,...)がタプル
#注　a.sort(key=lambda x:(x[k],*x[:k],*x[k + 1:])) #現時点ではとりあえず*つけておけばOK

#a.sort(key=lambda x: tuple([x[k]] + x[:k] + x[k + 1:]))でもOK
#[x[k]]で後ろのlist型に合わせていることに注意

for row in a:
    print(*row)
```

## 解説
## 1. Pythonのソートの基本原理

- Pythonの`sort()`や`sorted()`は、**キーの辞書順（lexicographical order）で比較する。  
    → キーに「**比較したい列の値を、優先順位の順に並べたもの**」を渡せばよい。  
    → 今回は「**k列目 → 1列目 → 2列目 → ...（k-1列目）→（k+1列目以降）**」の順に比較する。
    
- 行`x`から`([x[k]] + x[:k] + x[k+1:])`という「比較用の並び」を作り、キーにする。
    
```python
# ex) keyにlenを指定 → 文字列の長さ順に並び替え
a = ["apple", "banana", "cherry"] 
a.sort(key=len)
```

---

## 2. `lambda`とは

- `lambda x:` は**その場で関数を作る無名関数**。短い処理を使い捨てで書ける。
    

`# 普通の関数定義 def func(x):     return x + 1 # 上を1行に省略した形 lambda x: x + 1`

- 注意点
    - `lambda`は**式**なので`if`文や複数行の処理は書けない。
    - 常に「右側の式の値を返す」。
---

## 3. タプル（tuple）

- `(a, b, c, …)`のように要素を**カンマ（,）で区切って丸括弧で囲う**。
- 特徴
    - **イミュータブル（不変）**：作成後に変更できない。
    - **ソートキーの定石**：辞書順で比較されるため**多重比較を自然に書ける**。変更不可で**安全・軽量**。

`key = lambda x: (x[k], *x[:k], *x[k+1:])`
*があるとリストの中身が展開される。現時点ではとりあえずつけておけば大丈夫

→ 「k列目を主キー、その後を従キーとして比較する」という意図が一目でわかる。


#### その他の解答(あまり参考にならない)
```python
#1 key,lambdaを使用したソート
n, m, k = map(int, input().split())
k -= 1

a = []
for i in range(n):
    row = list(map(int, input().split()))
    a.append(row)

a.sort(key=lambda x: [x[k]] + x[:k] + x[k + 1 :])

for i in range(n):
    print(*a[i])

#2 スライス構文を使用したソート
n, m, k = map(int, input().split())
k -= 1

a = []
for i in range(n):
    row = list(map(int, input().split()))
    row = [row[k]] + row[:k] + row[k + 1 :]
    a.append(row)

a.sort()

for i in range(n):
    row = a[i][1 : k + 1] + [a[i][0]] + a[i][k + 1 :]
    print(*row)
```

## 自分の解答（失敗）
```python
#失敗
n,m,k = map(int,input().split())
a = [0]*n
lst = []
for i in range(n):
    a[i] = list(map(int,input().split()))

for j in range(m):
    if j != k-1:
       lst.append(str(j))
t = tuple(lst)
a.sort(key=lambda x: (x[t]))
for x in a:
    print(*x)
```
