# UIGen

AI でReactコンポーネントを生成し、ライブプレビューするアプリ。Next.js 15 (App Router) / React 19 / Tailwind v4 / Prisma (SQLite) / Vitest。

## コマンド

| 目的 | コマンド |
|------|----------|
| 初期化（依存＋Prisma生成＋マイグレーション） | `npm run setup` |
| 開発サーバ | `npm run dev` |
| 開発サーバ（バックグラウンド、`logs.txt` に出力） | `npm run dev:daemon` |
| テスト | `npm test` |
| DB リセット | `npm run db:reset` |

- `NODE_OPTIONS='--require ./node-compat.cjs'` が全 next コマンドに必要。素の `next dev` は使わない。
- 動作確認でサーバを立てるときは `npm run dev:daemon` を使い、`logs.txt` を読む。フォアグラウンドで起動するとセッションが返らない。

## この構成でハマる点

- `src/generated/prisma/` は Prisma の生成物。手で編集しない。スキーマを変えたら `npx prisma generate` を通す。
- `ANTHROPIC_API_KEY` が未設定でもアプリは動く。その場合 LLM 生成の代わりに静的コードが返るので、「生成結果が固定に見える」ときはまず `.env` を疑う。
- インポートは `@/` プレフィックスを使う（`vite-tsconfig-paths` と tsconfig の両方で解決）。相対パスの深い遡り（`../../../`）を書かない。
- 生成コードの変換ロジックは `src/lib/transform/`、LLM に渡すプロンプトは `src/lib/prompts/`、ツール定義は `src/lib/tools/` にある。プロンプトを直すときはこの3つの整合を確認する。

## コンテキスト蓄積

- ビルド・テスト・環境の「毎回引っかかる点」はこのファイルに追記する。
- テスト規約は `.claude/rules/testing.md`（`*.test.ts(x)` を触るときだけ読み込まれる）。
- 受けた個別の訂正は auto memory に任せる。
