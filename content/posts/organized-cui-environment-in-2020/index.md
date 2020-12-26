---
title: 2021 年に向けて CUI 環境を整理した
date: 2020-12-26T17:21:25+09:00
description:
draft: true
author: shiomiya
categories: 
tags:
  - 
  -

---

2020 年も終わりそうなので Vim や Shell 周りの開発環境を断捨離したのでその記録。

## Vim

### .vimrc

これまで言語ごとのインデントは全部手動で以下のように設定していた。

```viml
augroup fileTypeIndent
  autocmd!
  autocmd BufNewFile,BufRead *.c setlocal tabstop=4 shiftwidth=4
  autocmd BufNewFile,BufRead *.cpp setlocal tabstop=4 shiftwidth=4
  autocmd BufNewFile,BufRead *.py setlocal tabstop=4 shiftwidth=4
  autocmd BufNewFile,BufRead *.rs setlocal tabstop=4 shiftwidth=4
  autocmd BufNewFile,BufRead *.java setlocal tabstop=4 shiftwidth=4
  autocmd BufNewFile,BufRead *.elm setlocal tabstop=4 shiftwidth=4
  ...
augroup END
```

このままだと永遠に増え続けそうだったのでプラグインを導入した ([sheerun/vim-polyglot](https://github.com/sheerun/vim-polyglot)) 。

### プラグイン

プラグインマネージャーは導入が楽なので vim-plug を継続して使う。

```diff
- Plug 'tomasr/molokai' " theme
- Plug 'micha/vim-colors-solarized' "theme
- Plug 'morhetz/gruvbox' " theme
+ Plug 'arcticicestudio/nord-vim' " theme
Plug 'airblade/vim-gitgutter'
Plug 'sheerun/vim-polyglot'
Plug 'cohama/lexima.vim'
Plug 'rust-lang/rust.vim'
Plug 'racer-rust/vim-racer'
- Plug 'ElmCast/elm-vim'
- Plug 'mattn/sonictemplate-vim'
Plug 'wakatime/vim-wakatime'
Plug 'hugolgst/vimsence'
Plug 'itchyny/lightline.vim'
- Plug 'yuttie/comfortable-motion.vim'
- Plug 'justinmk/vim-dirvish'
- Plug 'prabirshrestha/async.vim'
Plug 'prabirshrestha/vim-lsp'
+ Plug 'mattn/vim-lsp-settings'
Plug 'prabirshrestha/asyncomplete.vim'
Plug 'prabirshrestha/asyncomplete-lsp.vim'
- Plug 'ryanolsonx/vim-lsp-javascript'
- Plug 'ryanolsonx/vim-lsp-python'
- Plug 'ryanolsonx/vim-lsp-typescript'
Plug 'w0rp/ale'
- Plug 'ianding1/leetcode.vim'
- Plug 'mattn/emmet-vim'
```

もともとあまりプラグインが入っていなかったけど更に減らした。

`vim-lsp-**` を LSP を使うために導入していたが、 [mattn/vim-lsp-settings](https://github.com/mattn/vim-lsp-settings) を導入して超すっきりした (そのために [`lspconf.vim`](https://github.com/shiomiyan/.dotfiles/blob/master/.vim/userautoload/lspconf.vim) を作って `.vimrc` の肥大化を抑えていたがこれも要らなくなった) 。

ファイラはシンプルかつ軽量な dirvish を使っていたけど、標準の netrw で十分そうなのでこれも消した。

その他使用頻度の少なかったプラグインを削除した。

ちなみにテーマはお気に入りの gruvbox をやめて気分転換に nord にしてみた。

## Zsh

これと言って大きな変更点はないが macOS と WSL で dotfiles を共有した際に Tmux がいい感じで動いてないので、以下のようにして ディストリビューション別に処理を分けるようにした。

```sh
case "${OSTYPE}" in
  drawin*)
    # macOS
    ;;
  linux*)
    # Linux
    ;;
esac
```

> [.zshrcでOSを判断する – かひわし4v1.memo](https://khws4v1.myhome.cx/article/2015/02/zshrc%E3%81%A7os%E3%82%92%E5%88%A4%E6%96%AD%E3%81%99%E3%82%8B/)

tmux 以外にも分岐させたい処理がいくつかあるので近いうちにもう少しスタイリッシュな感じにしたい。

