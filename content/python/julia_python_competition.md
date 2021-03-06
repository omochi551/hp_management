Title:JuliaとPythonと競技プログラミング
Date: 2019.04.14
Category: python
Tags: python
Slug: julia_python_competition
Author: 小川
Summary:JuliaとPythonと競技プログラミング

最近友人と話していて<a href="https://julialang.org">julia</a>が話題になったことがあったので、少しだけ調べて試して
みた話。

<strong>Juliaってなに?</strong>

Pythonのような動的型付けのスクリプト言語です。実行時にコンパイルを行いC言語にも迫る実行速度、科学技術系の数値計算もどんと来い、という触れ込みで、人気上昇中らしいです。Pythonを含む他言語のライブラリを読み込む仕組みを備えているのもすごいところ。
<del>ただ、コードの見た目が激しくMatlab風味で思わず目を背けたくなります。</del>

<strong>AtCoderでのJulia</strong>

ご多分に漏れず、実行速度に惹かれました。半年ほど前から参加している競技プログラミングサイト<a href="https://atcoder.jp" target="_blank" rel="noopener noreferrer">AtCoder</a> で、常用しているPython(← Python会だからね!)で実行時間切れ、C/C++に
書き換えると正答、という経験を何度かしてきたので。
そういうわけで、ここでは最近の第121回 <a href="https://atcoder.jp/contests/abc121/" target="_blank" rel="noopener noreferrer">AtCoder Beginner Contest (ABC121)</a>
の問題で、Juliaのパフォーマンスを実際に見てみます。
(言語知識0から数十分調べて書いたコードのため、動きはするが思わぬところで非効率、ということはあるかもしれません。)

<strong>AtCoder Beginner Contest 121 問題A "White Cells"</strong>

(問題は<a href="https://atcoder.jp/contests/abc121/tasks/abc121_a" target="_blank" rel="noopener noreferrer">こちら</a>)
入力値4個を読み込んで簡単な演算結果を返すだけの問題です。

<pre><code># ABC121-A "White Cells" in Julia
inpl() = map(parse,split(readline()))
(H,W) = inpl()
(h,w) = inpl()
println((H-h)*(W-w))</code></pre>

所要時間が入力にほぼ依存しない問題ですが、、各言語でのAtCoder上実行結果。

<table>
<tbody>
<tr>
<td>言語</td>
<td>実行時間</td>
<td>消費メモリ</td>
</tr>
<tr>
<td><strong>Julia</strong></td>
<td><strong>360ms</strong></td>
<td><strong>110MB</strong></td>
</tr>
<tr>
<td>PyPy3</td>
<td>180ms</td>
<td>40MB</td>
</tr>
<tr>
<td>Python3</td>
<td>17ms</td>
<td>3MB</td>
</tr>
<tr>
<td>C++</td>
<td>1ms</td>
<td>256kB</td>
</tr>
</tbody>
</table>

C++にもPythonにも、実行時間と消費メモリ双方で惨敗。
おそらくですが、<strong>実行ごとにまずコンパイルを行う</strong>ので、簡単な問題だとそれが相対的に巨大なオーバーヘッドになってしまうようです。
Pythonの半コンパイラ型実装であるPyPyはJuliaの半分程度でした。

<strong>AtCoder Beginner Contest 121 問題C "Energy Drink Collector"</strong>

(問題は<a href="https://atcoder.jp/contests/abc121/tasks/abc121_c" target="_blank" rel="noopener noreferrer">こちら</a>)

読み込んだ値の列をソートして、条件判定をしながら順番に足し上げていく問題。

<pre><code># ABC121-C "Energy Drink Collector" in Julia
inpl() = map(parse,split(readline()))
(N,M) = inpl()
A = Array{Int}(N,2)
for i in 1:N
  A[i,:] = inpl()
end
A = sortrows(A, by=x-&gt;x[1])
ans = 0
for i in 1:N
  if A[i,2] &gt;= M
    ans += M*A[i,1]
    break
  else
    M -= A[i,2]
    ans += A[i,1]*A[i,2]
  end
end
println(ans) </code></pre>

なんと、テスト16個中15個でタイムアウト(2000ms以上)。。。
Pythonのコードはこちら:

<pre><code> # ABC121-C "Energy Drink Collector" in Python3
inpl = lambda: list(map(int,input().split()))
N,M = inpl()
A = []
for i in range(N):
  A.append(inpl())
A.sort(key=lambda x: x[0])
ans = 0
for i in range(N):
  if A[i][1] &gt;= M:
    ans += A[i][0]*M
    break
  else:
    M -= A[i][1]
    ans += A[i][0]*A[i][1]
print(ans) </code></pre>

こちらは最大466msでクリア(同一コードのPyPy3では733ms)。ここで134msのテストもJuliaではタイムアウト。悲しい。
今回Juliaでタイムアウトになったのは、言語の特性や正しいコーディングの仕方を知らないから、という可能性は高いです。ただ実際にこの問題でJuliaを使って提出されている答案は、最速クリアのものでも1724ms(そもそもJuliaでの提出数自体が少ないですが)。やはり上の安直なPythonコードが圧勝しています。

<strong>Juliaは競技プログラミングに向かない?</strong>

Juliaの実行速度が速いこと自体は(今回検証していませんが、きっと)本当なんだと思います。しかしそれは時間のかかる複雑・大規模な処理の場合であって、競技プログラミングのような高々2-3秒の計算にはコンパイルのオーバーヘッドがやはり大きいのかな、という印象です。
AtCoderなどでは、C++などのあからさまなコンパイル型言語はコンパイル時間が実行時間に算入されず、一方でJuliaに対しては算入されます。やや理不尽な感じはしなくもないけれど、このルール下でJuliaの高速性能を生かすことは(あくまでAtCoderのような短時間型競技プログラミングの話ですが)なかなか難しそう。残念ながら、普通にやるとPythonよりもずっと遅い。
なので、当面の競技プログラミング用言語はやっぱりPython(とC/C++)、と個人的には結論づけたところです。おしまい。
