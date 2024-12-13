# 算術演算子
ただ文字や数値を表示していてもつまらないですよね。ここでは算術演算子を学んで、ただ表示させるプログラムから電卓程度の機能を持ったプログラムを作っていきましょう。
## 四則演算
次のプログラムを実行してみましょう。
```js
function myFunction() {
  Logger.log(3 + 4 * 5 - 6 / 8);
}
```
「22.25」と表示されていれば成功です。「+」と「-」は分かりやすいですが、なぜ×ではなく「*」で、÷ではなく「/」なのでしょうか。これは昔、使用できる文字が限られていた時の名残ですが、文字の節約のために代わりの文字が使用されています。ややこしいですがプログラムの世界ではこれが常識となっています。

## MOD演算子
次のコードを実行してみましょう。
```js
function myFunction() {
  Logger.log(10 % 3);
}
```
プログラムの世界では「%」演算子をよく使用します。これは「MOD演算子」といい、上の例でいうと「10を3で割った余り」を求めます。四則演算子にこのMOD演算子を合わせて算術演算子と言います。様々な利用用途がありますが、例えば倍数の判定で使用します。
```
n % 2
```
2で割った余りが0の場合→2で割り切れる→偶数  
2で割った余りが1の場合→2で割り切れない→奇数

## 演算子の優先順位
四則演算では、加算、減算より乗算、除算を先に行うのがルールですよね。加減算を先に行いたい場合は次のように()で囲みます。
```js
Logger.log((3 + 4) * (5 - 6));
```
数学の中カッコと大カッコは使用できないので注意しましょう。  
MOD演算子は乗除算演算子と同じ優先順位です。
<br><br>
GASにはこの他にもたくさんの演算子があり、全てに優先順位が設定されています。これは極めて重要なことなので覚えるようにしましょう。自信がない場合は()で囲えば最初に計算してくれます。

## 文字列の加算？
次のコードを実行してみましょう。
```js
function myFunction() {
  Logger.log('abc' + 'def');
}
```
GASにおいて、文字列+文字列は文字列の連結を表します。では次のコードは？
```js
function myFunction() {
  Logger.log('abc' + 345);
}
```
'abc345'となりました。GASにおいて、<span style="color: red;">文字列+数値は数値を文字列として扱い、文字列の連結</span>になります。この変換は暗黙的に行われるので気をつけましょう。