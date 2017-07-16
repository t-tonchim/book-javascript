# 型

Javaなどの静的型付け言語のユーザーの一部はしばしば「JavaScript（やRuby, Pythonなど）には型が無い」と言います。これは誤りで動的型付け言語という名の通り、実行時に型が変化するためそのような誤解が生まれています。しかし、当然ながら実際にコーディングする時には型を意識して記述しなければいけません。

動的に型が変化するからといってそこまで構えることもありません。良い書き方をすれば変数の状態を気にして混乱することもありません。

## JavaScriptにおける型

変数について説明する前にJavaScriptの型について簡単に説明します。型には以下のものが存在します。

* プリミティブ型（Immutableつまり不変の値。代入した場合、変数には値そのものが入る\)
  * Boolean `true`
  * Null `null`
  * Undefined  `undefined`
  * Number `1`
  * String ```'foo' "bar" `buz`(``はES6以降のみ)```
  * Symbol （ES2015以降\)
* オブジェクト（Mutable、動的に変更可能。変数に代入した場合、変数には参照が入る）
  * オブジェクトリテラル `{ foo: "bar" }`
  * 配列　`[1, 2, 3]`
  * 関数 `function f() { ... }`
  * etc..

## JavaScriptの真偽判定

JavaScriptでは`true` と`false` 以外に値そのものを真偽の判定に使うことができます。以下の例では`true`が出力されます。

```js
if("a" && [] && {} && (function(){}) && true　&& 10) {
  console.log(true);
} else {
  console.log(false);
}
```

次の例では`false`となります。

```js
if("" || null || undefined || false || 0) {
  console.log(true);
} else {
  console.log(false);
}
```

#### 比較演算子の==と===

JavaScriptの比較では基本的に`===`を使用すべきです。`==`を使用した場合は以下のような場合に思いがけない結果となります。

```js
// 暗黙的に型変換がなされる
"1"  == 1         //=> true
0    == false     //=> true
null == undefined //=> true

// 型変換はされない
"1"  === 1         //=> false
0    === false     //=> false
null === undefined //=> false
```

## オブジェクト

オブジェクトは利便性が高くJavaScriptでよく使用されます。オブジェクトのプロパティは`{ key: value }`の形式になっているのでMap構造に類似していますが、Mapは別に存在します（ES2015以降）。valueには何でも入ります。

```js
var obj = {
  foo: "foo",
  bar: [1, 2, 3],
  buz: function() {
    console.log('hello, world');
  },
  obj: { hoge: "hoge"}
};

obj.foo //=> "foo"
obj.bar //=> [1, 2, 3]
obj.buz() //=> "hello, world"
obj.obj //=> { hoge: "hoge" }
```

また、比較演算子をオブジェクトに使う場合は注意が必要です。同じ構造のオブジェクトでも参照が異なれば同一、同値とはみなされません。プロパティを比較するようにしましょう。

```js
var obj = { foo: 'foo' }
obj ==  { foo: 'foo' } //=> false
obj === { foo: 'foo' } //=> false

// プロパティを比較するようにすればいい
obj.foo === 'foo' //=> true
```



