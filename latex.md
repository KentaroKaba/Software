# Visual Studio Code上でLaTeXのコンパイルをできるようにする

## LaTeXとVisual Studio Codeとは？

**LaTeX**とはフリーの組版ソフトです。
組版とは、文字・図版・写真などを配置することです。
要は、LaTeXではレポートや論文などを作ることができます。

おそらく皆さんが使ったことのある組版ソフトは、Microsoftが提供している**Word**だと思います。
WordはGUI(Graphical User Interface)ですが、LaTeXはCUI(Character User Interface)です。
Wordは作成する紙面を直接操作することで編集作業を行いますが、LaTeXはコマンドなどの文字(Character)のみを用いて組版を指定し、
それをもとに紙面が作られます。

LaTeXを使うメリットは色々挙げられますが、数式の記述と、図表の挿入のしやすさがWordに比べて圧倒的に優れていると思います。
事実、この世に出ている論文はLaTeXを用いて作られたものがほとんどです。
あとWordはフォントがダサいです。

Visual Studio Codeとは、


## LaTeXの導入
TeX Wikiの[このページ](https://texwiki.texjp.org/?TeX%E5%85%A5%E6%89%8B%E6%B3%95)を見て、インストールしてください。

Windowsの人は**TeX Live**、Macの人は**MacTeX**をインストールします。
OS別のTeXのインストール方法のページへのリンクに飛んで、それに従えば問題なく完了するはずです。

**TeX Live**というのは、TeXの本体と、それをサポートする様々なパッケージが一緒に入ったお得セット(Distributionというらしい)です。
非常に特殊なことをしようとしない限り、TeX Liveのみで十分に完結すると思います(今のところ、私は特に困ったことはありません)。
Mac TeXはTeX Liveをベースにしたものです。

TeXとLaTeXの違いについては、[このページ](https://texwiki.texjp.org/?LaTeX)に書いてあります。
名前が異なるので厳密には区別すべきものではありますが、区別が必要な場合というのはLaTeXそのものをいじるときとかだと思うので、日常生活では同じものを指していると考えていいでしょう。
私はLaTeXと口で言うことは殆どありません。TeXといったほうが短いですしね。

## Visual Stadio Codeの導入
[VScodeのダウンロードページ](https://code.visualstudio.com/download)から自分のPCのOSにあったものを選択してインストーラーをダウンロードし、インストールしてください。
MacOSの人は、Homebrewを使ってインストールもできる様です。次のコードをターミナルに打ち込めばいいらしいです。
```
brew install --cask　visual-studio-code
```
## LaTeXとVScodeの接続
