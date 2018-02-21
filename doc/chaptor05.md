# prototypeによるオブジェクト指向

## JavaScriptのオブジェクト指向

### JavaScriptにおけるクラスの宣言

- Class(Prototype)はFunctionオブジェクトをコンストラクタとして使用する。

- コンストラクタとして実行した場合にはObjectが戻り値となるが、

   明示的に宣言する必要は無いので注意。

  ```javascript
  //コンストラクタの宣言
  const Member = function(firstName, lastName) {
    // this.~: プロパティ・メソッドの宣言
    this.firstName = firstName;
    this.lastName = lastName;
    // メソッドは、prototypeオブジェクトを用いる方法が推奨される(後述)
    this.getName = function(){
      return this.lastName + ' ' + this.firstName;
    }
  };

  // new 演算子で関数を実行するとインスタンスを生成する
  const m = new Member('Doe', 'Jhon');
  console.log(m.fistName) // Doe

  // new 演算子がない関数実行はインスタンスは生成されないので注意
  const m = Member('Doe', 'Jhon');
  ```

- コンストラクタとして宣言した変数が誤って関数実行されないようにするために

   下記のように`instanceof`演算子を使って、強制的にインスタンスを返すようにすることも可能

- ただし、実行の仕方を意識しなくなるのでおすすめしない
  ```javascript
  // 関数内のthisはグローバルオブジェクトを参照する
  // グローバルオブジェクトに`fistName`は宣言されていないので`undefined`となる
  console.log(m.fistName) // undefined

  const Member = function(firstName, lastName) {
    if(!(this instanceof Member)) {
      return new Member(firstName, lastName);
    }
    this.firstName = firstName;
    this.lastName = lastName;
    this.getName = function(){
      return this.lastName + ' ' + this.firstName;
    }
  };
  ```

### 動的にプロパティ・メソッドの追加

- インスタンスに個別にプロパティ・メソッドを追加できる

- Javaのクラスではあとからプロパティやメソッドを追加出来ないが、JSでは可能

   厳密なクラス定義ができないのが、利点であり難点でもある。

  ```JavaScript
  const Member = function(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  };

  const mem = new Member('Doe', 'Jhon');
  // memインスタンスに対して、`getName`メソッドを追加する
  mem.getName = function() {
   return this.lastName + ' ' + this.firstName;
  }
  console.log(mem.getName()); // Jhon Doe

  const mem2 = new Member('bar', 'foo');
  // mem2のインスタンスには`getName`は宣言されていないので実行出来ない
  console.log(mem2.getName()); // is not a function
  ```
## prototypeオブジェクトの宣言

### コンストラクタの問題点

- メソッドの数に比例して、コンストラクタが生成されるたびにメモリを消費する

- 同じ処理をするのにいくつもメソッドがある必要は無い

- prototypeオブジェクトにメソッドを宣言する

  ```javascript
  const Member = function(firstName, lastName) {
    this.firstName = firstName;
    this.lastName = lastName;
  };

  // prototypeというプロパティにオブジェクトリテラルでメソッドを宣言する
  Member.prototype = {
    getName : function() {
      return this.lastName + ' ' + this.firstName;
    },
    toString : function() {
      return this.lastName + this.firstName;
    }
  };

  const mem = new Member('Doe', 'Jhon');
  console.log(mem.getName());
  console.log(mem.toString());

  const mem2 = new Member('foo', 'bar');
  // toStringメソッドを再定義(オーバーライド)する
  mem2.toString = function() {
      return this.lastName + ' ' + this.firstName;
  }

  console.log(mem2.getName());
  // mem.toStringと振る舞いが異なる
  console.log(mem2.toString());
  ```


