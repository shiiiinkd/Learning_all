

## 学んだこと
- `import sys で高速に入力を受け取ることが出来るようになる。
- `split(),rstrip()の仕様
- `import sys を使ったときは split()がなければ rstrip()をつける

```python
import sys
input = sys.stdin.readline #ここでrstrip()は基本的にはつけられない。

n = int(input().rstrip()) # 改行文字削除のためにrstrip()必須
a, b = map(int, input().split()) # split()があるためrstrip()不要
```

## 注意点：改行文字について
- `sys.stdin.readline では末尾に改行文字が残るため、場合によっては削除しなければいけない。
- `rstrip() を使うことで末尾にある改行文字を削除することが出来る
- `split() は空白を削除するだけでなく、改行文字も削除する（rstrip()をその意味で包括している）
- `最悪迷ったらrstrip()を全部につけてしまっても大丈夫

### まとめ
- `つまり import sys を使ったときは split()がなければ rstrip()をつける！だけでOK