---
name: qa:ui-verify
description: >
  実際のUIスクリーンショットをCanvaのデザインモックアップと比較し、レイアウトやスタイルの違いを報告します。
  Triggers when: user says "UI検証", "CanvaとUI比較", "デザインチェック", or types /qa:ui-verify.
---

# /qa:ui-verify
**Role**: QA  
**Purpose**: Canvaのオリジナルデザインと実際のUIスクリーンショットを視覚的に比較し、相違点をデベロッパー向けにログ出力します。

---

## 手順

1. タスクID、デザインのスクリーンショットパス、実際のUIパスを収集します（またはローカルサーバーを起動し、ブラウザサブエージェントでキャプチャします）。
2. 画像を `docs/tasks/[TASK-ID]/canva-design.png` と `docs/tasks/[TASK-ID]/actual-ui.png` に保存します。
3. `ui-comparator` サブエージェント（モデル: `sonnet` / `oracle`）を起動して画像を比較します。
4. テンプレート `templates/ui-feedback.md` を使用して `docs/tasks/[TASK-ID]/ui-feedback.md` を作成します。
5. Human Gate: 検証結果の概要と一致スコアを提示し、`question()` で確認します。
6. デベロッパーに対し、`ui-feedback.md` を確認してレイアウトバグを修正するよう促します。
