# math — 計算機科学で使用する記号と分布の一覧

数学・計算機科学で使う記号と確率分布を、記号・LaTeX・意味・例つきの表でまとめた静的 HTML リファレンスサイト。

## 構成

- `index.html` — トップページ（分野別インデックス）
- 分野ページ: `prob.html`（確率）、`alg.html`（代数）、`anal.html`（解析）、`derivative.html`（微分）、`ineq.html`（不等式）、`elec.html`（電気）、`econ.html`（経済）、`comp.html`（計算機科学）など
- `img*/` — 数式・グラフの PNG 画像。画像は外部ツールで生成したものが多く、ページごとにまとまっている（`img9/` は prob.html が主に使用）

## ページの構造

各ページは Tailwind CSS（CDN）を使った単一 HTML で、`<table>` の集まり:
- 1列目: 記号・表記の画像
- 2列目: LaTeX 表記
- 3列目: 意味（日本語の箇条書き、`<br />` 区切り）
- 4列目: 例・グラフ画像

## エージェント向けガイドライン

- ビルド・テスト・Lint は存在しない。変更後はブラウザで開くか、`verify-html` スキルで画像参照・マークアップの整合を確認する
- 新しい分布・記号・公式の行追加は `add-table-row` スキルに従う（`/add-distribution`, `/add-symbol` コマンドもこのスキルを参照する）
- 数式画像・グラフ画像が必要なら matplotlib で生成し `img9/` 等に置く。matplotlib はユーザーの Python 環境にインストール済み（`pip3 install --user --break-system-packages matplotlib numpy`、2026-10 時点で matplotlib 3.11.2 / numpy 2.5.4）なのでそのまま使える
- 画像 `<img>` には LaTeX ソースを `alt` 属性に入れる（既存の慣習）
- 説明文は日本語で、既存の行と同じ粒度（別名・英名・定義・利用例・名前の由来）で書く
- HTML のインデントはタブとスペースが混在している。Edit する前に必ず Read で対象箇所の正確な空白を確認する
- 既存の `img*/` 内の画像は他ページから参照されている可能性がある。削除・リネームは行わない

## エージェント設定ファイル

- `.mcp.json` — MCP サーバ設定（現在未使用）
- `.claude/settings.json`, `.antigravity/settings.json` — ファイル編集の許可設定
- `.claude/commands/*.md` — スラッシュコマンド（`/add-distribution`, `/add-symbol`）
- `.claude/skills/` — スキル定義。`.agents/skills/` と `.kimi/skills/` はここへのシンボリックリンク
- `.claudeignore` — エージェントに無視させるファイル。`.antigravityignore` / `.kimiignore` はここへのシンボリックリンク
- `AGENTS.md` / `CLAUDE.md` / `ANTIGRAVITY.md` — 本ファイルへのシンボリックリンク
