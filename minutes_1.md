# 第一回議事録

## 関数の定義の方法

### 関数命令

+ ソースを読み込むタイミングで関数として登録されるので、どこでも呼び出せる。

### 関数リテラル

+ 評価される前に呼び出すことは出来ない。

```JavaScript
//変数宣言する前なので、undefinedになる。
console.log(getTriangleLiteral(5, 2));
//関数として登録されているので、実行できる。
console.log(getTriangle(5, 2));

var getTriangleLiteral = function(base, height) {
  return vase * height / 2;
};

function getTriangle(base, height) {
  return vase * height / 2;
};
```

### Functionコンストラクター

+ 使わない -> evalと同じで動的に処理の内容を操作できちゃう。

+ どうしても使う必要がある場合、以下の箇所では使用しないこと

  1. while/forのような繰り返すブロックの中

  1. 頻繁に呼び出される関数の中

  + 実行時にコードを解析から関数オブジェクトの生成まで行うため(パフォーマンス低下の一因になる)。

### scriptブロック

+ 関数を定義したスクリプトブロックは、呼び出し側より前か同じブロックに記述する必要がある。

+ 例) `jQuery`と`jQueryのプラグイン`の関係

## スコープ

### グローバルスコープ・ローカルスコープ

1. ブロック外で宣言された変数は、グローバルスコープ

1. 関数ブロックの中で宣言された変数は、ローカルスコープ

1. 同じ変数名がどちらでも宣言されている場合は、ローカルスコープの値が優先される。

1. `var`等が省力された場合には、グローバル変数として扱う。

1. `var`は何度でも宣言できるので注意。

1. function命令のあとに同じ名前の変数を`var`宣言したら、上書きされるので注意。

```JavaScript
function foo() {
  return 'foo';
};

console.log(foo()); //fooが表示される

var foo = 'bar';

console.log(foo()); //TypeError: foo is not a functionとなる

```

### 巻上げ(ホスティング)

+ 3の場合、ローカルスコープ内は、ローカルスコープで宣言された値が使用される。

+ 変数宣言前に変数を呼び出していると、`undifined` になるので注意！

### 仮引数のスコープ(参照型の値の場合)

+ 参照型のデータの場合、ローカルスコープで処理された内容も引数も渡した値そのものに影響する。

```JavaScript
var value = [1, 2, 3, 4, 5, 6];

function deleteElement(value) {
  value.pop();
  return value;
}

console.log(deleteElement(value)); //[1, 2, 3, 4, 5]
console.log(value); //◯[1, 2, 3, 4, 5] ✕[1, 2, 3, 4, 5, 6]
```

### if/whileのスコープ

+ ES2015以前はローカルスコープを作るのは、`function`の場合のみ。

+ ES2015から`let`、 `const`を使えばローカルスコープを作れる。

+ 変数は極力`let`、`const`で宣言する。

+ `var`しか使えない環境では、スコープを意識すること。

+ もしくは、即時関数でラップして擬似的にブロックスコープを作る

```JavaScript
//即時関数
(function () {
  var i = 5;
  console.log(i);
}).call(this);

console.log(i); //undifined
```

+ Functionコンストラクターのブロックではグローバル変数を参照する。

**「JavaScript 本格入門」(著 山田祥寛)chapter4より引用**
