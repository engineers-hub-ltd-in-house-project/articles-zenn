---
title: "Claude CodeからZennに記事を投稿する方法"
emoji: "🚀"
type: "tech"
topics: ["claudecode", "zenn", "git", "automation", "ai"]
published: true
---

# はじめに

Claude Codeを使ってZennに記事を投稿したいと思ったことはありませんか？この記事では、Claude Codeを活用してZennへの記事投稿を効率化する方法を解説します。

# TL;DR

- Claude Codeで記事を作成・編集
- Zenn CLIを使ってローカルで記事を管理
- GitHubリポジトリと連携して自動投稿
- Claude Codeのセキュリティ制限を理解して適切に対処

# 前提条件

- Claude Codeがインストール済み
- Node.js/npmが利用可能
- GitHubアカウントを持っている
- Zennアカウントを持っている

# セットアップ手順

## 1. Zenn CLIのインストール

Claude Code内で以下のコマンドを実行：

```bash
npm install -g zenn-cli
```

## 2. Zennプロジェクトの作成

適切なディレクトリを作成して初期化します：

```bash
mkdir -p ~/articles/zenn
cd ~/articles/zenn
npx zenn init
```

これにより以下の構造が作成されます：

```
zenn/
├── .gitignore
├── README.md
├── articles/    # 記事を格納するディレクトリ
└── books/       # 本を格納するディレクトリ
```

## 3. Claude Codeのセキュリティ制限への対処

Claude Codeには作業ディレクトリの制限があります。以下のいずれかの方法で対処できます：

### 方法1: pushdコマンドを使用

```bash
pushd ~/articles/zenn > /dev/null && npx zenn new:article && popd > /dev/null
```

### 方法2: サブシェルで実行

```bash
(cd ~/articles/zenn && npx zenn new:article)
```

### 方法3: 作業ディレクトリ内でプロジェクトを作成

Claude Codeの作業ディレクトリ内でZennプロジェクトを作成することも可能です。

# 記事作成から投稿までの流れ

## 1. 新しい記事を作成

```bash
npx zenn new:article --slug my-awesome-article --title "素晴らしい記事のタイトル"
```

## 2. Claude Codeで記事を編集

作成された記事ファイルをClaude Codeで編集します：

```markdown
---
title: "素晴らしい記事のタイトル"
emoji: "✨"
type: "tech"
topics: ["technology", "programming"]
published: false
---

# 記事の内容をここに書く
```

## 3. プレビューで確認

```bash
npx zenn preview
```

ブラウザで `http://localhost:8000` にアクセスして記事をプレビューできます。

## 4. GitHubリポジトリの作成と連携

### リポジトリの初期化

```bash
git init
git add .
git commit -m "Initial commit"
```

### GitHubでリポジトリを作成後、リモートを追加

```bash
git remote add origin https://github.com/yourusername/zenn-content.git
git push -u origin main
```

## 5. ZennとGitHubの連携

1. [Zennのダッシュボード](https://zenn.dev/dashboard/deploys)にアクセス
2. 「GitHubからのデプロイ」を選択
3. 作成したリポジトリを連携

## 6. 記事の公開

記事を公開する場合は、frontmatterの`published`を`true`に変更：

```yaml
published: true
```

その後、変更をコミット＆プッシュ：

```bash
git add articles/my-awesome-article.md
git commit -m "Publish article: 素晴らしい記事のタイトル"
git push
```

# Claude Codeで効率化できること

## 1. 記事のテンプレート作成

Claude Codeに記事のテンプレートを作成してもらうことができます：

```bash
# Claude Codeに依頼
"Zennの技術記事のテンプレートを作成してください。
React Hooksについての記事で、実装例を含めてください。"
```

## 2. Markdownの整形

Claude Codeは美しいMarkdownを生成できます：

- 適切な見出し構造
- コードブロックのシンタックスハイライト
- 表やリストの整形

## 3. 画像の管理

Zennでは画像を`images/`ディレクトリに配置します：

```bash
mkdir -p articles/images
# 画像をコピー
cp /path/to/image.png articles/images/
```

Markdown内での参照：

```markdown
![画像の説明](/images/image.png)
```

## 4. 複数記事の一括管理

Claude Codeを使って複数の記事を効率的に管理できます：

```bash
# すべての記事をリスト
ls articles/*.md

# 特定のトピックを含む記事を検索
grep -l "React" articles/*.md
```

# よくあるトラブルと対処法

## 1. ディレクトリ移動の制限

**問題**: Claude Codeでは作業ディレクトリ外への`cd`が制限されている

**解決策**: 
- `pushd`/`popd`を使用
- 絶対パスでコマンドを実行
- 作業ディレクトリ内でプロジェクトを作成

## 2. プレビューサーバーが起動しない

**問題**: ポートが既に使用中

**解決策**:
```bash
# 別のポートを指定
npx zenn preview --port 3000
```

## 3. 画像が表示されない

**問題**: 画像パスが間違っている

**解決策**:
- 画像は`/images/`から始まるパスで参照
- ファイル名の大文字小文字に注意

# 高度な使い方

## 1. GitHub Actionsとの連携

`.github/workflows/zenn.yml`を作成：

```yaml
name: Publish to Zenn
on:
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      
      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'
      
      - name: Install Zenn CLI
        run: npm install -g zenn-cli
      
      - name: Validate articles
        run: npx zenn validate
```

## 2. 記事のメタデータ管理

Claude Codeで記事のメタデータを一覧表示：

```bash
# すべての記事のタイトルとステータスを表示
for file in articles/*.md; do
  echo "=== $file ==="
  grep -E "^title:|^published:" "$file"
done
```

## 3. 下書きと公開記事の管理

```bash
# 下書き記事のみ表示
grep -l "published: false" articles/*.md

# 公開済み記事のみ表示
grep -l "published: true" articles/*.md
```

# まとめ

Claude Codeを使ってZennへの記事投稿を効率化する方法を解説しました。主なポイント：

1. **Zenn CLIとGitHubの連携**で自動投稿を実現
2. **Claude Codeの制限**を理解して適切に対処
3. **効率的なワークフロー**で記事作成を加速

Claude Codeの強力な編集機能とZennの投稿システムを組み合わせることで、技術記事の執筆がより楽しく、生産的になります。

# 参考リンク

- [Zenn CLIの使い方](https://zenn.dev/zenn/articles/zenn-cli-guide)
- [ZennとGitHubリポジトリの連携](https://zenn.dev/zenn/articles/connect-to-github)
- [Claude Code Documentation](https://docs.anthropic.com/claude-code)

---

この記事がClaude CodeユーザーのZenn投稿の助けになれば幸いです。Happy Writing! 📝