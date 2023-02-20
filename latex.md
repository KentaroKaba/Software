# Visual Studio Code上でLaTeXのコンパイルをできるようにする

## LaTeXとVisual Studio Codeについて

### Latexとは

**LaTeX**とはフリーの組版ソフトです。
組版とは、文字・図版・写真などを配置することです。
要は、LaTeXを用いてレポートや論文などを作ることができます。

おそらく皆さんが使ったことのある組版ソフトは、Microsoftが提供している**Word**だと思います。
Wordは**GUI**(Graphical User Interface)ですが、LaTeXは**CUI**(Character User Interface)です。
Wordは作成する紙面を直接操作することで編集作業を行いますが、LaTeXはコマンドなどの文字(Character)のみを用いて組版を指定し、
それをもとに紙面が作られます。

LaTeXを使うメリットは色々挙げられますが、数式の記述と、図表の挿入のしやすさがWordに比べて圧倒的に優れていると思います。
事実、この世に出ている論文はLaTeXを用いて作られたものがほとんどです。
あとWordはフォントがダサいです。

LaTeX自体に紙面を編集する機能は無いので、それを行うエディタが必要になります。
そのエディタにVisual Studio Codeを使おうというのが今回の目的です。

### Visual Studio Codeとは

Visual Studio Code(以下、VScode)とは、Microsoftが提供している軽量で高機能なテキストエディタです。
プログラムの編集とかいろいろできます。

VScode上でLaTeXを使うメリットは、視認性の良さと、ショートカットキーとスニペットの多さです。
VScodeは括弧などを自動で色分けしてくれるなど、ユーザーフレンドリーな機能がデフォルトで多く実装されています。
また、文章を作るうえで頻出の環境や単語の挿入、文章の前後関係の入れ替えやコメントアウトなどの編集作業をショートカットキーとスニペットで簡単に行うことができます。

共同編集をする場合はOverleafを使ったほうが良いと思いますが、学部で作る文章は一人で作るものがほとんどだと思うので、自分のPCで完結するVScodeを使うメリットは十分あると思います。

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

インストールが完了したら、VScodeを起動して日本語化を行いましょう。  
Ctrl+Shift+X(Cmd+Shift+X)または左のサイドバーにある  
![image](https://user-images.githubusercontent.com/75883741/220059116-01bb2b8d-b162-456a-878e-0aec8630e883.png)  
のアイコンを押して、拡張機能(Extensions)のページに行きましょう。  
移動が終わったら、検索欄に「Japanese Language Pack for Visual Studio Code」と打ち込み、Installのボタンをクリックしましょう。  
そうしたら右下に表示されたポップアップのRestartを押し、VScodeを再起動しましょう。  
これで日本語化は完了です。

## LaTeXとVScodeの接続

### latexmkの設定

我々は.texファイルの中身を記述することで、組版を指定することができます。しかし、.texファイルを作った時点で紙面はまだ作成されていません。
紙面を作成するためには、.texファイルを.pdfファイルに変換する作業(コンパイル)を行う必要があります。
(コンパイルは正確には.tex -> .pdfではなく、.tex -> .dvi -> .pdfという三店方式をとっています。)

コンパイルは1回で済む場合もありますが、参考文献を記述するパッケージ(Biblatexなど)を用いる場合には、異なる種類のコンパイルを複数回行う必要があります。
そこで「**必要な種類のコンパイルを必要な回数だけ**」行ってくれるのが**latexmk**というものです。

latexmkの設定のためには、ホームディレクトリに.latexmkrcというファイルを作る必要があります。
VScodeを開いて、Ctrl+@(Cmd+@)もしくは上のタブのターミナルをクリックし「新しいターミナル」を選択しましょう。
そこで開かれたターミナルはおそらくホームディレクトリにいるので、
```
code .latexmkrc
```
と打ち込んで、Enterを押せばホームディレクトリに.latexmkrcが作られ、VScodeでそれが開かれているはずです。

まだ.latexmkrcの中身は空なので、次をコピペしてください(中身の説明は面倒なので省きます)。
```
$latex = 'platex %O %S';
$bibtex = 'pbibtex %O %S';
$biber = 'biber --bblencoding=utf8 -u -U --output_safechars %O %S';
$makeindex = 'mendex %O -o %D %S';
$dvipdf = 'dvipdfmx %O -o %D %S';

$max_repeat = 5;
$pdf_mode = 3;
```
これをCtrl+S(Cmd+S)で保存すれば、latexmkの設定は完了です。

### VScodeの設定

VScodeではまだ日本語化を行っただけなので、LaTeXの設定をしていきます。

まず、日本語化を行った時と同じように拡張機能のページに移動して「LaTeX Workshop」と打ち込み、出てきたものをインストールし、VScodeの再起動を行ってください。

次に、Ctrl+,(Cmd+,)を入力し、VScode全体の設定画面を開きます。
設定に移動したら、右上の設定(JSON)を開くというアイコンをクリックします。  
![image2](https://user-images.githubusercontent.com/75883741/220064035-9004f54b-b1bb-4d1c-ac89-6962bc16204e.png)  
そしたら、{}以外何もないと思うので(もしかしたらそれもないかもしれない)、{}の中に次をコピペします(ここも中身の説明は面倒なので省きます)。
```
    "latex-workshop.latex.tools": [
        {
            "name": "latexmk",
            "command": "latexmk",
            "args": [
                "-synctex=1",
                "-interaction=nonstopmode",
                "-file-line-error",
                "-halt-on-error",
                "-pdfdvi",
                "-outdir=%OUTDIR%",
                "%DOC%"
            ],
            "env": {}
        },
    ],
    "latex-workshop.latex.recipes": [
        {
            "name": "latexmk",
            "tools": [
                "latexmk"
            ]
        },
    ],

    "latex-workshop.view.pdf.viewer": "tab",
    "latex-workshop.view.pdf.zoom": "page-width",
```
これでLaTeXがVScode上で動くようになりました。

## 環境のテスト
最後に、実際にVScode上でLaTeXを使った組版ができるのか試してみましょう。

まず、適当なディレクトリに移動します。(わかんなかったら何もしなくていいです。)  
次に、
```
code text.tex
```
と打ち込んで、テスト用の.texファイルを作り、VScode上で開きます。

開けたら、そこに次をコピペします。
```
\documentclass[dvipdfmx]{jsarticle}
\begin{document}
test
\end{document}
```
そして、Ctrl+S(Cmd+S)でファイルを保存し、Ctrl+Alt+B(Cmd+Option+B)でコンパイルを行います。
その後、Ctrl+Alt+V(Cmd+Option+V)を押すと、画面の右半分にtest.pdfファイルが開かれ、「test」のみが書かれていれば完了です。

Ctrl+Alt+B(Cmd+Option+B)はファイルを開いた最初のコンパイルのみに必要で、あとはCtrl+S(Cmd+S)で保存をするたびに勝手にコンパイルが実行されます。

表示されたpdfファイル上でCtrl(Cmd)を押しながらクリックをすると、左の.texファイル上での対応箇所に飛びます。

## 最後に
以上の手順を踏めば、LaTeXをVisual Studio Code上で動かすことができる様になると思います。

ショートカットキーやスニペットに関しては自分で調べてください(気が向いたら追記するかもしれません)。
便利なものが沢山あります。
また、これらは自分で登録することもできます。

この記事を書いたのは、2年前くらいに「LaTeX VScode」で調べて出てきた記事を意味も理解せずに鵜呑みにした結果、様々な問題(エラーが表示されないなど)を抱えながらLaTeXを使う羽目になったからです。
検索して一番上に出てくる記事を参考にしても、**最高の環境にはなりません**。
卒論を書くにあたって今のままではさすがに困ると思って、自分で1から調べ直した結果、最低限の理解ができたかなと思ったのでその備忘録も兼ねています。

LaTeXをきちんと教えてくれる人はいないと思うので、その一助となれば幸いです。
