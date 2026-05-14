# confetti-es

[
![ISC License](https://img.shields.io/badge/license-ISC-blue.svg)
](LICENSE)

canvas上で華やかでカスタマイズ可能な紙吹雪（コンフェッティ）エフェクトを作成するための軽量なESモジュールです。

## デモ

- [**Basic Cannon**](https://code4fukui.github.io/confetti-es/demo/BasicCannon.html) - 中央から単発で打ち上がる紙吹雪。
- [**Fireworks**](https://code4fukui.github.io/confetti-es/demo/Fireworks.html) - 画面上部からランダムに連続して打ち上がる花火のようなエフェクト。
- [**School Pride**](https://code4fukui.github.io/confetti-es/demo/SchoolPride.html) - 画面の両端から絶え間なく降り注ぐ紙吹雪。
- [**Level Up**](https://code4fukui.github.io/confetti-es/demo/LevelUp.html) - 画面下部の両隅からの祝福のクラッカーに続き、星型の紙吹雪が弾けるエフェクト。（[chiritsumo](https://github.com/haruyuki-16278/chiritsumo) より）

## 特徴

- **モダンJavaScript**: 依存関係のない標準的なESモジュールとして提供されます。
- **高いカスタマイズ性**: パーティクルの数、色、形状（`square`、`circle`、`star`）、広がり、速度、重力などを制御できます。
- **柔軟なターゲット指定**: ビューポート全体、または特定の `<canvas>` 要素内に紙吹雪を描画できます。
- **アクセシビリティ対応**: `prefers-reduced-motion` メディアクエリを自動的に尊重し、アニメーションの軽減を必要とするユーザーに対してはアニメーションを無効にします。

## 使い方

CDNから直接 `confetti` 関数をインポートして呼び出します。

```javascript
import { confetti } from "https://code4fukui.github.io/confetti-es/confetti.js";

// シンプルな打ち上げ
confetti();

// または、カスタムオプションを使ってクリエイティブに
confetti({
  particleCount: 150,
  spread: 180,
  origin: { y: 0.6 }
});
```

以下は、画面の両端から2筋の紙吹雪を打ち上げる、より高度な例です。

```javascript
// 左から打ち上げ
confetti({
  particleCount: 100,
  angle: 60,
  spread: 55,
  origin: { x: 0 }
});

// 右から打ち上げ
confetti({
  particleCount: 100,
  angle: 120,
  spread: 55,
  origin: { x: 1 }
});
```

## API

### `confetti([options])` → `Promise|null`

紙吹雪のアニメーションをトリガーします。アニメーションの完了時に解決される `Promise` を返します。Promiseがサポートされていない場合は `null` を返します。

`options` オブジェクトを使用してエフェクトをカスタマイズできます。すべてのプロパティは省略可能です。

| オプション                  | 型                 | デフォルト                            | 説明                                                                                                    |
| --------------------------- | ------------------ | ------------------------------------- | ------------------------------------------------------------------------------------------------------- |
| `particleCount`             | `Integer`          | `50`                                  | 打ち上げる紙吹雪のパーティクル数。                                                                      |
| `angle`                     | `Number`           | `90`                                  | 打ち上げ角度（度）。`0` は右、`90` は真上。                                                             |
| `spread`                    | `Number`           | `45`                                  | `angle` から紙吹雪が広がる範囲（度）。                                                                  |
| `startVelocity`             | `Number`           | `45`                                  | 紙吹雪のパーティクルの初期速度（ピクセル）。                                                            |
| `decay`                     | `Number`           | `0.9`                                 | 紙吹雪が減速する速さ。`1` は減速なし。                                                                  |
| `gravity`                   | `Number`           | `1`                                   | パーティクルが下に引っ張られる速さ。`0` は重力なし。                                                    |
| `drift`                     | `Number`           | `0`                                   | 紙吹雪が横に流れる量。`0` は直進、負の値は左、正の値は右。                                              |
| `ticks`                     | `Number`           | `200`                                 | 各パーティクルのアニメーションフレーム数。                                                              |
| `origin`                    | `Object`           | `{ x: 0.5, y: 0.5 }`                  | 打ち上げの起点。`x` と `y` は `0` から `1` の値で、キャンバスのパーセンテージを表します。               |
| `colors`                    | `Array<String>`    | `['#26ccff', ...]`                    | 紙吹雪に使用するHEXカラー文字列の配列。                                                                 |
| `shapes`                    | `Array<String>`    | `['square', 'circle']`                | 形状名の配列。利用可能な形状: `'square'`、`'circle'`、`'star'`。                                        |
| `scalar`                    | `Number`           | `1`                                   | 各紙吹雪のパーティクルのスケール係数。                                                                  |
| `zIndex`                    | `Integer`          | `100`                                 | 紙吹雪を描画するキャンバスの `z-index`。                                                                |
| `disableForReducedMotion`   | `Boolean`          | `false`                               | `true` の場合、ユーザーが視差効果を減らす設定（reduced motion）を有効にしていると紙吹雪を無効にします。 |

### `confetti.create(canvas, [globalOptions])` → `function`

ビューポート全体ではなく、特定の `<canvas>` 要素に描画する新しい `confetti` インスタンスを作成します。

```javascript
import { confetti } from "https://code4fukui.github.io/confetti-es/confetti.js";

const myCanvas = document.getElementById('my-canvas');

// カスタムの紙吹雪インスタンスを作成
const myConfetti = confetti.create(myCanvas);

// グローバルの confetti 関数と同じように使用
myConfetti({
  particleCount: 200,
  spread: 80
});
```

このインスタンスで行われるすべての呼び出しに適用される `globalOptions` を指定することもできます。

## ライセンス

ISC License
