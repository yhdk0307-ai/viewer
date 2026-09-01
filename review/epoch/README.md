# EPOCH Manga Reviewer（開発中スライス）

> **ここは「開発中・自分が確認するもの」**。viewer の `/review/epoch/` へ転送される。
> LP からはリンクせず `robots.txt` で検索避けしてある。
> **完成して読ませるものは `outputs/publish/epoch/arc<N>/interactive/` → viewer `/pub/epoch/arc<N>/`**。
> 転送の正本は `.github/workflows/sync-viewer.yml` の `MAP`。ここに制作の中間物を置かないこと。
>
> **⚠ `reviewer*.html` と `index.html` は git で追跡していない（2026-07-27〜）**。
> `sync-viewer.yml` が CI で `build_reviewer.py` / `build_index.py` を実行して viewer へ直接送る。
> 材料（`scenes/<id>/pages/pageNNjp.png` と `dialogue.json`）を push すれば自動で反映される。
> ローカルで見たいときは自分で `build_reviewer.py --scene <id>` を実行する（生成物は commit しない）。
> 手書きで維持するのは `arc2_outline_map.html` / `manga_harness.html` / `outline_map_sync.json` / この README。

EPOCH マンガの Scene 別レビュー用ビューア (1 file HTML、画像 base64 埋め込み)。

## 公開 URL

GitHub Pages 経由で公開:

| Page | URL |
|---|---|
| **Index (目次)** | https://yhdk0307-ai.github.io/viewer/review/epoch/index.html |
| Arc 1 Scene 1 (ダートマス会議篇) | https://yhdk0307-ai.github.io/viewer/review/epoch/reviewer.html |
| Arc 1 Scene 2 (パーセプトロン篇) | https://yhdk0307-ai.github.io/viewer/review/epoch/reviewer_scene2.html |
| Arc 1 Scene 3 (第二次 AI ブーム篇) | https://yhdk0307-ai.github.io/viewer/review/epoch/reviewer_scene3.html |
| Arc 2 Scene 1 (冬を越えた 3 人篇) | https://yhdk0307-ai.github.io/viewer/review/epoch/reviewer_arc2_scene1.html |

新規 Scene の追加は `scripts/build_reviewer.py` の `SCENES` 辞書と `scripts/build_index.py` の `ARCS` リストに登録する。

## 機能

- 画像ペイン (左) + セリフペイン (右、スマホは下) のレイアウト
- 日本マンガ読み順 (左タップ = 次へ、右タップ = 前へ、矢印キーも同じ)
- 各ページの修正メモを localStorage に自動保存 (Scene 別 key)
- 全ページのメモを Markdown で Export ダウンロード
- dialogue / speaker をブラウザ上で編集 → Issue として送信 (Claude が dialogue.json をピンポイント更新)
- レスポンシブ対応 (PC / スマホ)

## 操作

| 動作 | キー | ボタン | タップ |
|---|---|---|---|
| 次のページ | ← (左矢印) | 「← 次」 | 画像の左半分 |
| 前のページ | → (右矢印) | 「前 →」 | 画像の右半分 |

## 再生成

scenes/<scene>/pages/page0N.png を更新したら:

```bash
# 個別 Scene の reviewer
python3 outputs/learning/manga_epoch/scripts/build_reviewer.py --scene arc2_scene1

# index の再生成 (page 数表示など更新したい時、新 Scene 追加時)
python3 outputs/learning/manga_epoch/scripts/build_index.py
```

→ `interactive/reviewer_<scene>.html` および `interactive/index.html` が再生成される。
main にマージすると `.github/workflows/sync-viewer.yml` が起動して `yhdk0307-ai/viewer` に自動同期される。
