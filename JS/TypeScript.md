## JSとTSの違い
JSは動的型付け言語（Pythonとかと同じ）であるがTSは静的型付け言語である。JSは型宣言しなくてもかけるが、実行するまでエラーとなるかはわからない。  
TSはコンパイルの段階でエラーが出るため、バグなどを未然に防ぎやすい（一応JSでも型定義はできるけど）。
クラスなども使用できるため、コードの量が減る分学習コストは高くなる。  
JSを拡張して作られているため両者に互換性はある。JSさえ理解していれば学習コストはやや下がる

## 型
 - Boolean：true or false
 - Number：浮動小数点。2,8,10,16進数も対応
 - String：文字列。'か"で囲うのはJSと同じ
 - Array：配列。書き方は以下の２通り
```
let list: number[] = [1, 2, 3];
let list: Array<number> = [1, 2, 3];
```
 - Tuple：要素の個数・型が決められた配列
 - Enum：集合の型付け
```
enum Color {Red, Green, Blue};
let c: Color = Color.Green;
```
 - Any：型が不明な時に、宣言するのに使用。
 - Void：型なし。undefinedまたはnullのみ割当可能。
 - Never：決して発生することのない値の型。

## 変数宣言
JSと同じのため省略。letやconstを推奨。このハンドブックにおいてはletを主に使用している。

## インターフェース
値の型チェックが値を持つ形状に焦点を当てている。インターフェースは命名付の規則を満たすもの。

例
```
function printLabel(labelledObj: { label: string }) {
    console.log(labelledObj.label);
}
let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```
これをこう書き直す
```
interface LabelledValue {
    label: string;
}
function printLabel(labelledObj: LabelledValue) {
    console.log(labelledObj.label);
}
let myObj = {size: 10, label: "Size 10 Object"};
printLabel(myObj);
```
使用するのはinterfaceで、書き直す前のものをこれで実行できる。labelプロパティがこの場合は必須となる。

```
interface SquareConfig {
    color?: string;
    width?: number;
}
function createSquare(config: SquareConfig): {color: string; area: number} {
    let newSquare = {color: "white", area: 100};
    if (config.color) {
        newSquare.color = config.color;
    }
    if (config.width) {
        newSquare.area = config.width * config.width;
    }
    return newSquare;
}
let mySquare = createSquare({color: "black"});
```
インターフェースを任意にしたい場合、プロパティの末尾に？をつけることで可能になる。  
任意のプロパティを使うことでインターフェースの一部にないプロパティが使われることや打ち間違いをエラーとして出してくれることがメリット。

```
interface Point {
    readonly x: number;
    readonly y: number;
}
```
読み込みのみにしたい場合、readonlyとつけることで実現できる。
→割り当てたあとに変更することはできない（errorが出力される)






## 参考
https://js.studio-kingdom.com/typescript/
