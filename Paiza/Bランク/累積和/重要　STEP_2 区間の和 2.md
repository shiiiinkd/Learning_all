

## 学んだこと
区間和のとり方のルール

区間和の書き方
`区間 [l, r] の合計
`[l] 〜 a[r]（閉区間）の和は → S[r+1] - S[l]
```python
n = len(A)
S = [0] * (n + 1)

#i,i-1を参照すること
for i in range(1, n + 1):
    S[i] = S[i-1] + A[i-1]  # Aは0-indexでもOK（ここだけ注意）
　　
# 区間 [l, r] の合計
# a[l] 〜 a[r]（閉区間）の和は → S[r+1] - S[l]
```



## 自分の解答
```python
# 誤り。模範解答の累積和の書き方を採用すべし。
a = list(map(int,input().split()))
s = [0]*len(a) # len(a)+1
for i in range(1,len(a)): # len(a)+1にする
    s[i] = s[i-1] + a[i] #ここをa[i-1]にしなければいけない
print(s[7]-s[1])
```

## 模範解答
```python
#あまりよくない。i,i-1を参照するというルールを徹底する
a = [int(x) for x in input().split()]
s = [0] * 11

for i in range(10):
    s[i + 1] = s[i] + a[i]

print(s[8] - s[2])
```