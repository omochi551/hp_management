Title:ベイズ流T検定 BEST
Date: 2019.04.14
Category: statistics
Tags: statistics
Slug: bayesian_T_test
Author: 安水
Summary:ベイズ流T検定 BEST

ここ最近pymcを使ったベイズ推論のことをずっと考えています。
pymc3を扱った本(http://amzn.asia/1TWcfTI)が先週発売されて買ってしまったのですが、
まだ前のpymc本(http://amzn.asia/8CPISDp)を読み切っていなかったので急いで読み切りました。
読み切った記念に一個面白そうなものがあったのでまとめました。

2群の平均値に差があるかどうか比べたいというありがちな問いに対しては一般にt検定が使われます。
当分散性が言えるとき（2郡の分散が同じである確信が持てるとき）はStudent's t-testを使います。
分散については立山さんのノートを参考にどうぞ。
当分散性が言えないときは（自信がないときも保守的に）Welch's t-testを使います。
余談ですが、どちらのt-testも平均値が正規分布に従うことを仮定しているので、
その仮定が怪しいときはノンパラメトリックな検定を選びます。
まあこのへんは誰かがコード付きでまとめてくれると信じてます。

このt検定ですが、ベイズ風のアレンジの論文が存在するようです。
BEST(Bayesian estimation supersedes the t-test)
というかっこいい名前です。
2群それぞれを独立にt分布に従うと仮定し、それぞれ3つのパラメーター（平均、分散、外れ値）
を推論します。つまり、6つのパラメーターを推論します。
ベイズ推論に落とし込むことで、2群それぞれの平均、分散、外れ値の解釈が容易になります。
ベイズ推論とか統計モデリングってこんなんなんやっていうのもなんとなくわかると思うので、
とりあえず下のnotebookを開いてみてください。

ipynbはこちら
↓↓↓↓↓
http://nbviewer.jupyter.org/gist/yyoshiaki/255d392ae32d258cfdf19cfad855b8fb
余談に余談を重ねますが、
ipynbの公開方法はhtmlやpdfにexportしたり、いろいろありますが、
少し凝った方法で公開してみました。
githubのgistという機能を用いて、公開し、それをnbviewerに渡してみました。
スマホでもみれていいですね。
[参考HP](http://kasoutuuka.org/jupyter-notebook)
