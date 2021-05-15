---
title: obsidian.md の エディタ部分のフォントを変更する
date: 2021-05-15T19:43:08+09:00
description:
draft: false
author: shiomiya
categories: tech
tags:
  - obsidian

---

{{< blogcard "https://obsidian.md/" >}}

これについて。カスタム CSS でフォントを変更するのがややわかりにくかったのでメモ。

## カスタム CSS を有効にする

Settings > Appearance > CSS snippets からフォルダアイコンを押して Snippets フォルダを開く。

`**.css` ファイルを作成。

フォルダアイコンの左の更新ボタンで更新すると設定項目が増えてるので有効にする。

## CSS

```css
.theme-dark {
    --font-monospace: 'Consolas NF', 'Yu Gothic';
}

body {
    font-family: 'Consolas NF';
}
```

`.theme-dark` の `--font-monospace` が等幅のフォントで、 `body` の `font-family` はファイルツリーや設定項目等のフォント。

ライトテーマなら `.theme-light` に書けば良さそう。