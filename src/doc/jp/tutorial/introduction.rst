******************
イントロダクション
******************

このチュートリアルは、3-4時間ほどで終わります。
HTML、PDF、Sage ノートブック形式で読む事ができます。
Sage ノートブックから読むには、 ``Help`` をクリックし、 ``Tutorial`` をクリックしてください。

SageのほとんどはPythonで実装されていますが、このチュートリアルを読むには、Pythonの知識は必要ありません。
ある程度まで行くと、あなたはPythonを学びたくなるでしょうが、そのための非常に優れた資料がいくつもあります。
例えば、[PyT]_ や [Dive]_ を参照してください。
ただ、Sageのみを素早く試したいなら、このチュートリアルから始めましょう。
下にあるのは、Sageコードの例です。

::

    sage: 2 + 2
    4
    sage: factor(-2007)
    -1 * 3^2 * 223

    sage: A = matrix(4,4, range(16)); A
    [ 0  1  2  3]
    [ 4  5  6  7]
    [ 8  9 10 11]
    [12 13 14 15]

    sage: factor(A.charpoly())
    x^2 * (x^2 - 30*x - 80)

    sage: m = matrix(ZZ,2, range(4))
    sage: m[0,0] = m[0,0] - 3
    sage: m
    [-3  1]
    [ 2  3]

    sage: E = EllipticCurve([1,2,3,4,5]);
    sage: E
    Elliptic Curve defined by y^2 + x*y + 3*y = x^3 + 2*x^2 + 4*x + 5
    over Rational Field
    sage: E.anlist(10)
    [0, 1, 1, 0, -1, -3, 0, -1, -3, -3, -3]
    sage: E.rank()
    1

    sage: k = 1/(sqrt(3)*I + 3/4 + sqrt(73)*5/9); k
    36/(20*sqrt(73) + 36*I*sqrt(3) + 27)
    sage: N(k)
    0.165495678130644 - 0.0521492082074256*I
    sage: N(k,30)      # 30 "bits"
    0.16549568 - 0.052149208*I
    sage: latex(k)
    \frac{36}{20 \, \sqrt{73} + 36 i \, \sqrt{3} + 27}

.. _installation:


インストール
============

もし、Sageをまだインストールしていなくて、ただいくつかのコマンドを試したいだけならば、http://www.sagenb.org で実行する事ができます。

Sageのウェブページ [SA]_ のドキュメントセキュションのSage インストールガイドを参照して、Sageをインストールして下さい。
ここでは単に、2、3のコメントをします。

#. Sageのダウンロードファイルは"電池内臓"です。
   つまり、SageはPython、IPython、PARI、GAP、Singular、Maxima、NTL、GMP等の外部ソフトウェアに依存してますが、ユーザーはこれらを個別にインストールする必要はありません。
   これらは、Sageの配布ファイルに含まれます。
   しかし、MacaulayやKASH等の、Sageのいくつかの機能を使うには、関係するパッケージをインストールする必要があります。
   MacaulayとKASHはSageパッケージに含まれているので、簡単にインストールする事ができます。
   Sageパッケージの一覧を得るには、 ``set -optional`` を実行するか、Sageのウェブサイトの"Download"ページを見てください。

#. コンパイル済みのSageのバイナリファイルを用いると、ソースコードからビルドするよりも簡単にインストールできます。
   ファイルを解凍し、 ``sage`` を実行するだけです。

#. もし、SageTeXパッケージ(Sageの計算結果をLaTeXファイルに落とし込めます)を使いたい場合、SageTexにTexのインストール場所を教える必要があります。
   このためには `Sage installation guild <http://www.sagemath.org/doc/>`_ を参照して下さい
   ( `このリンク <../installation/index.html>`_ でローカルバージョンが見られるかもしれません)。
   環境変数をセットし、ファイルを一つコピーするだけで済みます。 

   SageTexを使うためのドキュメントは ``$SAGE_ROOT/local/share/texmf/text/generig/sagetex/``にあります。
   "``$SAGE_ROOT``"はSageがインストールされているディレクトリを指す環境変数です。

Sageの使い方
================

Sageはいくつかのやり方で使えます。

-  **ノートブック・グラフィック・インターフェース:** リファレンスマニュアルのノートブックのセクションと、:ref:`section-notebook` を見てください。

.. -  **Interactive command line:** see :ref:`chapter-interactive_shell`,
..
.. -  **Programs:** By writing interpreted and compiled programs in
..    Sage (see :ref:`section-loadattach` and :ref:`section-compile`), and
..
.. -  **Scripts:** by writing stand-alone Python scripts that use the Sage
..    library (see :ref:`section-standalone`).


.. Longterm Goals for Sage
.. =======================
..
.. -  **Useful**: Sage's intended audience is mathematics students
..    (from high school to graduate school), teachers, and research
..    mathematicians. The aim is to provide software that can be used to
..    explore and experiment with mathematical constructions in algebra,
..    geometry, number theory, calculus, numerical computation, etc. Sage
..    helps make it easier to interactively experiment with mathematical
..    objects.
..
.. -  **Efficient:** Be fast. Sage uses highly-optimized mature software
..    like GMP, PARI, GAP, and NTL, and so is very fast at certain
..    operations.
..
.. -  **Free and open source:** The source code must be freely
..    available and readable, so users can understand what the system is
..    really doing and more easily extend it. Just as mathematicians gain
..    a deeper understanding of a theorem by carefully reading or at
..    least skimming the proof, people who do computations should be able
..    to understand how the calculations work by reading documented
..    source code. If you use Sage to do computations in a paper you publish,
..    you can rest assured that your readers will always have free access
..    to Sage and all its source code, and you are even allowed to archive and
..    re-distribute the version of Sage you used.
..
.. -  **Easy to compile:** Sage should be easy to compile from source
..    for Linux, OS X and Windows users. This provides more flexibility
..    for users to modify the system.
..
.. -  **Cooperation:** Provide robust interfaces to most other
..    computer algebra systems, including PARI, GAP, Singular, Maxima,
..    KASH, Magma, Maple, and Mathematica. Sage is meant to unify and extend
..    existing math software.
..
.. -  **Well documented:** Tutorial, programming guide, reference
..    manual, and how-to, with numerous examples and discussion of
..    background mathematics.
..
.. -  **Extensible:** Be able to define new data types or derive from
..    built-in types, and use code written in a range of languages.
..
.. -  **User friendly**: It should be easy to understand what
..    functionality is provided for a given object and to view
..    documentation and source code. Also attain a high level of user
..    support.
..
