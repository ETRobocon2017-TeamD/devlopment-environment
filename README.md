# EV3RT開発環境 構築手順

現在(2017-04-04),TOPPERS/EV3RT開発環境を最短で構築する手順を示す。ユーザが多いと思われるWindows10を想定。
macOSは公式ページ通りにやればできるが、一応書いておく。

## Windows

最初は[公式の開発環境構築のマニュアル](http://dev.toppers.jp/trac_user/ev3pf/wiki/DevEnv#開発環境構築のマニュアル)の通りに進める。
<pre>
開発プラットフォームEV3RTのダウンロード＆インストール
ダウンロードページからEV3RTのパッケージをダウンロードし、以下の手順に従ってインストールしてください。 
① zipファイルを解凍し、プラットフォームのパッケージ（hrp2.tar.xz）を作業フォルダに移動します。 
作業フォルダの場所は基本的に自由ですが、パスにスペースや全角文字が含まれている場所は避けてください。 
② ターミナルを開いて作業フォルダに移動します（もし、Windows環境でCygwinをインストールしていない方は、先に「開発環境（クロスコンパイラ，ツール）のインストール」を実施してください）。 
③ 下記のコマンドでプラットフォームの簡易パッケージを解凍します 
注意：解凍ソフトを使用して解凍すると、アーカイブに含まれるシンボリックリンクが壊れてしまうことがありますので、以下のように tar コマンドを使用してください。 
$ tar xvf hrp2.tar.xz
作業フォルダに、hrp2 フォルダができたら、プラットフォームのインストールが完了です。 
</pre>

* Bash on Ubuntu on Windows をインストール
* コマンドプロンプトで bash を たたき、ubuntu 14.04 を起動
* ARM社が提供するGCC用APTリポジトリをapt sourceに追加する
<pre>
$ sudo add-apt-repository ppa:team-gcc-arm-embedded/ppa
</pre>
* aptを更新
<pre>
$ sudo apt update
</pre>
* ARM用GCCをインストールする
<pre>
$ sudo apt install gcc-arm-embedded
</pre>
注意：gcc-arm-none-eabiは canonical社 が提供する arm向けgccだ。誤ってgcc-arm-none-eabiインストールするとサンプルプログラムのビルドが通らない。インストールしないように！

* ブートローダーを生成するためのツールをインストールする
<pre>
$ sudo apt install u-boot-tools
</pre>

* EV3RTのコンフィギュレータ cfg のソースをビルドするために boost が必要。 windows10のubuntu-trustyだと 1.55 が最新。
<pre>
$ sudo apt install libboost1.55-all-dev
</pre>

* EV3RTのコンフィギュレータのインストール

端末で，EV3RTのパッケージをインストールした場所に移動して cfg をビルドする 

<pre>
$ cd hrp2/cfg
$ make
</pre>

以上が終わったらサンプルをビルドしてみましょう。
[サンプルアプリケーションのビルドと実行 ¶](http://dev.toppers.jp/trac_user/ev3pf/wiki/SampleProgram)
