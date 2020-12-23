---
title: "パスワードマネージャーを 1password から Bitwarden に乗り換えた"
date: "2020-12-21T15:47:10+09:00"
description: ""
draft: false
author: "shiomiya"
categories: ["random"]
tags: ["1password","bitwarden"]
---

3 年間使い続けた 1password を解約して Bitwarden に乗り換えた。

## 動機

1password をしばらく使い続けてきたが、最近 PC のツール周りをまた試行錯誤し始めていていい機会なのでパスワードマネージャーも乗り換えることにした。

もともと、1password に不満がなかったわけでもなく、以下の点においてやや不満があった。

- Auto-Fill 機能がトロい(PC、スマホ両方)
- 1password7 に関しては Windows クライアントもややレスポンスが悪い
- Linux では 1passwordX の利用が必須
  - OS 間で体験が結構違っている
- コストが高い ($39/年)
- 新しいデバイスでのログインが面倒 (セキュアなのはわかるけど)

という感じで、移行を決意した。

## 移行

### 1Password

Bitwarden 側でサポートしているようなので `.1pif` でエクスポートした。

アカウント管理からサブスクリプションを解除して終わり。ありがとう ﾜﾝﾊﾟｽ 。

### Bitwarden

アカウントは作成済みだったので、一旦保管庫を削除してからインポートした。ワンクリックで問題なくインポートは完了。超楽ちん。

アカウントごとの 2 Factor Authentication には今まで 1password を使っていたので、これからは Bitwarden 君に担ってもらうためプレミアムを契約した。年間 $10 なのでこれまでの 1/4 である。これの移行作業が面倒かと思ってたけどよしなにしてくれたようで良かった。

ブラウザ拡張と OS ごとのクライアントも入れておいた。またメールアドレス・パスワードの流出検知には [Firefox Monitor](https://monitor.firefox.com) を使うことにした。

パスワードの総数自体もそこまで大量ではないので、ざっと目を通して使っていないサービスからアカウントを削除したり、最近用途に応じてメールアドレスを使い分け始めたので登録メールアドレスを変更したりした。

## おわりに

パスワードマネージャーを使い始めてはや 3 ~ 4 年といったところですが、未だに再利用が多くあってなかなか重い腰が上がらない現状ではある。

実は去年あたりに一度移行を考えて短期間使っていた時期があったのだが、 UI とスマホ側での挙動がイマイチだったことを理由に結局乗り換えなかった。

一応書いておくとすでに 1password に劣っていると感じる点はあって、再利用されたパスワードを検出したり、クレカの有効期限が迫っていることを教えてくれたりする機能は Bitwarden にはない。

1 年越しにまた触った感じかなりレスポンスも良くなっていて今後の成長にも期待できそうなので、近いうちにそこらへんも実装してほしい。