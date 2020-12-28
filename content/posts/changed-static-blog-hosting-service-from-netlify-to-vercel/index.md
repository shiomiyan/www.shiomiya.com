---
title: 静的ブログのホスティングサービスを Netlify から Vercel に乗り換えた
date: 2020-12-28T20:13:01+09:00
description:
draft: true
author: shiomiya
categories: tech
tags:
  - netlify
  - vercel
  - hugo

---

静的ブログのホスティングにこれまで Netlify を使ってきたが、静的ブログなのに読み込みがオッソい。日本からだとキャッシュサーバーがシンガポールらしいのでまぁそうだよねって感じ。

Lighthouse の評価でもサーバーのレイテンシが高いぞって言われてたのでなんとかしたいなって思ってました。

日本鯖のホスティングサービスないかな ~ ってなっていたところで、以下の記事を見つけた。

> [VercelとNetlifyの違いが分からなかったので実際に比べてみた。 - Qiita](https://qiita.com/fussy113/items/ba204747e3f0e6c59af0)

で、調べてみたらどうやら[東京サーバーがあるらしい](https://vercel.com/docs/edge-network/regions)ので、移行してみることにした。

## 移行

基本ほとんど Netlify と同じ。

デプロイしたら独自ドメインの設定を書き換えて終了。ものの 15 分。

## 応答時間

Firefox の devtool でロード時間を計測してみる。

### Netlify

- 初回読み込み: 1642 ms
- 2 回目以降: 270 ~ 300 ms

### Vercel

- 初回読み込み: 874 ms
- 2 回目以降: 90 ~ 100 ms

## おわりに

読み込み時間も 1/2 から 1/3 くらい短縮され、不満を解消できたようで大満足。
