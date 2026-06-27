---
name: ba:canva-spec
description: >
  Canvaのデザインモックアップと生の要件を読み込んで、詳細なUIおよびビジネス仕様書を作成します。
  Triggers when: user says "Canva読み込み", "Canvaから仕様書作成", or types /ba:canva-spec.
---

# /ba:canva-spec
**Role**: Business Analyst  
**Purpose**: Canvaのデザインと生の要件を分析し、詳細なUI/UX仕様書を作成します。

---

## 手順

1. 生の要件とCanvaデザインのスクリーンショット、または公開Canvaリンクを収集します.
2. 公開リンクの場合、**Browser subagent** を使用してスクリーンショットを撮影し、`docs/tasks/[TASK-ID]/canva-design.png` に保存します。
3. `canva-reader` サブエージェント（モデル: `sonnet` / `oracle`）を起動してデザインを解析します。
4. Human Gate: 解析結果の概要を提示し、`question()` を使用して不明点を質問します。
5. テンプレート `templates/task-doc-canva-requirements.md` を使用して `docs/tasks/[TASK-ID]/requirements.md` を作成します。
6. Final Human Gate: 仕様書の最終レビューと `question()` による承認。
