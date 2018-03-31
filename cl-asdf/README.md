# ASDFの使い方 (How to use)

## ASDFの役割  (The role of)
Lispシステムのコンパイルやロード、テストを司る。  
より分かりやすい表現では、外部ライブラリのリンクやテストの実行関数を提供する。

Lisp. Compile, load and test the system. In a more comprehensible expression, it
provides links to external libraries and test execution functions.

## 使い方  (How to use)
外部システムはQuicklispでダウンロード・インストールすれば良いとして、それをロードするにはパスを通さなければならない。  

The external system should be downloaded and installed with Quicklisp, and you
must pass it to load it. 

ASDFのデフォルトパスは (The default path of F is)`~/common-lisp`と(and)`~/.local/share/common-lisp/source`を示している。  (respectively)
基本的にはこの中にシステムをインストールすれば良いのだが、Quicklispは (Basically you just install the system in this, Quicklisp)`~/quicklisp/dists/(dist name)/software/`にシステムをインストールしてしまう(I install the system to)(Roswellを使っている場合は(If you are using)`~/.roswell/impls/ALL/ALL/quicklisp/dists/quicklisp/software/`)。  
ASDFの設定は(Setting of)`~/.config/common-lisp/source-registry.conf`に書く。(Write on)  
```lisp
(:source-registry
  (:tree "~/quicklisp/dists/")
  (:tree "~/lisp-dev/")
  :inherit-configuration)
```

:treeは下に書くほど優先度が高いため、開発版のテストなどをしたい時は (The higher you write below, the higher the priority, so when you want to do development testing etc.) `~/lisp-dev`にシステムを置くと良い。  (It is good to put the system on)
これで (with this)`(require 'your-system)`または (or) `(asdf:load-system 'your-system)`で外部システムをロード出来る。 (You can load an external system with)
テストをしたい時は (When you want to test) `(asdf:test-system 'your-system)`で実行してくれる。  (It will run in)
ちなみにQuicklispは内部でASDFを呼んでいるので、quickloadのパスにも適用される。  (By the way, since Quicklisp calls ASDF internally, it also applies to the path
of quickload)

## 参考  (reference)
[require, ASDF, quicklispを正しく使う](use correctly)(http://keens.github.io/blog/2014/11/30/quicklisp/)
