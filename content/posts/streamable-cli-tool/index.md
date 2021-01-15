---
title: Streamable へ動画をアップロードする CLI ツール
date: 2021-01-15T02:50:40+09:00
description:
draft: false
author: shiomiya
categories: tech
tags:
  - rust
  - cli

---

[streamable.com](https://streamable.com/) へコマンドラインから動画をアップロードするツールを作った。

[shiomiyan/streamable-uploader - GitHub](https://github.com/shiomiyan/streamable-uploader)

今のところ、以下の機能だけ実装してある。

- setup
- upload

低機能過ぎて需要はなさそうだけど crates.io に上げているので、一応 `cargo install streamable-uploader` でインストールできる。

Windows10 と macOS では動く。

## コマンドライン解析

おなじみの [clap](https://docs.rs/clap/3.0.0-beta.2/clap/) で。

## setup

[rpassword](https://docs.rs/rpassword) を使って Streamable の id/password を受け取ってローカルに保存する。

```rust
pub fn get_username_password() -> (String, String) {
    println!("Please input Your username and password");
    let username = rpassword::read_password_from_tty(Some("Username: ")).unwrap();
    let password = rpassword::read_password_from_tty(Some("Password: ")).unwrap();
    (username, password)
}

pub fn setup() -> Result<()> {
    let env = get_username_password();

    let text = format!(
        "STREAMABLE_USERNAME={}\nSTREAMABLE_PASSWORD={}",
        env.0, env.1
    );

    let home_path = dirs::home_dir().unwrap();
    let config_path = home_path.join(".streamable");
    std::fs::OpenOptions::new()
        .write(true)
        .create(true)
        .open(config_path)
        .expect("can not create config file")
        .write_all(text.as_bytes())
        .unwrap();

    println!(
        "saved your login params in {} as .streamable",
        home_path.to_str().unwrap()
    );
    Ok(())
}
```

~~もともと、 reqwest でログインキャッシュを拾ってローカルに保存しておく予定だった~~

## upload

ベーシック認証して multipart で form を送信する。

```rust
#[derive(Serialize, Deserialize, Debug)]
pub struct UploadResponse {
    pub shortcode: String,
    pub status: i8,
}

pub fn upload(filepath: &str) -> Result<UploadResponse> {
    let home_path = dirs::home_dir().map(|a| a.join(".streamable")).unwrap();

    dotenv::from_path(home_path.as_path()).unwrap();

    let username = env::var("STREAMABLE_USERNAME").unwrap();
    let password = env::var("STREAMABLE_PASSWORD").unwrap();

    let endpoint = "https://api.streamable.com/upload";

    let form = multipart::Form::new()
        .file("file", std::path::Path::new(filepath))
        .unwrap_or_else(|e| panic!("Error: {}", e));

    let client = Client::new();
    let resp = client
        .post(endpoint)
        .basic_auth(username, Some(password))
        .multipart(form)
        .send()
        .unwrap_or_else(|e| panic!("Error: {}", e));

    let response_as_json = resp.json::<UploadResponse>().unwrap();

    Ok(response_as_json)
}
```

Rust でホームディレクトリを参照するとき、標準ライブラリの [`std::env::home_dir`](https://doc.rust-lang.org/std/env/fn.home_dir.html) は非推奨らしいので [dirs](https://docs.rs/dirs/) を使った。

アップロードが完了すると動画へのリンクを教えてくれる。
