# 第3回議事録

## 3.1 再帰関数

+ 「再帰」とは自分自身を呼び出すという意味。
+ 階乗のように「扱う値が徐々に少なくなり」「同じような処理を繰り返す」際に用いられる。
+ 必ず終了条件を記述しなくてはならない.

### 再帰関数の例
```JavaScript
/** 引数にnを持つ関数を定義する */
function saiki(n) {
    if (n != 0) {
        return n * saiki(n - 1); //ここでもsaiki関数を呼び出す.
    }
    return 1; //nが0になったら1を返す.(本関数の終了条件)
}

console.log(saiki(5)); //5*4*3*2*1の結果が出力される.
```
## 3.2 高階関数

+ 関数を引数に渡したり、戻り値とする関数のこと。

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
