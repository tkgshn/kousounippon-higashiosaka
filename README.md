# kousounippon-higashiosaka（東大阪・対話型改善提案シート）

「対話型改善提案シート: 東大阪」（旧いどばた政策）で改善提案を受け付けるためのコンテンツリポジトリです。  
東大阪市の中間取りまとめ資料を Markdown 化し、テーマごとに分割したドキュメントを公開しています。policy-edit から参照し、対話的に改善提案（Pull Request）を作成できるようにすることを想定しています。

## 🔖 公開中のドキュメント

- [`docs/higashi-osaka-interim/`](docs/higashi-osaka-interim/)  
  「【A班修正】東大阪市第2回中間とりまとめ1115修正.docx」をテーマ別に再編したディレクトリです。各サブファイルで課題と主体別の取組アイデアを参照できます。

## 🔌 対話型改善提案シートとの連携手順

1. GitHub 上に `kousounippon-higashiosaka` など任意のリポジトリを作成し、このディレクトリの内容を push します。
2. `idobata` プロジェクトのルートで `.env.template` をコピーして `.env` を用意し、以下を設定します。
   - `GITHUB_TARGET_OWNER`：対象リポジトリのオーナー名
   - `GITHUB_TARGET_REPO`：対象リポジトリ名（例: `kousounippon-higashiosaka`）
   - `GITHUB_BASE_BRANCH`：改善提案のベースにするブランチ（通常は `main`）
   - `OPENROUTER_API_KEY`、`GITHUB_APP_ID`、`GITHUB_INSTALLATION_ID` など policy-edit で必要な環境変数
3. GitHub App の秘密鍵を `policy-edit/backend/secrets/github-key.pem` に配置します。
4. `docker-compose up --build -d policy-backend policy-frontend postgres-policy` で policy-edit を起動します。
5. ブラウザで `http://localhost:5174/view/docs/higashi-osaka-interim/` を開き、各テーマの Markdown を選択して AI との対話を開始します。

## 📦 新規リポジトリとして公開する手順例

```bash
cd kousounippon-higashiosaka
git init
git remote add origin git@github.com:<your-account>/kousounippon-higashiosaka.git
git add .
git commit -m "初回コミット: 東大阪市中間とりまとめのMarkdown版を追加"
git push -u origin main
```

公開後、policy-edit の `.env` を上記リポジトリに合わせて更新すれば、AI を通じた改善提案フローを利用できます。
