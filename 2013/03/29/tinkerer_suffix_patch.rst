TinkererのリンクSuffixを設定できるようにする
============================================

例えばこの記事
http://blog.yotchang.org/2013/03/26/start_blog
のように.htmlを付けないPermanent linkが欲しかったのでTinkererの拡張を作りました。

Sphinxではhtml_link_suffixというHTMLのリンクに付けるsuffixを設定できるので、

.. code-block:: python

  html_link_suffix = ''

として.htmlを付けないようにしたのですが、一部.htmlが残ってしまいました。
Tinkererのソースコードを読んだら .html がハードコードされていたので、 .html を付けている
関数を書き換えるモンキーパッチをTinkerer拡張として作りました。

動的型付け言語、特にPythonは素晴らしいですね！
ついでにRSSも書き換えています。

使い方
------
適当に `GitHubのページ <https://github.com/yotchang/tinkerer_suffix_patch>`_ から落としてきて下さい。

適当にインストールして下さい。

.. code-block:: sh

  $ python setup.py install

Tinkererのconfig.pyに追加します。tinkerer.ext.blogの直後に追加して下さい。

.. code-block:: python

  extensions = ['tinkerer.ext.blog', 'tinkerer_suffix_patch']

以下も追加します。

.. code-block:: python

  html_link_suffix = ''

これでHTML内のリンクから .html が無くなります。

もちろんサーバー側がhogeでもhoge.htmlの内容を返すように設定してある必要があります。
GitHub Pagesだとよしなにしてくれますが、Bitbucketではできないようです。

また、Apacheだと簡単に設定できますが、Nginxだとrewriteの魔術が必要です。

多分.htmlが付いてることを気にする人はほぼ居ないので、ただの自己満足ですね。


.. author:: default
.. categories:: none
.. tags:: Tinkerer, Python
.. comments::
