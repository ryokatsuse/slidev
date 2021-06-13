---
theme: geist
background: https://source.unsplash.com/collection/94734566/1920x1080
class: text-center
highlighter: shiki
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
title: さよならIE
layout: center
---

# さよならIE

　〜IEがない世界線で使えるCSSの紹介〜

2021/06/18




<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

<div class="text-2xl">

<div class="mb-10">

# 自己紹介

</div>

- 🙋‍♂️ 勝瀬 亮(Ryo Katsuse)
- 👉🏼 [@ryo__kts](https://twitter.com/ryo__kts)
- 🏢 YUMEMI Inc.
- 👨🏻‍💻 リードフロントエンドエンジニア
- 🥰 Reactが大好きです！

<div class="relative">
<img
  class="absolute -top-55 -right-0 w-80"
  src="/assets/ryo_k.png"
/>
</div>
</div>

<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->


---
layout: center
---

# 皆さん！朗報です！！

---

# IEサポート終了のお知らせ🎉🎉

- 2022年 6月 15日をもってサポートを終了すると発表！

<div class="flex justify-center">
  <img
    class="w-100"
    src="/assets/ietoedge.png"
  />
</div>

https://blogs.windows.com/windowsexperience/2021/05/19/the-future-of-internet-explorer-on-windows-10-is-in-microsoft-edge/

---
layout: center
---

# 「IE対応」という言葉を聞いて思い浮かぶこと🤔


---
layout: center
---

<div v-click class="absolute top-12 left-30 text-3xl rounded-4xl">つらい</div>
<div v-click class="absolute top-17 right-12 text-3xl rounded-full">なんか分かんないけど崩れてる</div>
<div v-click class="absolute top-30 left-80 text-3xl rounded-full">やりたくない</div>
<div v-click class="absolute top-50 right-20 text-3xl rounded-full">大量のBabelポリフィル</div>
<div v-click class="absolute top-60 left-50 text-3xl rounded-full">レガシー</div>
<div v-click class="absolute bottom-12 right-30 text-3xl rounded-full">動作確認したくない</div>
<div v-click class="absolute bottom-30 left-20 text-3xl rounded-full">Chromeだと崩れてないのに何故。。。</div>


<h1 v-click class="text-8xl">😵</h1>




---

# IEとの戦い

- 😇 サポートされていないCSSに対してベンダープレフィックスを付けてた(```ms-*```)
- 🤕 IEの特定のバージョンだけに適用したCSSのメディアクエリを追加していた。

```css

.hoge {
  display: flex;
}

@media all and (-ms-high-contrast:none){
  *::-ms-backdrop, .hoge { display: block } /* IE11のみに適用されたCSS */
}

```

- 😭 過去には条件付きコメントなんてものもあった・・・

```html
<!-- IE9にしか適用されないCSS -->
<!--[if IE 9]>
<link rel="stylesheet" href="xxx.css" />
<![endif]-->

```

<style>

pre {
  border: none;
}

</style>

---
layout: center
---
# 今日紹介するCSSたち

---

<div class="text-xl">

# IEがない世界線で使えるCSS

- flex-gap
- filter
- aspect-ratio
- clip-path
- position-sticky
- line-clamp

### 他にも沢山ありますが、すぐに現場で使えそうなCSSを紹介します！

</div>


---
layout: default
---

# flex-gap

- 

<div grid="~ cols-2 gap-4">

<div>

- 🎊 行、列の余白を定義できる
- 🎁 カラムレイアウトの余白を簡単に実装できる！
- 👇👇 デモします！
- https://codepen.io/ryokatsuse/pen/eYvPNRx


</div>

<div>

- サンプルコード

```css
.img{
  display: flex;
  gap: 30px;
}
```
</div>

</div>


<style>

pre {
  border: none;
}

</style>

---
layout: default
---

# filter


<div grid="~ cols-2 gap-4">

<div>

- 😻 要素に様々な効果を加えることができる
- 😼 ぼかし、彩度、明度の変更などが可能！

- 👇👇 サンプルコード
- https://codepen.io/ryokatsuse/pen/poexPYG


</div>

<div>
<video class="-top-4 relative" src="/assets/filter.mp4" controls autoplay></video>
</div>


</div>


---
layout: default
---
# aspect-ratio

<div grid="~ cols-2 gap-4">

<div>

- アスペクト比を明示的に書くことで要素を表示できます。
- Safariでは15から対応します。
- レイアウトシフト（ガタツキ）を防ぐことができます。

#### 従来のアスペクト比計算方法

| アスペクト比 | 計算                |
| ------------ | ------------------- |
| 16:9         | 9/16 * 100 = 56.25% |
| 4:3          | 3/4 * 100 = 75%     |
| 3:2          | 2/3 * 100 = 66.67%  |
| 2:1          | 1/2 * 100 = 50%     |

</div>

<div>

<video src="https://storage.googleapis.com/web-dev-assets/aspect-ratio/gridimages2.mp4" controls autoplay></video>

参考：https://web.dev/aspect-ratio/

</div>

</div>

---
layout: default
---

# サンプルコード

- 以下のようなHTMLを想定

```html
<div class="aspect-ratio-block"></div>
```

<div grid="~ cols-2 gap-4">
<div>

- IE時代

```css
.aspect-ratio-block {
  position: relative;
  background: #999;
  width: 50%;
}

.aspect-ratio-block::before {
  content:"";
  display: block;
  padding-top: 56.25%; /* 16:9のアスペクト比を計算した値を書く */
}
```
</div>

<div>

- モダンブラウザ時代

```css
.aspect-ratio-block{
  width: 100%;
  aspect-ratio: 16 / 9;　/* 明示的に書ける！ */
}
```

</div>


</div>

<style>

pre {
  border: none;
}

</style>

---

# iframeでも使えます。

- Google Mapの埋め込みなどをいい感じにレイアウトできます。
- サンプルコード
- https://codepen.io/ryokatsuse/pen/mdWQmmV

---
layout: default
---
# clip-path

- 要素をクリッピング（切り抜き）ができる！
- PhotoshopとかでやっていたことがCSSで表現できる！
- このジェネレータで色々試すことができます！


https://bennettfeely.com/clippy/


---
layout: default
---
# 図形どうやって作ってた？？


- clip-pathで実装しない場合はborder,width,heightなどを駆使して頑張って作っていた。
- そのためCSSの記述量も増えがちだった。。。

- 例）三角形の作り方

```css
.triangle {
  width: 0;
  height: 0;
  border-left: 20px solid transparent;
  border-right: 20px solid transparent;
  border-bottom: 40px solid #dd0000;
}

```

参照: [[CSS]CSS で円形、三角形、台形、星形 などを表現する方法のまとめ](https://www.webantena.net/css/css3-circle-ttriangle-trapezoid-star/)

---
layout: default
---


# position-sticky

- 

---


# line-clamp

- 

---
# まとめ
- IE対応は辛い。
- 今までハックな書き方をしていた部分がなくなる
- 表現できる自由度が更に増えることで様々なUIを作ることができるようになる

---
# まとめ

- IE対応は辛い。
- 今までハックな書き方をしていた部分がなくなる
- 表現できる自由度が更に増えることで様々なUIを作ることができるようになる

---
# 最後に

---

# 最後に

