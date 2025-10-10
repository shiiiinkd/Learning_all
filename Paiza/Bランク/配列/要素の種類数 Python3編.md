

## 学んだこと
リスト内包表記とセット内包表記、種類を管理する配列の準備

## 問題内容
配列 A の要素数 N と配列 A の各要素 A_1, A_2, ..., A_N が与えられるので、配列 A には何種類の値が含まれているかを求めてください。

## 自分の解答
```python
n = int(input())
a = [""]*n
b = [""]*n
count=0
for i in range(n):
    a[i] = int(input())
    if a[i] not in b:
        count+=1
    b[i] = a[i]
print(count)
```

## 模範解答
```python
#1 入力の存在の有無を管理する配列を準（存在しない→0　存在する→1と定義）
n = int(input())
numbers = [0] * 101
ans = 0

for _ in range(n):
    a = int(input())
    #入力された値 a をインデックスとして使う
    if numbers[a] == 0:
        ans += 1
        #更新
        numbers[a] = 1

print(ans)

#2
n = int(input())
a = set()#set()は重複を自動でなくしてくれるメソッドで集合を定義

for _ in range(n):
    a_i = int(input())
    if a_i not in a:
        a.add(a_i)
#aにa_iを追加するaddメソッド（実はこれも重複を自動で無視してくれるからifなしでも動作する。なぜならset.add()だから）

print(len(a))

#3 ChatGPT
n = int(input())
a = {int(input()) for _ in range(n)} #{}:セット内包表記
print(len(a))

```
a = {int(input()) for _ in range(n)} #{}：セット内包表記
a = [int(input()) for _ in range(n)] #[]：リスト内包表記

セット内包表記は重複を自動で削除して追加してくれる。
リスト内包表記は重複があってもそのまま追加される。

```python
#セット内包表記
a = set()
for _ in range(n):
    x = int(input())
    a.add(x) #point

#リスト内包表記
a = []
for _ in range(n):
    x = int(input())
    a.append(x) #point
```