# ImageJ Plugin を作るための Java

非情報科学研究者 (特に生物系研究者) が ImageJ plugin を作るために超えるべき壁やTipsをまとめます。  
今回は最低限のJavaについて。  

## 対象者
**画像処理を ImageJ を用いて行なっている人**  
**画像処理手順を自動化したい人**  
**ImageJ macro では満足できず、よりも複雑な処理を施したい人**  
**とにかく ImageJ plugin を書いてみたい人**  

![ImageJで始める生物画像解析](http://images-jp.amazon.com/images/P/B01DY4RS9Y.09.MAIN._SCLZZZZZZZ_.jpg)  

学研メディカル秀潤社から発売されている「ImageJで始める生物画像解析」を読んでみた人、と言い変えても良いかもしれません。  

## はじめに
プログラム言語の経験が無くとも、とにかく小さいものでも良いので作ってみることをオススメします。  

plugin を作るためのプログラム言語は、とにかく Java がオススメです。他の言語でも書けますが、まずは騙されたと思って Java から始めましょう。  

ImageJ Plugin を作るための Java なので、最低限下記を習得すれば充分ということにします。  

- 型
- 変数
- for文
- if文

とにかく一刻も早く Java を乗り超えて、plugin 作成に取り組みましょう。

## 型
後述する変数の性質を決めているのが型です。  
2つだけ覚えましょう。 **int型** と **double型**。  
もっと沢山あるよ! という技術者の言葉に惑わされてはいけません。  
 
**int型**: 整数を扱う時に使います。1 とか 2 とか。    
**double型**: 浮動小数点数を扱う時に使います。 0.5 とか 42.195とかですね。    

## 変数

実際にプログラム上に書く時は、型と変数をセットで記述します。まずは下記のコードを眺めてみましょう。   

```java
int hoge = 42;
//doule foo = 2.5;
```

たった2行のコードですが、結構大事なことがつまっています。  
**冒頭に型**を書いて、**次に変数**を書きます。  
1行目の場合、型名が int型、変数名が hoge ですね。  
次に、= (イコール) で繋げて 42 を書いてますが、これは int型の変数 hoge に 42 を代入しています。  

### = (イコール) なのに代入って...?  
算数とか数学では イコールって等しいって意味でしたね。プログラミングの世界だと、右辺を左辺に代入する、って意味になります。  
R言語だと、下記みたいに書けます。  

```java
hoge <- 42
```

何となく、代入してるっぽい表現ですね。  
プログラミングを習得していない生物学にとって、イコールなのに代入とは...? って疑問はもっともです。気持ちはわかりますが、何とか受け入れて欲しいです。  

### じゃあ、hoge って何?  
こちらもよくある疑問ですね。  
変数名なんですが、型名と違って変数名は自分で好きな単語にできます。  

```java
int suuji = 42;
int test = 114514;
int a = 683298;
```

suuji でも test でも a でも、お好きな文字列で構いません。  
でも、何でも好きにして良いって言われると逆に何を選んで良いか迷ってしまいますね?  
そんな時に便利な、意味の無い文字列が hoge だったり foo だったりします。名前の記入例にある太郎君とか、花子さんとか、そういうニュアンスです。    

### 42ってたまに見るけど何?  
「人生、宇宙、全ての答え」です。生物系研究にとっては驚きかもしれませんが、一部の技術者にとって「人生、宇宙、全ての答えは42」なのです。Java本などで何の説明もなくこのフレーズが使われたりしますが、驚かないで欲しいです。  

### 文末の ; (セミコロン) って何?  
文末に書く、謎の記号です。日本語の「。」だと思って受け入れて欲しいです。  

### //って何?    
コメントアウトです。冒頭に // と書けば、その行は無視されます。  

## for文
繰り返して処理するためのコードです。基本形は以下の形。  

```java
for (int i = 0; i < 10; i++) {
	IJ.log("count: " + i);
}
```

i は変数。suuji でも test でも良いですね。  
慣習的に i が良く使われています。  

### {}が出てきたけど何?    
{} で囲った所をくり返します。上の場合は、i が 0 から 9 までの合計 10 回、ログ出力をくり返します。  

### IJ.log...?  

```java
IJ.log("count: " + i);
```

これはImageJで使えるログ出力用のコードです。意外に便利で良く使います。  
何気に大事なのは、文字は "" でくくる、とうことでしょうか。  

for文は2重にもできます。  

```java
for (int y = 0; y < 10; y++) {
	for (int x = 0; x < 10; x++) {
		IJ.log(coordinate: (" + x + ", " + y + ")");
	}
}
```

何なら3重にもできます。  
画像処理をしていると、x座標とy座標を2重のfor文で呼び出すこの構文を良く使うかもしれません。  



## if文
条件分岐ができます。  

```java
int width = 100;
int height = 100;

if (width == height) {
	IJ.log("quadrate");
} else {
	IJ.log("rectangle");
} 
```

for文と似てますね。if () 内に条件を書いて、それが正しかったら {} 内を実行します。正しくない場合は else {} 内を実行します。  
else は省略可能です。  

イコールを2つ重ねる (==) が、数学的な意味のイコールです。  
上記コードの場合は、width と height を評価して、同じ値であれば quadrate (正方形) を表示、違い場合は rectangle (長方形) と表示しています。  

## まとめ
最低限、「型」・「変数」・「for文」・「if文」をクリアすれば ImageJ plugin は書けてしまいます。生物学者が自分のために ImageJ plugin を書く場合は、Javaの習得はそこそこにして、早速 plugin を作ってしまう方が長い目で見ると良いのではないでしょうか。  

次回は早速、plugin 作成に取りかかりましょう。  

