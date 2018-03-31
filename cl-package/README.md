# CLにおけるパッケージの扱い (Handling of packages in CL)

## パッケージとは  (What is a package?) 
他のプログラミング言語におけるモジュールシステム。  
名前空間とエクスポートするシンボル(すなわち関数や変数)を記述する仕組み。  
ES6のimport/exportの仕様が近い気がする。
(Modular systems in other programming languages. A mechanism to describe a
namespace and exporting symbols (ie, functions and variables). I feel that the
specification of import/export of ES 6 (ECMA 6) is similar.)

## パッケージの定義方法  (How to define packages)
```lisp
(defpackage package-name
  (:nicknames :package-nickname)
  (:use :cl :name-space-A :name-space-B)
  (:export variable-A variable-B function-A function-B))
```

:useで指定したパッケージ名(名前空間)は、そのパッケージ内で省略可能になる。  (:use The package name (namespace) specified in the package can be omitted in the
package)

例えば`hoge:*special*`としていたシンボルが`*special*`として参照出来る。  
基本的には事前にasdfでロードした外部ライブラリのパッケージ名を列挙することになる。  
(For example, the symbol `hoge:*special*` could be referenced as `*special*`. Basically, we will enumerate the package names of external libraries loaded
in advance with asdf.)
:exportで指定したシンボルは外部から参照可能(public)になる。  
:exportで公開されたシンボルは`パッケージ名:シンボル`で呼べる。  
非公開シンボルであっても`パッケージ名::シンボル`で呼び出せる。  
コロンの数がポイント。
(The symbol specified by :export is externally visible (public). The symbol
exported by :export can be called with `package-name:symbol`. Even private
symbols can be called with `package-name::symbol`. The number of colons is the
difference.)

## パッケージの読み込み方  (How to load packages)
```lisp
(use-package :hoge)
```

上記の(Above) :useで指定するのと同じ。(Same as specifying with)
