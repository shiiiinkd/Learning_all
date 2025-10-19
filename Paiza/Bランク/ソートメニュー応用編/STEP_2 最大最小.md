

## 学んだこと
max,min以外の最大最小
a.sortの後、max→a[n-1],min→a[0]

## 問題内容
整数 n と、数列 a_1, ... , a_n が与えられます。  
  
数列 a の最大値と最小値をそれぞれ半角スペース区切りで出力してください。

## 自分の解答
```python
n = int(input())
a = list(map(int,input().split()))
print(max(a),min(a))
```

## 模範解答
```python
n = int(input())
a = list(map(int, input().split()))

a.sort()

print(a[n - 1], a[0])
```