# Zenn Articles Repository

このリポジトリは、Zennに投稿する記事を管理するためのものです。

## 📚 リポジトリ情報

- **GitHub URL**: https://github.com/engineers-hub-ltd-in-house-project/articles-zenn
- **Zenn Profile**: https://zenn.dev/engineers_hub_ltd (設定後)

## 🚀 セットアップ手順

### 1. 初回セットアップ（完了済み）

```bash
# Zenn CLIのインストール
npm install -g zenn-cli

# プロジェクトの初期化
npx zenn init

# GitHubリポジトリの作成
gh repo create engineers-hub-ltd-in-house-project/articles-zenn --public
```

### 2. ZennとGitHubの連携

1. [Zennのデプロイ管理ページ](https://zenn.dev/dashboard/deploys)にアクセス
2. 「GitHubからのデプロイ」をクリック
3. GitHubと連携（初回のみ）
4. リポジトリ `engineers-hub-ltd-in-house-project/articles-zenn` を選択
5. 「連携する」をクリック

## 📝 記事の管理

### 新しい記事を作成

```bash
# 記事の作成
npx zenn new:article --slug 記事のスラッグ --title "記事のタイトル"

# 例
npx zenn new:article --slug my-new-article --title "素晴らしい新記事"
```

### 記事のプレビュー

```bash
# ローカルでプレビュー
npx zenn preview

# ブラウザで http://localhost:8000 にアクセス
```

### 記事の公開

1. 記事ファイルの `published: false` を `published: true` に変更
2. 変更をコミット＆プッシュ

```bash
git add articles/記事ファイル名.md
git commit -m "記事を公開: 記事タイトル"
git push
```

## 📂 ディレクトリ構造

```
articles-zenn/
├── .gitignore
├── README.md          # このファイル
├── articles/          # 記事を格納
│   ├── .keep
│   └── *.md          # 各記事ファイル
└── books/            # 本を格納
    └── .keep
```

## 🎨 記事のフォーマット

### Frontmatter（記事の設定）

```yaml
---
title: "記事のタイトル"
emoji: "😊"              # アイキャッチ絵文字
type: "tech"             # tech: 技術記事 / idea: アイデア
topics: ["topic1", "topic2"]  # タグ（最大5つ）
published: false         # true: 公開 / false: 下書き
---
```

### 利用可能な絵文字

- 技術記事: 🚀 💻 🔧 ⚡ 🎯 📊 🔍 🛠️
- アイデア記事: 💡 ✨ 🌟 🎨 🌈
- Tips系: 📝 📌 💭 🔑

## 🔄 日常的なワークフロー

### 1. 記事を書く

```bash
# 新規記事作成
npx zenn new:article --slug article-slug

# エディタで編集
code articles/article-slug.md
```

### 2. プレビューで確認

```bash
npx zenn preview
```

### 3. 公開する

```bash
# published: true に変更後
git add .
git commit -m "feat: 新記事「タイトル」を公開"
git push
```

## 🛠️ トラブルシューティング

### プレビューが表示されない

```bash
# ポートを変更して起動
npx zenn preview --port 3000
```

### 画像が表示されない

- 画像は `articles/images/` に配置
- Markdownでは `/images/filename.png` で参照

### 記事が反映されない

1. GitHubへのpushが完了しているか確認
2. [Zennのデプロイ履歴](https://zenn.dev/dashboard/deploys)でエラーがないか確認

## 📋 記事執筆のベストプラクティス

### タイトル
- 具体的で検索されやすいタイトルにする
- 「〜する方法」「〜の解決策」など明確に

### トピックス（タグ）
- 関連性の高いものを3-5個選択
- 一般的な技術名を使用（例: react, typescript, aws）

### 構成
1. はじめに（課題・背景）
2. TL;DR（要約）
3. 本文（手順・解説）
4. まとめ
5. 参考リンク

### コードブロック
- 言語を指定してシンタックスハイライトを有効化
- ファイル名を記載（例: `\`\`\`ts:index.ts`）

## 🔗 便利なリンク

- [Zenn CLIの使い方](https://zenn.dev/zenn/articles/zenn-cli-guide)
- [Markdownの書き方](https://zenn.dev/zenn/articles/markdown-guide)
- [Zennのヘルプ](https://zenn.dev/faq)

## 📊 記事の管理コマンド

```bash
# すべての記事を一覧表示
ls -la articles/*.md

# 公開済み記事の確認
grep -l "published: true" articles/*.md

# 下書き記事の確認
grep -l "published: false" articles/*.md

# 記事数のカウント
ls articles/*.md | wc -l
```

---

Happy Writing! 📝✨