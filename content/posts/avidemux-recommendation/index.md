
+++
date = "2020-12-01 14:02:55 +0000 UTC"
draft = false
title = "フリー動画編集ソフト avidemux のすゝめ"
categories = ["software"]
tags = ["avidemux"]

+++
Davinci Resolve とか Aviutl とか、フリーでも高機能な動画編集ソフトはあるけど、メインの動画投稿先が Twitter の人にとってはそんなすごいのはいらない感がある。 (くだらん動画のためにいちいちプロジェクト作成するとか面倒臭すぎる)

劣化ほぼなしで動画のトリミングと結合だけできれば満足なんですが、意外とそういうのがなかったのでご紹介。

ちなみに今までは Microsoft Photo のトリミング機能 -> Free video joiner でやってたけど、 60fps の動画がトリミング後に低フレームレートになったり、劣化がひどいのでダメ。

## インストール

[Avidemux - Downloads](http://avidemux.sourceforge.net/download.html)

ここから自分の環境にあったものをインストール。

### 設定項目

言うてほとんどないですが、強いて言えば僕は mp4 の動画しか編集しないので

![](image1.png)

<table>
<thead>
<tr>
<th> hoge </th>
<th> huga </th>
</tr>
</thead>
<tbody>
<tr>
<td> Video Output </td>
<td> Copy </td>
</tr>
<tr>
<td> Audio Output </td>
<td> Copy </td>
</tr>
<tr>
<td>Output Format </td>
<td> MP4 Muxer </td>
</tr>
</tbody>
</table>


に設定して、 Edit > Save current setting as default をクリック。終わり。

Video Output でコーデックを指定すればまあまあ凝った編集はできるみたい。

## 編集

![](image2.png)

インターフェースはこんな感じで、下のボタンとスライダーくらいしか使うものはなし。

ポチポチ触ってればだいたい分かるけど、トリミングに使う機能だけ紹介すると、

<ul>
<li><span style="color: #d32f2f">A</span> -> Delete key: ここから消す</li>
<li>B -> Delete key: ここまで消す</li>
<li><span style="color: #d32f2f">A</span> -> B Delete key: ここからここまで消す</li>
</ul>


みたいな感じ。

後ろに新しい動画をつなげたいときは、 File -> Append で動画を選択。

解像度が違う動画同士は基本繋げられないけど、なんとかする方法はあるっぽい (自分は使わないので割愛)。

<iframe width="480" height="270" src="https://www.youtube.com/embed/orxUZGD75Dk?feature=oembed" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen=""></iframe><cite class="hatena-citation"><a href="https://youtu.be/orxUZGD75Dk">youtu.be</a></cite>

編集が終わったら Ctrl - S で保存。終わり!

サクッと編集してサクッと上げたい人におすすめの編集ソフトです。


