---
name: verify-html
description: HTML ページの画像参照・リンク切れ・マークアップの崩れを検査する。Use when the user asks to check or verify an HTML page after edits.
---

# HTML 検証スキル

このプロジェクトはビルド・テストシステムを持たない静的 HTML サイトなので、変更後は以下を手動で検査する。

## 手順

1. 編集した HTML 内の `<img src="...">` パスがすべて実在するか確認:
   `grep -o 'src="[^"]*"' <file> | sed 's/src="//;s/"//' | while read p; do [ -f "$p" ] || echo "MISSING: $p"; done`
2. `<tr>` / `<td>` / `<table>` の対応が崩れていないか目視（行追加・削除後は特に）
3. 内部リンク `./index.html` などが実在するか確認
4. 変更箇所の alt 属性や `<caption>` が新しい内容と一致しているか確認
