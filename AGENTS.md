# AGENTS.md — AI記事生成ルール

このリポジトリは「気になったことを質問するだけで、静的HTML記事として蓄積・公開する個人ナレッジベース」です。
AI（Claude Code）がこのファイルのルールに従って記事HTMLを生成します。

## コンセプト

- **メモる速度で記事化する。** 移動中・就寝前など、どこからでも知識を蓄積する。
- ビルドツールは使わない。**静的HTML/CSSのみ**。GitHub Pagesでそのまま公開できる状態を保つ。

## 記事を1本作るときの手順

1. 質問（お題）を受け取る。
2. カテゴリを決める（`dev` / `ai` / `infra` / `game` / `life` / `other` から選ぶ。なければ追加してよい）。
3. `articles/{カテゴリ}-{kebab-case-slug}.html` を生成する。
   - 例: お題「git rebase と merge の違い」→ `articles/dev-git-rebase-vs-merge.html`
4. 記事テンプレート（後述）に沿ってHTMLを書く。
5. `index.html` の記事一覧に1行追加する（新しい記事を**先頭**に）。
6. 人間が差分を確認してからコミット・プッシュする。

## 記事HTMLテンプレート

すべての記事は以下の構造に従う。`{{ }}` を実際の値で埋める。

```html
<!DOCTYPE html>
<html lang="ja">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>{{記事タイトル}} | AI Teacher</title>
  <meta name="description" content="{{120字以内の要約}}">
  <link rel="stylesheet" href="../styles/site.css">
</head>
<body>
  <main class="article">
    <nav class="breadcrumb"><a href="../index.html">← 一覧へ</a></nav>
    <article>
      <span class="category cat-{{カテゴリ}}">{{カテゴリ}}</span>
      <h1>{{記事タイトル}}</h1>
      <p class="meta">{{YYYY-MM-DD}}</p>

      <!-- 本文。h2/h3, p, ul/ol, pre>code, table を使う -->

    </article>
    <footer class="site-footer">
      <a href="../index.html">AI Teacher</a> — メモる速度で記事化する
    </footer>
  </main>
</body>
</html>
```

## 本文の書き方ルール

- **結論ファースト。** 冒頭に「一言でいうと」を置く。
- 自分が後で読み返して即思い出せる粒度。教科書ではなくメモ。
- コードは `<pre><code>` で囲む。言語ごとにシンタックスは付けない（静的・依存ゼロを優先）。
- 表で比較すると分かりやすいものは `<table>` を使う。
- 出典・参考URLがあれば末尾に「参考」セクションでリンクする。
- 推測で断言しない。不確かな点は「要確認」と明記する。
- 長さの目安: 300〜800字。深掘りが必要なら長くてよいが、冗長にしない。

## index.html への追加ルール

記事一覧の `<ul class="article-list">` の**先頭**に以下の形式で1行追加する:

```html
<li>
  <a href="articles/{{ファイル名}}">{{記事タイトル}}</a>
  <span class="category cat-{{カテゴリ}}">{{カテゴリ}}</span>
  <span class="date">{{YYYY-MM-DD}}</span>
</li>
```

## やってはいけないこと

- 外部CDN・JSフレームワーク・ビルドツールを導入しない。
- 機密情報（個人情報・認証情報・非公開の業務情報）を記事に書かない。**このリポはPublic**。
- `life` リポジトリの内容をそのまま転記しない。
