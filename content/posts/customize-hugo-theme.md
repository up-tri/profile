+++
date = 2021-02-06T09:00:00Z
lastmod = 2021-02-06T09:00:00Z
author = "default"
title = "Hugoテーマ「axiom」をカスタマイズしてみたよ"
subtitle = "Hugoテーマの「axiom」をカスタマイズ（とか）したときの知見を書いているよ！"
+++

こんにちは。

このサイトは Hugo のテーマ、[axiom](https://www.axiomtheme.com/)を使っていますが、主に下記内容をカスタマイズしています。

- [FontAwesome](https://fontawesome.com/) アイコンの導入
- 記事内フォントを[Noto Sans JP](https://fonts.google.com/specimen/Noto+Sans+JP)へ変更
- markdown 内での RAW HTML 許可
- リンクテキストの CSS 変更

詳細のコードは[GitHub](https://github.com/up-tri/profile)で公開しているので、必要な方・急いでいる方はご覧くださいませ。

## markdown 内での RAW HTML 許可

これを実装しないと FontAwesome アイコンが使えないですからね。変えました。

```toml
[params]
disableThemeAttribution = true
```

## FontAwesome の導入

`~/static/webfonts`に、FontAwesome のフリー版を配置しました。後述のカスタム CSS で import します。

## カスタム CSS の導入

axiom では、テーマ CSS のカスタマイズが可能となっています。
`assets/custom.css`に CSS を実装することで、お好みのスタイルで上書きすることができます。

{{< alert message="このカスタムCSSはaxiom独自の機能です。" type="warn" badge="注意" >}}

```css
@import url("https://fonts.googleapis.com/css2?family=Noto+Sans+JP:wght@100;400;700&display=swap");
@import url("/webfonts/css/all.min.css");

.font-content-title,
.cdata > blockquote p,
.cdata > ol,
.cdata > p,
.cdata > ul {
  font-family: "Noto Sans JP", sans-serif !important;
}

.font-content-title {
  font-weight: 600;
}

.cdata a {
  text-decoration: underline;
  font-weight: bold;
  color: rgb(0, 81, 173) !important;
}
```

**ところがどっこい！** axiom のテーマでは、デフォルト CSS ファイルの末尾にカスタム CSS を`post-css`で結合するため、
本来ファイル冒頭に書かなければ動かない`@import`が機能しないのです。（[このへん](https://github.com/marketempower/axiom/blob/master/layouts/partials/styles-app.html#L2-L6)）

ということで自アカウントに Fork して修正対応し、ついでに [PR 投げておきました](https://github.com/marketempower/axiom/pull/27)。
見てくれると良いな...。

---

上記の他にも`config.toml`を色々いじっています。

Fork してのカスタマイズ、最初からオリジナルテーマ作れば良いのでは？それは言わない約束。

ということで、めでたしめでたし。
