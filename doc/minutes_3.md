# 第3回議事録

## 3.1 再帰関数

+ 「再帰」とは自分自身を呼び出すという意味。
+ 関数の中から、その関数自身を呼び出す関数のこと。
+ 必ず終了条件を記述しなくてはならない.終了条件が無いと再帰処理を永遠に繰り返す無限ループが発生する。

### 再帰関数の例
```JavaScript
/** 引数にnを持つ関数を定義する */
function saiki(n) {
    if (n != 0) {
        return n * saiki(n - 1); //ここでもsaiki関数を呼び出す.
    }
    return 1; //nが0になったら1を返す. 再帰処理を実行しない（自身の関数を呼び出さない）ため、処理は終了となる。
}

console.log(saiki(5)); //5*4*3*2*1の結果が出力される.
```
## 3.2 高階関数

+ 関数を引数に渡したり、戻り値とする関数のこと。
+ 関数を引数として扱う関数が「高階関数」

### 高階関数の例
```JavaScript
// 高階関数を定義
function arrayWalk(data, f) {
    for (var key in data) {
        f(key, data[key]);
    }
}

//高階関数に渡すデータ（配列）
var ary = [1, 2, 4, 8, 16];

//高階関数に渡す関数（個別の機能）
function showElem(key, value) {
    console.log(key, ':', +value);
}

//高階関数にデータとコールバック関数を渡して実行
arrayWalk(ary, showElem);
```
```Javascript
// 上記のarrayWalkの具体的な中身
arrayWalk(ary, showElem){
    for(var key in ary){ //var ary = [1, 2, 4, 8, 16];をfor文で回す.
        showElem(key, ary[key]); //for文で取り出した、配列aryの要素をkey: valueの形で表示させる.
    }
}
```
