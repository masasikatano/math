---
name: verify-html
description: このサイトの HTML ページ（どのページでも）の画像参照・リンク切れ・マークアップの崩れを検査する。Use when the user asks to check or verify an HTML page after edits.
---

# HTML 検証スキル

このプロジェクトはビルド・テストシステムを持たない静的 HTML サイトなので、変更後は以下を手動で検査する。対象は編集した HTML（複数あればすべて）。

## 手順

1. `<img src="...">` の参照先がすべて実在するか確認（src は HTML ファイルからの相対パス）:

   ```sh
   f=prob.html   # 対象ページ
   d=$(dirname "$f")
   grep -o 'src="[^"]*"' "$f" | sed 's/src="//;s/"$//' | grep -v '^https\?://' | grep -v '^data:' | sort -u | while read -r p; do
     [ -f "$d/$p" ] || echo "MISSING: $p"
   done
   ```

2. `<tr>` / `<td>` / `<table>` の対応が崩れていないか目視（行追加・削除後は特に）。`<tr>` と `</tr>` の個数が一致するかで機械チェックもできる:

   ```sh
   echo "tr: $(grep -o '<tr[ >]' "$f" | wc -l) / $(grep -o '</tr>' "$f" | wc -l)"
   ```

3. 内部リンク（`href="..."`）が実在するか確認。`http` 外部リンクと `#` アンカーは除外:

   ```sh
   grep -o 'href="[^"]*"' "$f" | sed 's/href="//;s/"$//' | grep -v '^https\?://' | grep -v '^#' | sort -u | while read -r p; do
     [ -f "$d/$p" ] || echo "BROKEN LINK: $p"
   done
   ```

4. 変更箇所の alt 属性や `<caption>` が新しい内容と一致しているか目視で確認
