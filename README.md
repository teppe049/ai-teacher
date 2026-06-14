# AI Teacher

気になったことを質問するだけで、AIが静的HTML記事として蓄積・公開する個人ナレッジベース。

🔗 公開サイト: https://teppe049.github.io/ai-teacher/

## コンセプト

**メモる速度で記事化する。** 移動中・就寝前など、どこからでも知識を蓄積する。
ビルドツール不要、静的HTML/CSSのみ。GitHub Actions で push → 自動公開。

## 仕組み

```
お題（Issue or 直接指示）
        ↓
Claude Code が AGENTS.md のルールで記事HTML生成 + index.html更新
        ↓
git push → GitHub Actions → GitHub Pages で自動公開
```

## スマホからの使い方

1. GitHub アプリで `teppe049/ai-teacher` を開く
2. **Issues → New → 「📝 記事リクエスト」** を選ぶ
3. お題を書く（iOSキーボードのマイクで音声入力もOK）→ Submit

これで「あとで記事にするネタ」が Issue として貯まる。

## 記事を生成する（手元の作業）

自宅PCなどで Claude Code に:

> 「ai-teacher の open な記事リクエスト Issue を処理して」

→ Issue を読んで記事化 → push → 公開 → Issue クローズ、まで自動。
（push 前に差分を目視確認する運用）

## 構成

```
.
├── AGENTS.md                       # AIへの記事生成ルール
├── index.html                      # 記事一覧（トップ）
├── styles/site.css                 # 静的スタイル
├── articles/                       # 生成された記事HTML
├── .github/
│   ├── ISSUE_TEMPLATE/article.yml  # スマホからのお題投稿テンプレ
│   └── workflows/deploy.yml        # Pages自動デプロイ
└── .nojekyll                       # Jekyll無効化（静的配信）
```

## ルール

- 機密情報は書かない（このリポは **Public**）。
- 個人の人生データを管理する private リポの内容は転記しない。
