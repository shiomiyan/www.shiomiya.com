---
title: Alacritty で WSL を使う際の起動ディレクトリを WSL 側のホームディレクトリにする
date: 2021-01-17T11:06:19+09:00
description: Alacritty で WSL を使う際、起動時のディレクトリはショートカットがあるディレクトリ (Windows パス) になってしまう。それを WSL 側のホームディレクトリに変更する方法。
draft: false
author: shiomiya
categories: tech
tags:
  - alacritty
  - wsl

---

Alacritty で WSL を利用する際のメモ。

通常 Alacritty から WSL を使う際には `alacritty.yml` に以下のように設定する。

```yml
shell:
    program: wsl
```

しかしこれにはやや問題があって、このまま Alacritty を起動すると、起動時のディレクトリはショートカットのパスになってしまって、一々 `cd ~` とかする必要があって面倒。

## 解決法

Alacritty のショートカットを作成して、プロパティのターゲットを以下のようにする。

```
"C:\Program Files\Alacritty\alacritty.exe" -e wsl zsh -c "'cd ~ && pwd && zsh -i'"
```

邪道な匂いしかしないので、もっといい方法があれば教えていただきたい。

## 参考

- https://github.com/alacritty/alacritty/issues/3552
