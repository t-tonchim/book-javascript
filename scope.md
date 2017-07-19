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


```



