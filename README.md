# viewer

公開ツールの配信先。**中身は life リポジトリの `.github/workflows/sync-viewer.yml`
（`MAP_DEV`）が生成するので、ここを直接編集しても次の同期で上書きされる。**

- `tools/diagram_drawer/` — Diagram Engine（`tools/diagram_engine/interactive/` 由来）
- `epoch_arc*/`, `pub/epoch/` — 旧 URL から本番サイトへの転送
- `index.html`, `robots.txt` — 同期のたびに生成

自分用のもの（学習ノート・技術レポート・制作中のレビュー頁・構造図）は
2026-09-18 に認証付きの別ホストへ移した。ここには置かない。
