# labデータを用いた口パクのやり方

## 概要

labファイルを用いた口パクを行います。

## labファイルとは

labファイルとは音素のタイミングを記録したファイルです。
VOICEVOXやCeVIOなどの音声合成ソフトが出力可能です。
音素のタイミングに合わせて口パクを行うことで、対応した口を表示させることができます。

## 利用方法

### 素材の準備

- 好みのキャラクターの画像を用意します。
- PhotoshopやPSDToolなどを用いて、「あ」、「い」、「う」、「え」「お」「ん」の口だけの画像を用意してください。

## After Effectsでの設定

- After Effectsを起動します。
- 新規コンポジションを作成します。
- 画像を配置します。
- テキストレイヤーを作成します。
- テキストレイヤーの名前を「lab」とします。
- テキストレイヤーをもう一つ作成します
- テキストレイヤーの名前を「oto」とします。
- oto レイヤーをクリックして、**テキスト**、**ソーステキスト**を右クリックして**エクスプレッションの編集**
  をクリックします。エクスプレッションが入力できるようになります。以下のコードを貼り付けます。

```Javascript
const lab_data = thisComp.layer("lab").text.sourceText.toString()
const labs = lab_data.trim().split(/\s+/)
const tickTime = time * 1000 * 1000 * 10

// binary search
function binary_search() {
	let index = -1
	let left = 0
	let right = Math.floor(labs.length / 3)
	let middle
	
	while (left <= right) {
		middle = Math.floor((left + right)/2) 
		if ( Number(labs[middle * 3 + 0]) <= tickTime && tickTime < Number(labs[middle * 3 + 1])) {
			index = middle;
			break;
		} else if ( Number(labs[middle * 3 + 1]) < tickTime ) { 
			left = middle + 1
		} else {
			right = middle - 1
		}
	}
	return index
} 

const timelineIndex = binary_search()
if (timelineIndex != -1) {
	text.sourceText = labs[timelineIndex * 3 + 2]
} else {
	text.sourceText = "";
} 
```

- 「あ」の口の**トランスフォーム**->**不透明度**を右クリックして**エクスプレッションを編集**をクリックします。
- 以下のコードを貼り付けます。

```Javascript
const oto = thisComp.layer("oto").text.sourceText.toString()

if (oto == "a") {
	transform.opacity = 100
} else {
	transform.opacity = 0
}
```

- 「い」の口の**トランスフォーム**->**不透明度**を右クリックして**エクスプレッションを編集**をクリックします。
- 以下のコードを貼り付けます。

```Javascript
const oto = thisComp.layer("oto").text.sourceText.toString()

if (oto == "i") {
    transform.opacity = 100
} else {
    transform.opacity = 0
}
```

- 「う」の口の**トランスフォーム**->**不透明度**を右クリックして**エクスプレッションを編集**をクリックします。
- 以下のコードを貼り付けます。

```Javascript
const oto = thisComp.layer("oto").text.sourceText.toString()

if (oto == "u") {
    transform.opacity = 100
} else {
    transform.opacity = 0
}
```

- 「え」の口の**トランスフォーム**->**不透明度**を右クリックして**エクスプレッションを編集**をクリックします。
- 以下のコードを貼り付けます。

```Javascript
const oto = thisComp.layer("oto").text.sourceText.toString()

if (oto == "e") {
    transform.opacity = 100
} else {
    transform.opacity = 0
}
```

- 「お」の口の**トランスフォーム**->**不透明度**を右クリックして**エクスプレッションを編集**をクリックします。
- 以下のコードを貼り付けます。

```Javascript
const oto = thisComp.layer("oto").text.sourceText.toString()

if (oto == "o") {
    transform.opacity = 100
} else {
    transform.opacity = 0
}
```

- 「ん」の口の**トランスフォーム**->**不透明度**を右クリックして**エクスプレッションを編集**をクリックします。
- 以下のコードを貼り付けます。

```Javascript
const oto = thisComp.layer("oto").text.sourceText.toString()
const reg = /^[aiueo]$/
if (!reg.test(oto)) {
	transform.opacity = 100
} else {
	transform.opacity = 0
}
```

- labレイヤーとotoレイヤーの左端の目をクリックして、非表示にします。
- labレイヤーをクリックして、**テキスト**、**ソーステキスト**を右クリックして**プロパティをエッセンシャルグラフィックに追加**をクリックします。
- エッセンシャルグラフィックの**ソーステキスト**をクリックして**lab**に書き換えます。
- モーショングラフィックテンプレートを書き出しをクリックして、保存します。

### Nijikanツールの設定

- Premiere ProのNijikanのウィンドウを開きます。
- **キャラクター設定**をクリックします。
- 設定したキャラクターをクリックします。
- メニュー下部にある口パクMOGRTのフォルダアイコンをクリックします。
- 先ほど書き出したモーショングラフィックテンプレートを選択します。
- **キャラクター設定**を閉じます。

## そのほかの口パク方法

### Adobe Character Animatorを用いた口パク

Adobe Character Animatorを用いると、音声に合わせて口パクを行うことができます。


