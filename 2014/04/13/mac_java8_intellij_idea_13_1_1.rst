MacのJava8環境でIntellij IDEA 13.1.1が起動しない
===================================================================

IntelliJ IDEA 13のライセンスをゲットしたので早速起動しようと思ったら起動しない。何度ダブルクリックをしても起動しない。
色々試した結果起動するようになったので備忘録として残しておきます。

起動しない原因と対処
--------------------

環境は

* Mac OSX 10.9 Mavericks
* JDK 1.8.0
* IntelliJ IDEA 13.1.1

です。JDK 8以外は入れていませんJDK 6もJDK 7もです。

エラーログを見たところ、JDK 8のlibserver.dylibがロードできなくてJVMが落ちているらしいです。根本の原因はわかりませんが、JDK 8なのが原因っぽいです。

JDK 7を入れる
^^^^^^^^^^^^^

まずJDK 7を入れましょう。
しかしこれだけではIntelliJはJDK 8を見に行ってしまいます。
たとえJAVA_HOMEをJDK 7にしてもJDK 8を見に行ってしまいます。

Info.plistを編集する
^^^^^^^^^^^^^^^^^^^^

エディタは好きなのを使ってください。

.. code-block:: sh

  $ vi "/Applications/IntelliJ IDEA 13.app/Contents/Info.plist" 

このInfo.plistから

::

  <key>JVMVersion</key>
  <string>1.6*</string>

となっている箇所を

::

  <key>JVMVersion</key>
  <string>1.7*</string>

に書き換えます。

おそらく

.. code-block:: sh

  $ /usr/libexec/java_home -v 1.6

の結果をJAVA_HOMEに使っているのでしょう。
1.6が存在しない場合、このコマンドは1.8のJAVA_HOMEを返します。

これでようやくIntelliJが起動しました。やれやれ。

.. author:: default
.. categories:: none
.. tags:: Mac, IntelliJ IDEA, Java
.. comments::
