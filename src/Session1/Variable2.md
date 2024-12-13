# 変数（その２）

ここからは、変数のより詳細な仕様を見ていきます。次のコードを実行してみよう。

```Javascript
function myFunction() {
  var n = 5;
  Logger.log(n);
  n = n + 10;
  Logger.log(n);
}
```

重要なのは`n = n + 10;`というポイントです。ここでは二つの疑問が発生しています。  
1. 変数に値を入れるのに「var」って要らないの？
2. 「=」(イコール)の記号なのに右辺と左辺の値が違うじゃん

## 変数の再代入
変数は変わる数字というぐらいですから、一度決めた値を後から変更することができます。例えばゲームならプレイヤーの座標が毎フレーム変化するのは当たり前のことですよね。
## 代入演算子「=」
代入演算子は変数にデータを代入する演算子です(箱にデータを入れる演算子)。乗算と除算が`*`と`/`で代用されていたように、代入演算子も`=`で代用されています。<span style="color: red;">代入演算子と数学のイコールを混同しないように</span>。
<br><br>
後に登場しますが、GASでイコールは`===`と書きます、変ですよね。

## 変数の初期化省略とnull
次のコードを実行してみましょう。

```Javascript
function myFunction() {
  var n;
  Logger.log(n);
  n = 10;
  Logger.log(n);
}
```

今までと違う点は、nの初期値を設定していない点です。変数の初期化は任意で、省略する事も可能です。しかし、<span style="color: red;">コーディングルールとして変数には初期値を設定することが望ましいです</span>。
<br><br>
最初の表示が`null`となっていますね。GASでは、初期値が設定されていない場合自動でこの値が代入されます。  

### nullとは
`null`ってどんな値でしょうか？0ではありません、箱が空という訳でもありません。箱には`null`が入っています。`null`は、プログラム上でデータが何も含まれていない事を表す値です。
<br><br>
「何も含まれていないってことは空じゃないの？」  
違います、`null`は`null`です。  

## `let`と`const`
### `let`
次のコードを実行してみましょう。

```Javascript
function myFunction() {
  var n = 5;
  Logger.log(n);
  var n = 15;
  Logger.log(n);
}
```

問題なく動作します。では次のコードを実行してみましょう。

```Javascript
function myFunction() {
  let n = 5;
  Logger.log(n);
  let n = 15;
  Logger.log(n);
}
```

おや？実行どころか保存しようとするとエラーが発生してしまいました。安心してください、これが正常な動作です。
![let_error](images/let_error.png)
エラーとなった原因は次の箇所です:`let n = 15;`
<br><br>
`let`は同じスコープ内で同名の変数の定義を禁止する役割を持った`var`です。正確な表現のために少し難しい言い方をしましたが同じ名前の変数を定義出来なくするということです。エラーを修正するには、`n`以外の変数名を使用するか、`n`に再代入する形にします。

```Javascript
function myFunction() {
  let n = 5;
  Logger.log(n);
  let m = 15;
  Logger.log(m);
}
```
```Javascript
function myFunction() {
  let n = 5;
  Logger.log(n);
  n = 15;
  Logger.log(m);
}
```

### `const`
同じ要領で次のコードを実行してみましょう。

```Javascript
function myFunction() {
  const n = 5;
  Logger.log(n);
  const n = 15;
  Logger.log(n);
}
```
```Javascript
function myFunction() {
  const n = 5;
  Logger.log(n);
  n = 15;
  Logger.log(n);
}
```
どちらも保存時にエラーが発生すると思います。`const`は`let`と同じように同じ変数名が使用出来ない事に加え、`n`への再代入も禁止する`var`です。

### どれを使えばいい？
各仕様を表にまとめてみました。
|       | 初期化省略 | 同名定義 | 再代入 |
| ---- | ---- | ---- | ---- |
| `var` | ○ | ○ | ○ |
| `let` | ○ | ○ | × |
| `const` | × | × | × |

下に行くにつれて制約が厳しくなっていますね。原則、<span style="color: red;">制約が厳しい順に使用する</span>ようにしましょう。こうすることによって、変数定義で`let`が使用されている場合は「この変数は後で再代入するんだな」ということが、`var`を使用されている場合は「この変数は後で同名の変数を定義するんだな」ということが一目で分かるようになります。