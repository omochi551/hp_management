Title:組み込みでDeep Learningにつかえるハードについて
Date: 2019.04.14
Category: deeplearning
Tags: deeplearning
Slug: hardware_for_deeplearning
Author: 安水
Summary:組み込みでDeep Learningにつかえるハードについて

<h1>組み込みでDeep Learningにつかえるハードについて</h1>
2018/08/01　リレー投稿再掲　安水良明
<h2>Rasberry pi</h2>

<hr />

シングルボードコンピュータ。手のひらサイズで値段も５０００円とリーズナブルだが一人前のコンピューター。Linuxの練習にもうってつけ。クアッドコアだが機械学習としてはすこし非力。GPUもつかえない。電池で動く。何台もつなげてクラスター化する強者も。
<ul>
 	<li><a href="http://www.cenav.org/raspi2/">計算工学ナビ : RaspberryPiでスパコンを作ろう</a></li>
 	<li><a href="https://qiita.com/kazunori279/items/bb58f0b3095f3c65b2a1">Qiita : RasPiとディープラーニングで我が家のトイレ問題を解決する</a></li>
</ul>
<h2>スマホ</h2>

<hr />

やはり今の時代にハードとしてスマホに注目しないわけにはいかない。Tensorflowならスマホ組み込みも。まだ開発版のみだが、アンドロイドもiosもどちらも遊べるらしい。
<ul>
 	<li><a href="https://www.sejuku.net/blog/55188">侍エンジニア塾 : 【TensorFlow】スマホで動かせるLiteとは？</a></li>
</ul>
<h2>GPU</h2>

<hr />

おなじみ。Deep Learning等は大量の行列演算を必要とする。GPUはもともとグラフィックスにフォーカスして作られていた演算回路だが、グラフィックス自体大量の行列演算だったため、Deep Learningに転用することで超高速な学習が可能になった。Deep learningやるなら必需品。ただ、これ自体を持ち出すのは困難。市販最速のNVIDIA GTX 1080 tiで１０万円くらい。
<h2>FPGA</h2>

<hr />

Field Programmable Gate Arrayの略。デジタル回路を自分で設計できる集積回路。集積回路といえば単一タスクを低電力低コストで高速な演算が可能だが、専門家しか作れなかったし、そもそも作ること自体が大変だった。FPGAは集積回路の設計をソフトで行うことで、柔軟に専門設計が可能になった。ちっちゃいので組み込みにも向いている。最近Scienceにのって話題になったGohst CytometryもFPGA使ってるそうな。（阪大、東大、理研AIPのコラボ。下で書くjetson化も視野に入れているらしい。）最近では各社がFPGAに取り組みだしている。Tensorflowも動かせるらしい。ただしやはり専門外ではとっつきにくい。ピンキリだがやすいので１万５千円くらい。論理回路設計がもとめられるのでぶっちゃけよくわからん。
<ul>
 	<li><a href="https://qiita.com/kazunori279/items/a9e97a4463cab7dda8b9">Qiita : そろそろプログラマーもFPGAを触ってみよう！</a></li>
 	<li><a href="http://science.sciencemag.org/content/360/6394/1246.full">Science : Gohst Cytometry</a></li>
</ul>
<h2>jetson</h2>

<hr />

NVIDIA組み込みモジュール。安価かつ高速でポータブルなGPUが使える。NVIDIA製ということで、Tensorflowも使えるのが嬉しい。値段は開発キットが599ドル（1ドル＝114円換算で、6万8286円）で、製品に組み込んで出荷可能なProduction Moduleは1000個ロット時で399ドル（同、4万5486円）。256 CUDAコア（GTX 1080 tiで3584 cuda cores）なので、やはり学習済みモデルの運用がメインと思われる。
<ul>
 	<li><a href="https://qiita.com/ababa893/items/57b43e788d684c380866">Qiita : NVIDIA Jetson TX2でTensorFlowによる人体姿勢推定プログラムを動かせるようになるまで</a></li>
</ul>
ディープラーニングに限らず、なにか作ったよとか、こんなの面白いよというのがあれば教えてください。
