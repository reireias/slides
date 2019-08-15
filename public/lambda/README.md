# reveal.js [![Build Status](https://travis-ci.org/reireias/reveal.js.svg?branch=master)](https://travis-ci.org/reireias/reveal.js)

自分用にカスタマイズしたreveal.jsです。

## 変更点
- フォントを`Noto Sans Japanese`に変更
- フォントサイズを変更
- リロード時に同じスライドを表示するように変更
- スライド番号を表示
- スライドめくりのアニメーションを`fade`に変更
- `h1`〜`h6`を`text-transform: none;`に設定
- `live-server`による変更検知と自動更新を設定

## 使用方法
```sh
yarn install
yarn start
```

起動した状態で`body.md`を書き換えると、自動で反映されます。
