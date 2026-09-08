---
paths:
  - "src/**/*.test.ts"
  - "src/**/*.test.tsx"
  - "src/**/__tests__/**"
---

# テスト規約

- Vitest + React Testing Library。実行は `npm test`。
- テストファイルは対象ソースと同じ階層の `__tests__/` に置き、`[filename].test.ts(x)` と命名する。
- インポートは `@/` プレフィックスを使う。
- 環境は jsdom。ブラウザAPIを使う場合はモックを明示する。
- 各対象について happy path / エッジケース / エラー状態の3系統を最低限カバーする。
- 実装を通すためにテストを緩めない。テストが落ちたら実装側を直す。
