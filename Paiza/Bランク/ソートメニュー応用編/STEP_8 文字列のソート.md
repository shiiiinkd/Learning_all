

## 学んだこと
文字列の長さによるソート、条件の追加

## 問題内容
文字列が n 個与えられます。以下の条件を満たすように並び替えてください。  
  
1. 各文字列の文字数が昇順になるようにする。  
2. 文字数が等しい複数の文字列の中では、辞書順になるようにする。
## 自分の解答
```python
n = int(input())
s = [input() for _ in range(n)] 
# s = [input().split() for _ in range(n)]だとすべて長さが１になってしまう。split不要
    
s.sort()
s.sort(key=len)

for x in s:
    print(x)
```

## 模範解答
```python
# タプルを用いて比較条件を指定
n = int(input())
s = [input() for _ in range(n)]

s.sort(key=lambda s_i: (len(s_i), s_i))
#ここもタプル。(a,b,c,...)で優先順位をa,b,c,...で渡せる
#今回len(x)→x、つまり文字列の長さ→辞書順でソートすることをlambdaを使って指定している


for s_i in s:
    print(s_i)
```