===========================
Sphinx導入までの流れ
===========================

.. warning ::
    * この段階ではドキュメント作成しかできないぞ！！！
    * APIドキュメントの自動作成(sphinx-apidocやautodocの話)はここでは書かないぞ！！！

1. sphinxインストールする
2. sphinx-quickstartする
3. conf.pyいじくる
4. rstファイルいっぱい書く
5. makeする
6. 鑑賞する(グフぐへへ・・・)


Sphinxインストールする
===========================
2つインストールする

* sphinx
* 拡張テーマ sphinx-rtd-theme (デファクトスタンダード)

.. code-block :: sh

    pip install sphinx sphinx-rtd-theme


sphinx-quickstartする
===========================

カレントディレクトにドキュメントのページを作成する.

.. code-block :: sh

    sphinx-quickstart 


こんな感じのメッセージが出てくるので指示に従う

.. code-block :: sh

    Sphinx 2.0.1 クイックスタートユーティリティへようこそ。

    以下の設定値を入力してください（Enter キーのみ押した場合、
    かっこで囲まれた値をデフォルト値として受け入れます）。

    選択されたルートパス: .

    Sphinx 出力用のビルドディレクトリを配置する方法は2つあります。
    ルートパス内にある "_build" ディレクトリを使うか、
    ルートパス内に "source" と "build" ディレクトリを分ける方法です。
    > ソースディレクトリとビルドディレクトリを分ける（y / n） [n]: y

    プロジェクト名は、ビルドされたドキュメントのいくつかの場所にあります。
    > プロジェクト名: Sphinx-Handon
    > 著者名（複数可）: 🦊
    > プロジェクトのリリース []: 0.0.0

    ドキュメントを英語以外の言語で書く場合は、
    言語コードで言語を選択できます。Sphinx は生成したテキストをその言語に翻訳します。

    サポートされているコードのリストについては、
    http://sphinx-doc.org/config.html#confval-language を参照してください。
    > プロジェクトの言語 [en]: en

    ファイル ./source/conf.py を作成しています。
    ファイル ./source/index.rst を作成しています。
    ファイル ./Makefile を作成しています。
    ファイル ./make.bat を作成しています。

    終了：初期ディレクトリ構造が作成されました。

    マスターファイル ./source/index.rst を作成して
    他のドキュメントソースファイルを作成します。次のように Makefile を使ってドキュメントを作成します。
    make builder
    "builder" はサポートされているビルダーの 1 つです。 例: html, latex, または linkcheck。


実行するとファイルとディレクトリが生成される ::

    .
    ├── Makefile ............ ドキュメント作成に使うMakefile
    ├── build/ .............. ドキュメント出力先ディレクトリ
    ├── make.bat ............ Windows用のmakeスクリプト
    └── source/ ............. ドキュメントのソース保存ディレクトリ
        ├── _static/ ........ 静的ファイル保存ディレクトリ
        ├── _templates/ ..... テンプレート保存ディレクトリ
        ├── conf.py ......... sphinx設定スクリプト
        └── index.rst ....... ドキュメントファイル(雛形)


conf.pyいじくる
===========================
* sphinxに拡張テーマ(sphinx_rtd_theme)を適応するために, conf.pyに設定を追加する．
* 生成されたsource/conf.pyに↓を追加

.. code-block :: python
    :emphasize-lines: 1, 4, 7

    import sphinx_rtd_theme

    extensions = [
        "sphinx_rtd_theme",
    ]

    html_theme = "sphinx_rtd_theme"

今回変更した箇所

.. code-block :: sh
    :emphasize-lines: 4

    source/ ............. ドキュメントのソース保存ディレクトリ
    ├── _static/ ........ 静的ファイル保存ディレクトリ
    ├── _templates/ ..... テンプレート保存ディレクトリ
    ├── conf.py ......... sphinx設定スクリプト
    └── index.rst ....... ドキュメントファイル(雛形)

.. note ::
    * 他の拡張の話に少し触れたい
    * sphinx-apidocの話に繋げたい.  


rstファイルいっぱい書く
===========================
* sourceディレクトリにrstファイルをいっぱい書く(今回は2つしか作らないけどな！！！！)
* hell, worldなドキュメントを作成する
* index.rstを編集する

hell, worldなドキュメントを作成する
------------------------------------------------
2つのrstファイルを作成する

* source/hell.rst
* source/text/hell.rst

source/hell.rst
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block :: rst

    ================================================
    Hell, World... 地獄へようこそ (第1層)
    ================================================

    このドキュメントはなんなんだ一体
    ================================================

    このドキュメントはHell, World.のサンプルのドキュメントだ


    C++のHell, Worlo...
    ------------------------------------------------
    なんか尺が余ったのでC++でHell, World...書いときます


    .. code-block :: cpp

        #include<iostream>

        int main(void) {
            std::cout << "Hell, World..." << std::endl;

            return 0;
        }



source/text/hell.rst
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block :: rst

    ================================================
    Hell, World... 地獄へようこそ (第2層)
    ================================================

    このドキュメントはなんなんだ一体
    ================================================

    このドキュメントはHell, World.(C言語)のサンプルのドキュメントだ


    CのHell, Worlo...
    ------------------------------------------------
    なんか尺が余ったのでCでHell, World...書いときます


    .. code-block :: c

        #include<stdio.h>

        int main(void) {
            printf("Hell, World...");

            return 0;
        }


source/index.rstを修正する
------------------------------------------------

↓2つを目次に追加するために, source/index.rstを編集する

* source/hell.rst
* source/text/hell.rst


source/text/hell.rst
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

.. code-block :: rst
    :emphasize-lines: 8,9

    Welcome to Sphinx-Handson's documentation!
    ==========================================
    
    .. toctree::
        :maxdepth: 2
        :caption: Contents:

        hell.rst
        text/hell.rst
   


今回変更した箇所

.. code-block :: sh
    :emphasize-lines: 5,6

    source/ ............. ドキュメントのソース保存ディレクトリ
    ├── _static/ ........ 静的ファイル保存ディレクトリ
    ├── _templates/ ..... テンプレート保存ディレクトリ
    ├── conf.py ......... sphinx設定スクリプト
    ├── hell.py ......... 新しく追加したドキュメントファイル(hell, world...)
    └── index.rst ....... ドキュメントファイル(雛形)


Sphinxでドキュメントをビルドする
=========================================

Makefileがあるディレクトリでmakeコマンドを実行してドキュメントを生成する.

.. code-block :: sh

    make html

コマンドを実行するとbuild/htmlディレクトリにHTMLのドキュメントが生成される.

.. note ::
    ここにサムネイルを貼る

今回のディレクトリ構成に変更があった箇所

.. code-block :: sh
    :emphasize-lines: 3-5

    .
    ├── Makefile ............ ドキュメント作成に使うMakefile
    ├── build/ .............. ドキュメント出力先ディレクトリ
    │   ├── doctrees ........ TODO: なんだっけこれ
    │   └── html ............ 生成したHTMLドキュメント
    ├── make.bat ............ Windows用のmakeスクリプト
    └── source/ ............. ドキュメントのソース保存ディレクトリ
        ├── _static/ ........ 静的ファイル保存ディレクトリ
        ├── _templates/ ..... テンプレート保存ディレクトリ
        ├── conf.py ......... sphinx設定スクリプト
        ├── hell.py ......... 新しく追加したドキュメントファイル(hell, world...)
        └── index.rst ....... ドキュメントファイル(雛形)


補足事項
=====================

使っているライブラリとその説明
--------------------------------------------

.. list-table::
    :widths: 10 15
    :header-rows: 1

    * - ライブラリ名
      - 説明
    * - sphinx
      - sphinx本体
    * - sphinx-rtd-theme
      - sphinxの拡張テーマ