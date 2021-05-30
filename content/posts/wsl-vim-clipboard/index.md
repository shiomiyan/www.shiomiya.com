---
title: WSL の Vim で Windows とのクリップボードを共有する
date: 2021-05-31T00:40:44+09:00
description:
draft: false
author: shiomiya
categories: tech
tags:
  - wsl
  - vim

---

Xserver を使う方法はたくさんあったのですが、なるべく余計なものは入れたくないので。

## WSL の Vim のバージョンを確認

{{< blogcard "https://sy-base.com/myrobotics/vim/vim_use_clipboard/" >}}

こちらを参考にしました。 `vim --version | grep clip` で `+clipboard` を確認できなかった場合は、まず WSL の Vim をアンインストールします。

```
sudo apt remove vim
```

自分の環境では vim-gnome が入らなかったので、vim-gtk を入れて対応します。

```
sudo apt install vim-gtk
```

最後に、以下のように `+clipboard` を確認できれば準備は完了です。

```
❯ vim --version | grep clip
+clipboard         +keymap            +printer           +vertsplit
+emacs_tags        +mouse_gpm         -sun_workshop      +xterm_clipboard
```

## vimrc に yank 用の keymap を入れる

ここまででペーストは可能なのですが、yank ができませんでした。地味に不便なので yank もできるようにします。

そのために vimrc を編集するのですが、dotfiles で管理している手前他の環境に影響が出ると困るので、WSL 環境でのみ keymap を読み込むよう以下のように記載します。

```vim
" === WSL setting ===
if stridx(system('uname -r'), 'microsoft')
  augroup Yank
    au!
    autocmd TextYankPost * :call system('clip.exe', @")
  augroup END
endif
```

{{< blogcard "https://zenn.dev/zakuro9715/articles/wsl-vim-clipboard" >}}

綺麗にまとまっているので、こちらを参考にさせていただきました。

WSL でも tmux 使いたいですが、一旦我慢してこれで運用します。