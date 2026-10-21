---
name: add-distribution
description: prob.html の確率分布テーブルに新しい分布の行を追加する。数式画像・グラフ画像の生成も行う。Use when the user asks to add a probability distribution (e.g. レヴィ分布, コーシー分布) to prob.html.
---

# 分布追加スキル

prob.html の「確率分布」テーブル（離散 prob.html:232 付近 / 連続 prob.html:464 付近）に新しい分布の行を追加する。

## 手順

1. 対象のテーブルを Read で確認し、既存行（例: prob.html:864 のコーシー分布、prob.html:889 付近のレヴィ分布）のマークアップ構造を真似る
2. 行は4列: 表記画像 `<td>` / LaTeX `<small>` / 意味（日本語、`<br />` 区切りの箇条書き）/ 例画像2枚（グラフ + 数式）
3. コメント `<!-- 分布名 -->` を行の前に付ける（既存行の慣習）
4. 画像が必要なら matplotlib で生成する:
   - システム Python に matplotlib が無い場合は `python3 -m venv` で一時 venv を作って利用する
   - 数式画像は `fig.text` + mathtext で透明背景 PNG、グラフは 150dpi 程度
   - 出力先は `img9/`（既存の画像配置先）
5. 画像 `<img>` には LaTeX ソースを `alt` に入れる（既存行の慣習）
6. 説明文に含める内容: 日本語名・英名・別名、定義域、パラメータの意味、尾の重さなどの性質、利用例、分布の名前の由来（数学者名）

## 注意

- 離散分布か連続分布かを間違えないこと
- 期待値・分散の有無など、定義域の端に注意（レヴィ分布は片側など）
- ファイルはインデントがタブ混在なので、Edit 前に Read で正確な空白を確認すること
