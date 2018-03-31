# プロジェクト作成の方法 (How to create a project)

パッケージとasdファイルを組み合わせ、手軽にインストール・ロードが出来る構造をプロジェクトと呼ぶことにする。  
なお、ここではライブラリとアプリケーションを区別しない。  
(Combine the package and the asd file, and call the structure that can be easily
installed / loaded. Note that here, libraries and applications are not
distinguished.)

## 最も楽な方法   (The easiest way)
CL-Projectを使う。  (Use cl-project)
`(ql:quickload :cl-project)`でインストール出来るので予めしておくこと。  (Before using it you can install with)
仮に、(For example) `lisp-dev/`以下に (let's make a system named your-system located in the lisp-dev dir) `your-system`というプロジェクトを作るとしよう。  
```lisp
(cl-project:make-project #p"lisp-dev/your-system"
  :author "Your Name"
  :email "your.email@address.com"
  :license "LLGPL"
  :depends-on '(:cl-cffi-gtk :cl-annot))
```
これでプロジェクトを構成するファイルが指定したディレクトリ以下に作成される。  
:depends-onはlistの形式で記述しないと怒られるので注意。  
このプロジェクトはパスが通っていればそのままquickload出来る。  
テストは`asdf:test-system :your-system`で実行する。  
書き方は[prove](https://github.com/fukamachi/prove)に従う。
(The files constituting the project are created under the specified directory.
Note :depends-on will cause an error unless it is put in a list form. This
project can be quickloaded as it is if the path is passed. Test it with
`asdf:test-system:your-system`. This supposes use of the [prove] unit testing
package (https://github.com/fukamachi/prove).

## 参考  (Reference)
[第6回 Common Lispライブラリを書く](http://modern-cl.blogspot.jp/2011/07/6-common-lisp.html)

[[https://translate.google.com/translate?sl=ja&tl=en&js=y&prev=_t&hl=en&ie=UTF-8&u=http%253A%252F%252Fmodern-cl.blogspot.jp%252F2011%252F07%252F6-common-lisp.html&edit-text=][Writing the 6th Common Lisp library]]
