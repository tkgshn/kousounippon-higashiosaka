# kaizenteian-bot（改善提案ボット用リポジトリ）

「いどばた政策（policy-edit）」からの改善提案を受け付けるためのサンプルリポジトリです。  
東大阪市の中間とりまとめ資料を Markdown 化した文書を公開し、対話的に改善提案（Pull Request）を作成できるようにすることを想定しています。

## 🔖 公開中のドキュメント

- [`docs/higashi-osaka-interim-report.md`](docs/higashi-osaka-interim-report.md)  
  「【A班修正】東大阪市第2回中間とりまとめ1115修正.docx」を `npx mammoth --output-format=markdown` で変換したものです。必要に応じて Markdown の体裁を整えてください。

## 🔌 いどばた政策（policy-edit）との連携手順

1. GitHub 上に `kaizenteian-bot` など任意のリポジトリを作成し、このディレクトリの内容を push します。
2. `idobata` プロジェクトのルートで `.env.template` をコピーして `.env` を用意し、以下を設定します。
   - `GITHUB_TARGET_OWNER`：上記で作成したリポジトリのオーナー名
   - `GITHUB_TARGET_REPO`：上記で作成したリポジトリ名（例: `kaizenteian-bot`）
   - `GITHUB_BASE_BRANCH`：改善提案のベースにするブランチ（通常は `main`）
   - `OPENROUTER_API_KEY`、`GITHUB_APP_ID`、`GITHUB_INSTALLATION_ID` など policy-edit に必要な他の環境変数
3. GitHub App の秘密鍵を `policy-edit/backend/secrets/github-key.pem` に配置します。
4. `docker-compose up --build -d policy-backend policy-frontend postgres-policy` で policy-edit を起動します。
5. ブラウザで `http://localhost:5174/view/README.md` を開き、`docs/higashi-osaka-interim-report.md` を選択して AI との対話を開始します。

## 📦 新規リポジトリとして公開する手順例

```bash
cd kaizenteian-bot
git init
git remote add origin git@github.com:<your-account>/kaizenteian-bot.git
git add .
git commit -m "初回コミット: 東大阪市中間とりまとめのMarkdown版を追加"
git push -u origin main
```

公開後、policy-edit の `.env` を上記リポジトリに合わせて更新すれば、AI を通じた改善提案フローを利用できます。
