Fuzoku実践入門 環境サンプルファイル
====================================

[![Fuzoku実践入門](http://f.st-hatena.com/images/fotolife/l/learning-fuzoku/20141105/20141105234306.jpg)](http://www.amazon.co.jp/exec/obidos/ASIN/B00P4X25HO/)

このリポジトリは、Amazonで好評発売中の『[Fuzoku実践入門](http://www.amazon.co.jp/exec/obidos/ASIN/B00P4X25HO/)』の原稿執筆に実際使われた環境ファイルです。

『はじめに』と『第1章』のサンプルも兼ているため、ダウンロードして環境を整えることで、誰でもビルドすることが可能です。

なお、/src以下のMarkdownファイルは、ゲラ段階のものになっているため、プロジェクトルートにあるReviewファイルと一部内容が異なります。

Sample Files
------------

* [EPUB版](https://github.com/akinomurasame/learning-fuzoku-sample/blob/master/assets/learning-fuzoku-sample.epub?raw=true)
* [PDF版](https://github.com/akinomurasame/learning-fuzoku-sample/blob/master/assets/learning-fuzoku-sample.pdf?raw=true)
* [MOBI版](https://github.com/akinomurasame/learning-fuzoku-sample/blob/master/assets/learning-fuzoku-sample.mobi?raw=true)

How to install
--------------

    $ git clone https://github.com/akinomurasame/learning-fuzoku-sample.git

Setup
-----

    $ bundle install --path vendor/bundle --binstubs vendor/bundle/bin

How to build
------------

    $ rake -T
    rake all             # create all books (.epub, .pdf, .mobi)
    rake clean           # clean working files
    rake epub            # create .epub
    rake md2review       # convert ./src/*.md to ./*.re
    rake mobi            # create .mobi
    rake pdf             # create .pdf
    rake send_to_kindle  # send to kindle

If you want to build EPUB, Execute this command

    $ rake epub

Requirements
------------

### KindleGen for making .mobi

    $ brew tap homebrew/binary
    $ brew install kindlegen

### MacTex for making .pdf

    $ brew install caskroom/cask/brew-cask
    $ brew cask install mactex

Even if you have been completed to the installation of mactex, you need to add the `/usr/texbin` to the PATH environment variable.

### kindlemail

1. Get OAuth Token
2. Setup kindlemail

Follow the instructions from https://github.com/djhworld/kindlemail

参考記事: [kidlemailを使ってコマンドラインからKindleへファイルを送る - Fuzoku実践入門ブログ](http://learning-fuzoku.hatenablog.com/entry/2014/11/06/153447)
