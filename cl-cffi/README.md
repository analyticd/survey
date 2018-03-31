# CL-CFFIに関する備忘録

### defctype  
ポインタ型を定義する。Cのtypedefに対応。
:pointerのエイリアス型的な使い方が見られるので意味合いについては要検証。  

(Define a pointer type. Corresponds to C typedef. Since alias type usage of
:pointer can be seen, it is necessary to verify the meaning.)
```lisp
(defctype image* (:pointer image))
```

### defcstruct  
構造体の定義。Cのstructに対応。  
フィールド名と型の位置が逆なので分かりにくい。  
(Definition of structure. Corresponds to C struct. It is hard to understand
because the field name and type position are opposite.)
```lisp
(defcstruct image
  (width :int)
  (height :int)
  (data :string))
```

### defcfun  
Cの関数へのインターフェースを作成。  
最初に返り値の型を書いて、その後ろに引数を羅列する。  
(Create an interface to C functions. First write the type of return value and
list the arguments after it.)
```lisp
(defcfun ("c_function_name" lisp-function-name) :void
  (x :double) (y :double) (img image*))
```

### with-foreign-objects  
C版letみたいなやつ。  
初期値じゃなくて型を指定する。  
let1に対応するwith-foreign-objectもある。  
(C let like a let's. Specify the type rather than the initial value. There is
also with-foreign-object corresponding to let1.)
```lisp
(with-foreign-objects ((x :int) (y :int) (img '(:struct image)))
  (setf x 3 y 9)
  (lisp-c-function x y img))
```

### with-foreign-slots  
defcstructで定義した構造体のフィールドにアクセスする。  
(Access the fields of the structure defined by defcstruct)
```lisp
(with-foreign-slots ((width height data) img (:struct image))
  (setf width 320 height 240 data *image-data*))
```
