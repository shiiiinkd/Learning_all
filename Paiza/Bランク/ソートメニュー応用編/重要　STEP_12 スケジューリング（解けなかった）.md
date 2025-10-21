# 注意　まだまとめていない！

## 学んだこと
区間スケジューリング

## 問題内容
paiza スキルチェックでは年に何度かキャンペーンを開催しています。各回ではキャンペーン問題が提供され、その問題を解くと抽選で商品がもらえます。また、キャンペーンは n 回開催され、 i 回目のキャンペーンは paiza サービス開始日から数えて、 l_i 日目から r_i 日目の間(l_i 日目、 r_i 日目を含む)に開催される予定です。  
  
多くの商品がほしい京子ちゃんはできるだけ多くのキャンペーンに参加したいと思っています。しかし、京子ちゃんにとってキャンペーン問題は非常に難しく、開催期間中はずっとその問題に取りかかるため、 2 つの問題を同時に考えることはできません。このとき、京子ちゃんは最大でいくつのキャンペーンに参加できますか？  
  
たとえば、 n = 3, l = [ 1, 4, 7 ], r = [ 4, 7, 10 ]の場合、以下の画像のようにキャンペーンが開催されています。  
  
![](https://paiza-learning-mondai.s3.amazonaws.com/sort_advanced/problems_speedup_step6/1.png)  
  
このときは最大でキャンペーン 1 とキャンペーン 3 の 2 つに参加できます。別のサンプルも見てみましょう。 n = 3, l = [ 1, 3, 6 ], r = [ 8, 5, 9 ] の場合も 2 つのキャンペーン (キャンペーン 2 とキャンペーン 3) に参加できます。  
  
![](https://paiza-learning-mondai.s3.amazonaws.com/sort_advanced/problems_speedup_step6/2.png)

[▼　下記解答欄にコードを記入してみよう](https://paiza.jp/works/mondai/sort_advanced/sort_advanced__problems_speedup_step6/edit?language_uid=python3&t=4351fe0b4b4d37e643336dc9d33ea777#codeArea)

入力される値

n  
l_1 r_1  
l_2 r_2  
...  
l_n r_n

  
  
・ 1 行目に、数値 n が与えられます。  
・ 2 行目から n + 1 行目にかけて数値 l_i と r_i が与えられます。

  
入力値最終行の末尾に改行が１つ入ります。  
文字列は標準入力から渡されます。 [標準入力からの値取得方法はこちらをご確認ください](https://paiza.jp/guide/samplecode.html)

期待する出力

京子ちゃんが参加できる最大のキャンペーンの個数を答えてください。  
  
また、末尾に改行を入れ、余計な文字、空行を含んではいけません。

条件

すべてのテストケースにおいて、以下の条件をみたします。  
  
・ 1 ≦ n ≦ 100,000  
・ 1 ≦ l_i ≦ r_i ≦ 200,000

## 自分の解答（解けなかった）
```python
#l-rで開催期間を出し、この期間が短い順にソートしようとしていたが、失敗
n = int(input())
s = [0]*n
for i in range(n):
    s[i] = list(map(int,input().split()))
l = [0]*n 
r = [0]*n 
x = [0]*n
for i in range(n):
    l[i],r[i] = s[i]
    x[i] = r[i] - l[i]
   
    
print(x)

print(s)
```

## 模範解答
```python
n = int(input())

campaign = []
for i in range(n):
    l, r = map(int, input().split())
    campaign.append([l, r])

campaign.sort(key=lambda x: x[1])

participated_campaigns = 0
campain_lastday = 0
for i in range(n):
    if campain_lastday < campaign[i][0]:
        participated_campaigns += 1
        campain_lastday = campaign[i][1]

print(participated_campaigns)
```