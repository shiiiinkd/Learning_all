

## 学んだこと
座標圧縮、enumrate、辞書（ハッシュマップ）

座標圧縮とは　→　大きな値を小さい連番に置き換える手法
```python
for i, a_i in enumerate(sorted(a)):
    compressed[a_i] = i + 1
```
- sorted(a) で値を小さい順にソート （小さい順位を決定）
- enumerate で0,1,2,3,....という連番を付ける（i）でアクセス
- `compressed[a_i] = i + 1` でキーが配列Aの値　→　小さい順位  で登録

注意：compressedは辞書（ハッシュマップ）。配列ではない。→存在しない値はキーが存在しない。
```
#ex) a = [100, 500, 300]の場合

sorted(a) => [100, 300, 500]

compressed => {
  100: 1,  #キーで登録
  300: 2,
  500: 3
}
```

## 問題内容
横一直線に並んだ 1,000,000,000 (= 10^9 ) 個のマスがあり、左から A_1, ..., A_N 番目の N 個のマスに色を塗りました。全部で Q 回行われる以下の質問にすべて答えてください。

・左から X_i ( 1 ≦ i ≦ Q ) 番目のマスは色が塗られていることがわかりました。このマスは色が塗られているマスのうち左から何番目のマスでしょう。

![](https://paiza-learning-mondai.s3.amazonaws.com/sort_advanced/problems_speedup_step9/1.png)

## 模範解答
```python
n, q = map(int, input().split())
a = list(map(int, input().split()))
x = list(map(int, input().split()))

compressed = {}

for i, a_i in enumerate(sorted(a)): # enumerateで連番を付ける
    compressed[a_i] = i + 1

for x_i in x:
    print(compressed[x_i])
```