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
* 拡張テーマ (デファクトスタンダード)

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
生成されたsource/conf.pyに↓を追加

.. code-block :: python

    import sphinx_rtd_theme

    extensions = [
        ...
        "sphinx_rtd_theme",
    ]

    html_theme = "sphinx_rtd_theme"


.. note ::
    * 他の拡張の話に少し触れたい
    * sphinx-apidocの話に繋げたい.  

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