- 数字の文字列操作（時刻1） Python3編（paizaランク D 相当）
 -   S = input()
	h = int(S[:2]) #point
	m = int(S[3:])
	
	print(h)
	print(m)
- `XX:XX` というフォーマットから時と分を取り出します。これには文字列のスライスを使います。`S[a:b]` で S の a 文字目から (b-1) 文字目までを切り取った部分文字列が取得できます（この際、「 n 文字目」というのは 0 文字目から数えていることに注意してください）。たとえば `"paiza"[1:3]`は `ai` です。
- `S[a:]`, `S[:b]` などとすると、それぞれ、a 番目から最後まで、最初から (b-1) 番目までの部分文字列を取得できます。よって、`S[:2]` とすれば S の時の部分が、`S[3:]` とすれば S の分の部分が取り出せます。
- int関数 は 0埋め を無視して数字列を整数に変換するので、0埋め を削除するのに使えます。


- 「昇順ソート Python3編」採点結果
	n = int(input())
	a = [0] * n
	
	for i in range(n):
	    a[i] = int(input())
	
	a.sort() #point .sort()で昇順に並び替え
	     #point .sort(reverse=True)で降順ソート
	
	for i in range(n):
	    print(a[i])
	    
-  「辞書式ソート Python3編」
	正整数 n が与えられ、数のペアが n 個与えられます。各ペアの最初の数はりんごの個数を、その次の数はバナナの個数を表しています。これらの数のペアを以下の規則に従って、偉い順に並び替えてください。  
  
1. ふたつのペアのりんごの数が異なる場合、りんごの数が多い方が偉い（この際、バナナの数は関係ない）。  
2. りんごの数が同じである場合、バナナの数が多い方が偉い。
	 n = int(input())
	ab = [0]*n
	
	for i in range(n):
	    a,b = input().split()　　#point lineで一括管理ではなくaとbに分けて要素ごとで管理
	    a = int(a)
	    b = int(b)
	    ab[i] = [a,b]
	    
	ab.sort(reverse=True)  #point すべての要素について一度にソートできる
	
	for i in range(n):
	    [a,b]=ab[i]
	    print(a,b)
　　　#point sort(reverse=True)では左側の要素から降順ソート、もし左側要素の値が同じなら右の要素で降順ソート（つまりどの列でもすべて降順ソートになっている）
　　　
　・もし左要素は降順ソート、右側は昇順ソートをしたくなったら
	n = int(input())
	ab = [None] * n
	
	for i in range(n):
	    a, b = map(int, input().split())
	    ab[i] = [a, b]
	
	　#aを降順、同じならbを昇順
	　
	ab.sort(key=lambda x: (-x[0], x[1])) # point 
	
	for a, b in ab:
	    print(a, b)
 - mapの書き方(int型で入力を受け取る)
 　a = list(map(int,input().split())) #point list()の中でmapを宣言する
 
 - ループの抜け方
	1 から n まで番号が付けられた人々がいます。 i 番目の人の財産は a_i 円です。金額 k が与えられるので（k は a_1, ..., a_n のいずれか）、財産が k 円である人の番号を出力してください。ただし、そのような人が複数いる場合には、そうした人々の中で最も小さい番号を出力してください。
	
	n = int(input())
	a = [0]*n
	for i in range(n):
	    a[i] = input()
	k = input()
	for i in range(n):
	    if a[i] == k:
	        print(i+1)
	        break
	        
    例えばこのコードはfor文の中にあるif文の中でbreakが宣言されているが、これで問題なく外側のforループを抜けることができる。
    breakを宣言すると一番内側のループのみ抜けることができる

　外側のループまで一度に抜けたい場合は①フラグを立てる、②returnで関数を返す の二つの方法がある。
	①フラグを立てる
	found = False
	for i in range(3):
	    for j in range(3):
	        if j == 1:
	            found = True
	            break
	    if found:
	    　break
	②returnで返す
	def search():
    for i in range(3):
        for j in range(3):
            if j == 1:
                return (i, j)  # 外側ごと終了
	print(search())
	
　  #point ちなみに if a[i] == K and index == 0:でも行けた
- 辞書
  n 人の人に関して、それぞれの人の名前と財産が与えられます。その後に人名 S が与えられるので （S は最初に与えられた名前のうちのいずれか） 、 S の財産を表す整数を出力してください。

	入力される値
	
	入力は以下のフォーマットで与えられます。  
	
	n  
	s_1 a_1  
	...  
	s_n a_n  
	S  
	
	  
	1 行目には正整数nが与えられ、 2 行目から (n + 1) 行目には、人々の名前と財産が “s_i a_i” というフォーマット （s_i は人の名前を表す文字列、 a_i はその人の財産を表す整数、半角スペース区切り）で与えられます。 (n + 2) 行目には人名 S が与えられます (S は 2 行目から (n + 1) 行目にかけて与えられた人名のいずれか）。
	
	n = int(input())
	zaisan = {} #point 辞書を初期化
	
	for i in range(n):
	    [s, a] = input().split()
	    zaisan[s] = a #point zaisan[s] = a でzaisan に s に対応する値 a を追加する
	
	S = input()
	
	print(zaisan[S]) #point zaisan[S]でzaisanにおける　S に対応する値にアクセスする

- 辞書データのソート
	n 人の人の名前 s_1, ..., s_n が与えられたのち、 m 回の「攻撃」に関する情報が与えられます。各行は “p_i a_i” というフォーマットで与えられ、 p_i はダメージを受けた人の名前 （s_1, ..., s_n のいずれか） 、 a_i は p_i が受けたダメージ数を表す数です。なお、一度もダメージを受けていない人の合計ダメージは 0 とします。
	
	それぞれの人が受けた合計ダメージを、人の名前のアルファベットの辞書順に出力してください。
	
	入力される値
	入力は以下のフォーマットで与えられます。
	
	n
	s_1
	...
	s_n
	m
	p_1 a_1
	...
	p_m a_m
	
	1 行目には正整数 n が与えられ、 2 行目から (n + 1) 行目には人の名前 s_1, ..., s_n が改行区切りで与えられます。 (n + 2) 行目には正整数 m が与えられ、 (n + 3) 行目から (n + m + 2) 行目には人の名前 p_i （s_1, ..., s_n のいずれか） とその人が受けたダメージ a_i が "p_i a_i" という半角スペース区切りのフォーマットで m 行与えられます。
	
	入力値最終行の末尾に改行が１つ入ります。
	文字列は標準入力から渡されます。 標準入力からの値取得方法はこちらをご確認ください
	期待する出力
	それぞれの人が受けたダメージを、人の名前のアルファベットの辞書順に n 行出力してください（出力するのはダメージだけです）。
	末尾に改行を入れ、余計な文字、空行を含んではいけません。
	
	n = int(input())
	dmg = {}
	
	for i in range(n):
	    s = input()
	    dmg[s] = 0
	
	m = int(input())
	
	for i in range(m):
	    [p, a] = input().split()
	    a = int(a)
	    dmg[p] += a
	
	names = list(dmg.keys()) 
	#point keys は辞書のメソッドで、辞書のキー（今回だと人名）を取り出す
	#point dmg.keys()でdmgのキーを取り出し、listでリストnamesを作ることができる。
	　
	names.sort()

  #point name in namesで直接dmg[name]で呼び出せる
	for name in names:
	    print(dmg[name])
	    
　 #point こう書くこともできる(keyを配列でinputして、その配列を直接ソートする)
	    n = int(input())
		S = {}
		s = [0]*n
		for i in range(n):
		    s[i] = input()
		    S[s[i]]=0
		m = int(input())
		for i in range(m):
		    p,a = input().split()
		    a = int(a)
		    S[p] += a
		s.sort() 
		#point keyであるsを事前にソートして出力する方針
		
		# for i in range(n):
		#     print(S[s[i]])
		for name in s:
		    print(S[name])
		    
		    
- p 人のグループ A , q 人のグループ B , r 人のグループ C があります。各グループのメンバーにはそれぞれ番号がつけられており、 A グループの i 番目の人は B グループの j 番目の人に仕事を任せ、 B グループの j 番目の人は与えられた仕事を C グループの k 番目の人に任せます。すると結局、 A グループの i 番目の人の仕事をするのは C グループの k 番目の人だということになります。

	パイザ君は A グループの各人の仕事を結局 C グループの誰が行うことになるのか知りたがっています。 A グループの人のそれぞれが最終的に C グループの誰に仕事を頼むことになるのかを、 A グループの人の番号が小さい順に p 行出力してください。
	
	入力される値
	入力は以下のフォーマットで与えられます。
	
	p q r
	i_1 j_1
	...
	i_p j_p
	j'_1 k_1
	...
	j'_q k_q
	
	1 行目には A グループ、 B グループ、 C グループのそれぞれの人数 p , q , r が半角スペース区切りで与えられます。
	2 行目から (p + 1) 行目までは A グループの人の番号とその人が仕事を頼む B グループの人の番号 i_a, j_a （1 ≤ a ≤ p） が半角スペース区切りで、 (p + 2) 行目から (p + q + 2) 行目までは B グループの人の番号とその人が仕事を頼む C グループの人の番号 j’_b , k_b （1 ≤ b ≤ q） が半角スペース区切りで与えられます。
	
	期待する出力
	A グループの i_c 番目の人が C グループの k_c 番目の人に仕事を頼むとしたとき （1 ≤ c ≤ p） 、各 i_c, k_c をそれぞれ半角スペース区切りで、 i_c が小さい順に p 行出力してください。
	末尾に改行を入れ、余計な文字、空行を含んではいけません。
	
	
	[p, q, r] = [int(i) for i in input().split()]
	AB = {}
	BC = {}
	for _ in range(p):
	    [i, j] = [int(n) for n in input().split()]
	    AB[i] = j
	for _ in range(q):
	    [j, k] = [int(n) for n in input().split()]
	    BC[j] = k
	
	AC = {}
	
	for i in range(1, p + 1): #point ここはpではなく、１から始まるキーに着目してforループしている
	    AC[i] = BC[AB[i]]　配列のインデックスではなくて辞書のキーを参照していることに注意
	    
	    #point この時ACには挿入順が保持されているため、下の.itemsで参照するときにソートは不要
	for i, k in AC.items():
	    print(i, k)
	    
	    
	    
	#point AC.itemsでACの中身を参照して、それをi,kとしてforで出力する
	
	#point 下のようにも書ける（ACの辞書を作成せずに直接出力する）
	p,q,r = map(int,input().split())
	AB = {}
	BC = {}
	for i in range(p):
	    a,b = map(int,input().split())
	    AB[a] = b
	
	for j in range(q):
	    b,c = map(int,input().split())
	    BC[b] = c
	
	numbers = list(AB.keys())
	numbers.sort()
	for number in numbers:
	    print(number,BC[AB[number]])
	
- while文
  n = 10000
	while True:  #point while True:とすると、breakで脱出の指示があるまでループを続ける
	    if n % 13 == 0:
	        break  #point break文でループを抜ける
	    n += 1
	print(n)
	
- while＋漸化式問題
  カウンター魔法を得意とするパイザ君は、同じくカウンター魔法を使うモンスターと戦っています。バトルはターン制で、パイザ君が先攻で、パイザ君とモンスターで交互に魔法を使い合います。パイザ君の魔法は 1 回目と 2 回目に使うときにはダメージ 1 ですが、 3 回目以降の n 回目には、(モンスターから受けた (n - 1) 回目の攻撃のダメージ) + (モンスターから受けた (n - 2) 回目の攻撃のダメージ) のダメージを与えます。モンスターの魔法はこれよりも強力で、 1 回目と 2 回目には同じくダメージ 1 ですが、 3 回目以降の n 回目には、 (パイザ君から受けた (n - 1) 回目の攻撃のダメージ) * 2 + (パイザ君から受けた (n - 2) 回目の攻撃のダメージ) のダメージを与えます。
  パイザ君は自分がどれくらいモンスターの攻撃を耐えられるか知りたいと思っています。パイザ君の体力を H として、両者が同じ魔法を使い続けたとき、モンスターの何回目の攻撃でパイザ君の体力が 0 以下になるかを出力してください。
  
  自分の解答
　　H = int(input())
　　paiza_attack = [0]*100
	monster_attack = [0]*100
	fulldamage = 0
	turn = 0
	while fulldamage<H:
	    if turn<2:
	        turn+=1
	        paiza_attack[turn]=1
	        monster_attack[turn]=1
	        fulldamage+=monster_attack[turn]
	        
	    else:
	        turn+=1
	        paiza_attack[turn]=monster_attack[turn-1]+monster_attack[turn-2]
	        monster_attack[turn] = paiza_attack[turn-1]*2 + paiza_attack[turn-2]
	        fulldamage+=monster_attack[turn]
	print(turn)
	
	
	H = int(input())
	a = [0, 1, 1] #point 順にn-2,n-1,n回目の攻撃
	b = [0, 1, 1]  
	
	dmg = 2　　#point 二回目まではダメージ固定→固定部分は計算してしまってコードを簡略化
	
	i = 2　#point 二回目までは固定
	
	while dmg < H:
	    a[0] = a[1] #point 漸化式問題は初めに配列を準備して順に代入を繰り返すように解く
	    a[1] = a[2]
	    b[0] = b[1]
	    b[1] = b[2]
	
	    a[2] = b[0] + b[1]
	    b[2] = a[0] + 2 * a[1]
	
	    dmg += b[2]
	
	    i += 1
	
	print(i)