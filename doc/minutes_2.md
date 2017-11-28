#### 第２回議事録!!!

## 引数 (chapter4.4)

1. JavaScriptは引数の数をチェックしない

    → 設定されている引数以上の数の引数を関数へ渡しても、切り捨てられる訳ではなく、argumentsオブジェクトにしまわれる

```JavaScript
function showMessage(value){
	console.log(value);
}

showMessage();        //①結果 undefind
showMessage('hoge'); //②結果 hoge
showMessage('hoge','fuga','piyo');//③結果 hoge
```

②のargumentオブジェクト：{ '0': 'hoge' }

③のargumentオブジェクト：{ '0': 'hoge', '1': 'fuga', '2': 'piyo' }

* 引数の数をチェックしないので、JavaScriptでは全ての引数は省略可能

    → 省略してしまうと正しく動かなくなってしまうので、デフォルト値を決めておくと良い

```JavaScript
function getTriangle(base , height){
	if(base === undefined){ base = 1;} // baseのデフォルト値：1
	if(height === undefined){ height = 1;} // baseのデフォルト値：1
	return base * height / 2;
}

console.log(getTriangle(5)); // 結果 2.5

```

2. argumentオブジェクトには、可変長引数の関数という役割もある

```JavaScript
function sum(){
	var result = 0;

	//与えられた引数を順番に取り出し、順に加算処理
	for( var i = 0, len = arguments.length ; i < len ; i++ ){
		var tmp = arguments[i];
		result += tmp;
	}
	return result;
}

console.log(sum(1,3,5,7,9)); // 結果：25

```

3. 明示的に宣言された引数と可変長引数を混在させることもできる。

* ただし、argumentsオブジェクトの中に、明示的に宣言された引数もしまわれちゃうので注意！

    可変長引数にも仮の名前をつけるとわかりやすい。(そもそも、混在させることはあまりなさそう...)

```JavaScript
function printf(format, var_args){} // 例
```

4. function呼び出し時に引数の名前を明示的に指定することができる。(名前つき引数)

* 名前つき引数のメリット

  + 引数が多くなってもコードの意味がわかりやすい！
  + 省略可能な引数をスマートに表現できる！
  + 引数の順番を自由に変更できる！

```JavaScript
function getTriangle(args){ // 引数argsに、オブジェクト{ base:5 , height:4}が入る
	return args.base * args.height / 2;
}

console.log(getTriangle({ base:5 , height:4}); // 結果：10
```

#### 完
