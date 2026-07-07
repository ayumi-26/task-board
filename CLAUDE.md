# CLAUDE.md

このファイルは、Claude Code (claude.ai/code) がこのリポジトリで作業する際のガイドラインです。

## プロジェクト概要

task-board は React (Vite) 製のタスク管理アプリです。

- タスクの追加・完了切り替え・削除ができるシンプルなタスクボード
- 完了済みタスクはグレー表示になる
- 主要ファイル: `src/App.jsx` (状態管理・UIロジック), `src/App.css` (スタイル)

### 開発コマンド

- `npm install`: 依存関係のインストール
- `npm run dev`: 開発サーバー起動
- `npm run build`: 本番ビルド
- `npm run deploy`: `gh-pages` ブランチにビルド成果物 (`dist/`) を公開

### GitHub Pages公開

- 公開URL: https://ayumi-26.github.io/task-board/
- `gh-pages` パッケージを使い、`dist/` を `gh-pages` ブランチにデプロイする方式。
- `vite.config.js` の `base: '/task-board/'` はこのサブパス配信のための設定なので変更しないこと。
- コードを更新した際は、通常の `git push` (mainブランチ) に加えて `npm run deploy` を実行し、
  公開サイトにも反映すること。

## 技術スタック

- React 19 + Vite (JavaScript, JSXは `.jsx` 拡張子。TypeScriptは未導入)
- スタイリングはプレーンCSS (CSSファイルをコンポーネントと同名で配置し、直接import)
- Lintは `oxlint` (`npm run lint`)
- 状態管理はReact標準の `useState` / `useEffect` のみ。外部の状態管理ライブラリは導入しない
- ルーティングライブラリは未導入 (単一画面のアプリのため)

## コンポーネント命名規約

- コンポーネントは1ファイル1コンポーネントとし、ファイル名はコンポーネント名と一致させる
  (例: `App.jsx` → `function App()`)
- コンポーネント名はパスカルケース (`TaskList`, `TaskItem` など)。ファイル名も同じくパスカルケースの `.jsx`
- 対応するスタイルは同名の `.css` ファイルに書き、コンポーネントファイル内で直接importする
  (例: `TaskList.jsx` + `TaskList.css`)
- 関数コンポーネント + Hooksで実装する (クラスコンポーネントは使わない)
- propsで渡すイベントハンドラは `onXxx` (例: `onToggle`, `onDelete`)、
  コンポーネント内部の関数は動詞から始める名前 (例: `addTask`, `toggleTask`) にする

## Git運用ルール

- **コードに変更を加えたら、その都度GitHubにプッシュすること。**
  - 変更内容ごとに適切な単位でコミットを作成し、コミット後は速やかに `git push` を実行する。
  - 変更を溜め込んでまとめてプッシュしない。
- コミットメッセージは変更の「何を」ではなく「なぜ」を意識して簡潔に書く。
- force push (`git push --force` 等) や `git reset --hard` などの破壊的操作は、
  ユーザーの明示的な許可なく行わない。
- リモートリポジトリ (GitHub) が未設定の場合は、プッシュ前にユーザーに確認する。
