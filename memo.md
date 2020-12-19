## 環境構築

Anaconda(jupyter)を Docker コンテナで動かす。

> docker pull datascientist/ds-python-env

windows 環境では-v の後にフルパスを指定する。

> docker run -v C:\Users\KOHEI\Documents\GitHub\python\work:\work -p 8888:8888 --name my-env datascientistus/ds-python-env

## jupyter lab 使い方

Markdown モード

Kernel>Shutdown Kernel>Restart Kernel

Setting>JupyterLab theme

Shift を押しながら ↑↓ カーソルで複数行を選択して shift+M を押すとセルの統合ができる。

esc+A で上にセルを追加
esc+B で下にセルを追加
esc+D2 回でセルを削除
esc+Z で Undo
shift+Z で Redo
Ctrl+B でサイドバー開閉
Ctrl+スラッシュでコメントアウト
Ctrl+]でインデント
Ctrl+[でアンインデント
Ctrl+→← で単語の先端や後ろに
Shift+Ctrl+→← で単語を選択状態に
alt+→← で単語の先端や後ろに

Shift+Tab で関数のリファレンス(★ 重要)

## python 基本

### DataType

#### Numbers

3 とか"hello"は python では全てオブジェクトと呼ばれる。
Type(object)関数を使えば、Datatype を確認できる。

Numbers⇒integer(3)、float(1.0)、複素数(3.14j)の 3 つ

interger と Float で計算すると、結果は Float になる。(例:3+1.0)情報量が多い DataType になる点が Point。

1 == 1.0 は true

10 の-a 乗は[1e-a]と書ける。

#### Strings

シングル、ダブルクオーテーションどちらも使用可能。

'''クオーテーションを 3 つで囲むと、複数行の文字列を書ける。(\n で改行)

```python
index は 0 からスタートする。
'hello'[0]⇒'h'
[1:3]は 1 以上 3 未満を表す
'hello'[1:3]⇒'el'。
[-4]は後ろから 4 文字目までを表す
'fileID.png'[:-4]⇒'fileID'
format()の引数は文字列の{}に代入できる。
'hello {}'.format('world')⇒'hello world'
format()の引数は複数代入できる。
'key is {}, value is {}'.format('KEY', 'VALUE')⇒'key is KEY, value is VALUE'
format()の引数の代入場所は指定できる。
'key is {k}, value is {v}'.format(k='KEY', v='VALUE')⇒'key is KEY, value is VALUE'
+でつなげれば、文字列連結が可能
'hello' + 'world'⇒'helloworld'
split()の引数を区切り文字として、文字列をList形式で分割できる。
'hello_world'.split('_')⇒['hello', 'world']
'文字列'.join()で、join()の引数を結合できる。
''.join(['hello', 'world'])
'helloworld'
```

#### Lists

```python
append()でlistに要素を追加できる。
+でリストを結合できる。
```

#### Dictionary

{ key:value } というペアで要素を作成。
dictionary は list と違い順番を持たないので、list[0]のような検索ができない。
代わりに、key で value を検索できる。
key を数字にすることはあまりない。

```python
dict1 = {'key1':'value1', 'key2':2, 3:'value3' }
dict1['key1']⇒'value1'

Dictionaryのkeyとvalueを追加することもできる。
dict1['key4'] = 'value4'
Dictionaryのkeyとvalueを上書きすることもできる。
dict1['key1'] = 'value1 updated'
dict1,keys()でkeyの一覧Listを取得できる。
dict1,values()でvalueの一覧Listを取得できる。
```

#### Boolean

True/False

#### Tuples

変更できない List で、検索が List よりも少し高速になる。関数の戻り値などに使用する。

#### Set

重複を許さない List
重複していたら、除外される。

```python
set={1,1,1,1,2,2,2,3,3,}
set
```

#### Casting

int(1.0)⇒1

bool(1)⇒True

### 演算子

```python
2*3
⇒6
2**3
⇒8
16//5
⇒3(割り算の商のみ)
16%5
⇒1(割り算の余りのみ)
'w' in 'helloworld'
⇒True
'w' in ['w','o','r','l','d']
⇒True
a = [1,2]
b = [1,2]
a == b
⇒True(同一の値かどうか)
a is b
⇒False(同一オブジェクト(同じメモリに存在する)かどうか)
id(a)
⇒aが保存されているメモリのidを表示
a = None⇒NULLのようなイメージ
a is None
⇒True
```

is は None 判定に用いる。
None は undefined とは異なる。

### If

```python
if a == 2:
    print('a is 2')
else:
    print('a is not 2')
```

1 行でも書ける(この書き方は else が必要)
ラムダ関数で頻出。
(True の時の処理) if a == 2 else (True の時の処理)

```python
print('a is 2') if a == 2 else print('a is not 2')
```

### Loop

#### For 文

for 要素 in リスト:の形

```python
colors = ['red', 'blue']
for color in colors:
    print(color)
```

range(start, stop, step)
⇒[start, start+step, start+step*2(stop 未満)]のリストを作成可能。for 文内で連番を作る際によく使う。

```python
for i in range(10):
    print(i)
```

enumerate()
⇒list の index と要素どちらも使いたいときに使う。

```python
colors = ['red', 'blue']
for idx, color in enumerate(colors):
    print('{}: {}'.format(idx, color))
```

#### リスト内包表記

colors というリストから、colors_png というリストを新たに作りたい時に、for 文よりも早く作成できる。

作りたいリスト
colors_png = ['red.png', 'blue.png']

```python
colors = ['red', 'blue']
colors_png = []
for color in colors:
    color_png = color + '.png'
    color_png.append(color_png)
```

[(やりたい処理) for color in colors ]

```python
colors = ['red', 'blue']
[ color + '.png' for color in colors ]
```

#### while 文(上記 2 つに比べると、あまり使わない)

While loop⇒ ある条件が満たされている間はループ

```python
i = 0
while i < 5:
    print(i)
    i += 1
```

### iterable と iterator

iterable: Strings, List, Tuple, Set, Dictionary
Not iterable: Integer, Float, Boolean

iterable:iter()で iterator を返すオブジェクト
iterator:next()で iteration できるオブジェクト

iterable なオブジェクトは iteration(反復(Loop)処理)できる。

> iter(colors)

iterator が返されることが分かる。itaratir も iterable なオブジェクト。
<list_iterator at 0x7fef888bc0d0>

> colors_i = iter(colors)
> next(colors_i)

iterable なオブジェクトを list に入れると、list 型で返ってくる。

> r = range(10)
> list(r)

#### 関数

python では def を使って関数を定義

> def function_name(param1, param2)

もし関数からの戻り値を変数に格納していなくても、最後に実行したコードの戻り値であれば、\_(アンダースコア)に自動的に格納されている。

パラメタ名を指定して引数を渡すことが可能。

> function_name(param1='a', param2='b')

パラメタにデフォルト値を指定することができる。

> def function_name(param1, param2='hello')

しかし、デフォルト値を持たないパラメタ(param2)の前にデフォルト値を持つパラメタ(param1)を置くことはできない。

> def function_name(param1='hello', param2)

#### mutable と immutable

mutable(データが大きくなりがち)
⇒list,dictionary,set

immtable
⇒integer,float,bool,string,tuple

integer は immutable なので、値を変更するとメモリの参照箇所も変わっているはず。
immutable なので、値が変更できないから、コンピュータは新しいメモリに場所を確保して値を返している。

```python
a = 1
print(id(a))
a = 2
print(id(a))
```

さて、以下のような append_elem というメソッドに mutable な list_a と 4 を引数に渡す。
実行後に list_a の値は？

```python
def append_elem(list_param, elem=0)
    list_param.append(elem)
    return list_param

list_a = [1,2,3]
list_b = append_elem(list_a, elem=4)
list_a
```

実は append_elem に渡された list_a は、[1,2,3]という値ではなく、list_a が指すメモリの場所が渡されている。
このような仕組みを参照渡し(値を共有して、メモリは確保しない)という。

```py
def print_id(param):
    #param += 1
    print(id(param))

a = 5
print(id(a))
print_id(a)
```

一方で、immtable な値を同じような関数に渡すと、値が変化しないはず。
immtable なオブジェクトの場合は、値渡し(値のコピーを渡してメモリを新たに確保する。)のような挙動をする。
値が変更されない限りは、メモリは同じ場所を参照するが、
値を変更すると、メモリの場所が変化する。

### Lambda 関数

以下のように func という名前をつけるまでもない関数に使う。

```py
def func(a):
    return a + 1
↓
x = lambda a: a + 1

x(3)
4
```

### \*args と\*\*kwargs

\*args はいくつでも引数を受け取れる。並列処理では args を使う。
func2 の args の正体は、tuple(変更できないリスト)
func2 に[1,3,4]というリストを渡したら、それは変更できない tuple となる。

```py
def func1(a, b)
    return a + b

def func2(*args)
    return args[0] + args[1]
```

kwargs は keywordargs の略。並列処理以外では kwargs の方がよく使われる。
\*args の dictionary 版
引数が多くなる場合はこれを使うと良い。

kwargs.get(Key)で value を取ってこれる。
kwargs.get(Key, 100)で、Key に値が入っていなくても 100 を初期値として取得できる。

```py
def print_dict(**kwargs)
    print(kwargs)

print_dict(a=1, b=2)
⇒{'a': 1, 'b': 2}

print(kwargs.get('a'))
```

\*(アスタリスク)はアンパッキングオペレーターと呼ばれる。
\*\*では Dictionary のアパッキングができる。

```py
a = [1,2,3,4]
print(a)
print(*a)
[1, 2, 3, 4]
1 2 3 4
```

並列処理でラッパー関数を作るときに\*を使う。

f←f'

関数 f を参照する関数 f'という 2 つの関数があり、ユーザは関数 f を直接使うのではなく、関数 f'を使う事で、関数 f の処理を呼び出す、ということがよくある。
ユーザは関数 f のことを知る必要がない。
関数 f'のことを関数 f のラッパー関数と呼ぶ。

リスト内包表記と併せて使うと便利。

```py
def hoge(a, b, c)
    return aaa

def hoge_wrap(args)
    return hoge(*args)

list_hoge = [{'a':1,'b':2,'a':3 },{'a':1,'b':2,'a':3 }]
[hoge_wrap(arg) for arg in list_hoge]
```

```py
def func(a, b):
    return a+10, b+10

戻り値2つはtuple型になる。
result = func(10, 20)
⇒{20, 30}

戻り値2つはアンパックされてx､yに格納される。
x, y = func(20, 30)
x
⇒20

戻り値1つを変数x､y2つでは格納できないので、エラーになる。
def func(a, b):
    return a = 10

x, y = func(20, 30)
⇒
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-75-025479dacf46> in <module>
      2     return a+10
      3
----> 4 x, y = func(20, 30)

TypeError: cannot unpack non-iterable int object
```

## Numpy

Numerical Python の略

まず import する。

```py
import numpy as np

//numpy のファイルの場所を表示
np.__file__
```
