# スコープ

JavaScriptはES2015で`let`や`const`が使用できるようになるまでは変数や関数のスコープが他の言語と異なり、そのため勘違いされやすい仕様の一つです。

#### varにおけるスコープ

`var`によって宣言された変数のスコープはブロックではありません。`function(){}`のブロック内のみ（関数スコープ）です。

```js
if(true) {
  var a = 'a';
}

function foo(){
  var b = 'b';
}

console.log(a); //=> 'a' 参照できる
console.log(b); //=> ReferenceError: b is not defined 参照できない
```

#### let, constにおけるスコープ

`let`または`const`によって宣言された変数のスコープはおなじみのブロックスコープです。

```js
if(true) {
  let a = 'a';
  const b = 'b';
}

console.log(a); //=> ReferenceError: a is not defined 参照できない
console.log(b); //=> ReferenceError: b is not defined 参照できない
```

### モジュールバンドラのない環境での注意点

webpackなどのモジュールバンドラ（複数のファイルを統合して一つのファイルにまとめてくれるツール）を使用していない場合は、即時関数を使用して別のファイルへ影響を広げないようにしなければなりません。以下のように実装してみると理由がはっきりします。

```js
// a.js

var n = 0;
function funcA(){
  n++; // 本来はこのように外部のスコープの変数に影響を与えるような処理はしてはいけません。
  console.log(n);
}
```

```js
// b.js

var n = 0;
function funcB(){
  n++;
  console.log(n);
}
```

```html
<!DOCTYPE html>
<html lang="ja">
  <head>
    <meta charset="UTF-8">
    <title></title>
    <script src="a.js"></script>
    <script src="b.js"></script>
    <script>
      funcA(); // 1 と表示される
      funcB(); // 2 と表示される!?
    </script>
  </head>
  <body>
  </body>
</html>
```



