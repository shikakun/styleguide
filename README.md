# Hologram ではじめるスタイルガイド入門

スタイルシートを書くのってほんとうにややこしいですね。気がついたら、どこになにが書かれているのかわからない数万行の CSS 地獄になってしまいます。

CSS 地獄にならないためには、例えばボタンなら共通のボタンのスタイルシートに統一して、どのページでも同じスタイルシートでボタンを表現したほうが、効率的だし仕事も早いですよね。デザインのリニューアルだって一瞬です。さらには、デザイナーが作業しなくてもエンジニアだけでボタンを用意できてしまうという CSS 天国が待っています。

CSS 天国を実現するためには、どのような共通のスタイルシートを用意しているのかまとめてあるドキュメント、「スタイルガイド」を用意しておくと便利です。べつに wiki にまとめてもいいんだけど、wiki って更新するの忘れてしまいがちですよね。そこで、スタイルシートに書いたコメントを抽出して自動でスタイルガイドを生成してくれるっていう便利なツールを紹介したいと思います。

このようなツールは GitHub も使っている [KSS](http://warpspire.com/kss/) や、デフォルトのテンプレートがかっこいい [StyleDocco](http://jacobrask.github.io/styledocco/) などいろいろありますが、ここでは [Hologram](http://trulia.github.io/hologram/) を使ってスタイルガイドを作ってみようと思います。ツールそれぞれに特徴があるので、ぜひいろいろ試してみて自分のプロジェクトに合ったものを選んでください！

* [スタイルガイドについて調べた · Issue #72 · shikakun/tips](https://github.com/shikakun/tips/issues/72)

----

## Hologram を使ってみよう

それでは Hologram でスタイルガイドを作ってみましょう！

スタイルガイドの生成を体験するために、サンプルのかんたんなプロジェクトを用意しました。

* https://github.com/shikakun/styleguide

さっそく以下の手順で Hologram を実行してみましょう。<br>(環境は Mac の OSX、Ruby は最新のバージョンになっている前提のコマンドです！)

1. ターミナルを立ち上げます。
2. ```$ gem install hologram```
  * Mac に Hologram をインストールします。
3. ```$ git clone git@github.com:shikakun/styleguide.git```
  * サンプルプロジェクトを Mac にダウンロードします。
4. ```$ cd styleguide```
  * サンプルプロジェクトのディレクトリへ移動します。
5. ```$ hologram hologram_files/config.yml```
  * Hologram を実行します。

Hologram を実行すると、```app``` ディレクトリと同じ階層に ```styleguide``` というディレクトリができます。このなかにあるファイルが、スタイルガイドです！

```button.html``` をウェブブラウザで開いてみましょう。

![image](https://cloud.githubusercontent.com/assets/1396953/5794732/56020e3c-9fbe-11e4-9a5a-c6868f86cdf2.png)

スタイルガイドができてるぞ!!

## Hologram の仕組み

さきほど生成したスタイルガイドでは例としてボタンのスタイルシートについて説明していますが、この説明がどこに書かれているのかというと、ボタンのスタイルシートが書いてある CSS ファイルにコメントとして書かれています。

[```app/stylesheets/button.css```](https://github.com/shikakun/styleguide/blob/master/app/stylesheets/button.css) には、以下のように書いてあります。

```css
/*doc
---
title: このスタイルシートについて
name: 0-button-outline
category: button
---

このスタイルシートでは、ボタンのスタイルを指定しています。

*/
```

この ```/*doc``` からはじまったコメントが Hologram のために書かれたコメントです。スタイルシートのコメントがすべてスタイルガイドに反映されるわけではなく、Hologram の記法に沿っていないものは無視されます。

それぞれ指定してる項目の意味は以下の通りです。

* ```title:```
  * スタイルガイドで見出しになる文字列です。日本語で書いても問題ありません。
* ```name:```
  * スタイルガイドで URL のアンカーになる文字列です。また、同じ name は同じスタイルの説明として解釈されるので、スタイルの説明ごとに別の name をつける必要があります。半角英数で指定するのがおすすめです。
* ```category:```
  * スタイルガイドの目次に表示されたり、ファイル名になる文字列です。半角英数で指定するのがおすすめです。

コメントは issue でいつも慣れ親しんでいる Markdown で書くことができるので便利ですね。

## Hologram をカスタマイズする

スタイルガイド自体のテンプレートは [```hologram_files/templates```](https://github.com/shikakun/styleguide/tree/master/hologram_files/templates) ディレクトリに入っていて、ヘッダーとフッターのマークアップや、スタイルガイド自体のスタイルシートを編集できるようになっています。目の前の仕事から逃避したいときや、土日に予定がなさすぎてつらいときとかにプロジェクトに合ったおしゃれなデザインをしてみるのも一興です。

そんな暇ないよ！って人は、モダンな Hologram のテンプレートを作って公開してる人もいるので、そのまま使うなりディレクトリ構成を参考にするなりしてみたらいかがでしょうか。

* Cortana
  * https://github.com/Yago/Cortana

これは、CodeGrid っていう有料のメールマガジンで Hologram の使い方を紹介していたときのサンプルコード。サンプルコードは GitHub で無料で公開されています。

* Hologramでカスタムスタイルガイド
  * https://github.com/codegrid/hologram

<blockquote>
  <p>このサンプルプロジェクトの Hologram は、実は Markdown をパースするところもカスタマイズしています。</p>
  <pre>```example<br><button class="button">ボタン</button><br>```</pre>
  <p>というように書くと、実際にボタンとして html を表示してコードも併記できるようにしています。<br>
  詳しくは <a href="https://github.com/shikakun/styleguide/blob/master/hologram_files/markdown_renderer.rb"><code>hologram_files/markdown_renderer.rb</code></a> を参照ください。<br>
  Hologram はカスタマイズ性が高いので、自分の好きなように表示できてめっちゃ楽しい。</p>
</blockquote>

----

実際にスタイルガイドを書きながらスタイルシートを書いていると、いつも誰かに説明を迫られているような気がして、scss の長い入れ子を分割したり、どうしてこのように書いているのかをマメにコメントするようになって、あとから自分で見返したときもわかりやすくなって良いなと思います。

あと、サンプルの html が一覧になっていることで、そのスタイルシートがうまく適用されなくて壊れたスタイルが見つけやすいという、テスト的な使い方もできるなーと思いました。

まだ全然手探りでやってますけど、なかなかよかったので、とりいそぎご紹介でした！
