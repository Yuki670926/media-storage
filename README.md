# media-storage

iPhone に保存された写真・動画を、**自分の管理するストレージ(自宅サーバーなど)へ自動バックアップする**個人用システム。

## ステータス

**設計フェーズ完了・実装未着手。** このリポジトリは、クローンした人(= 運用者)が Claude Code を使って要件の最終決定と実装を進められるように文書化されている。

## 使い始め方(運用者向け)

1. このリポジトリをクローンする
2. Claude Code でセッションを開き、次のように依頼する:
   > CLAUDE.md と docs/ を読んで、REQUIREMENTS.md §5.2 のチェックリストを一緒に確定させてほしい
3. [docs/HARDWARE.md](docs/HARDWARE.md) を参考に機材を用意する(推奨: ミニ PC + USB HDD、約 3.5 万円。既存 PC の流用も可)
4. Phase 0(サーバー基盤)から実装を進める([docs/DESIGN.md](docs/DESIGN.md) §8 のロードマップ順)

## ドキュメント構成(読む順)

1. [docs/REQUIREMENTS.md](docs/REQUIREMENTS.md) — 要件定義。非機能要件の優先順位(トレードオフ方針)、決定済み事項、運用者が最終決定する項目
2. [docs/DESIGN.md](docs/DESIGN.md) — 設計書。アーキテクチャ、データモデル、アップロードプロトコル、iOS アプリ構成、開発ロードマップ
3. [docs/HARDWARE.md](docs/HARDWARE.md) — 機材・コスト計画。選択肢の比較と段階的拡張プラン
- [CLAUDE.md](CLAUDE.md) — 実装を担当する Claude Code 向けの指示(読む順・鉄則・フェーズの完了条件)

## 構成(予定)

- **iOS アプリ** (Swift / SwiftUI): 写真ライブラリの差分検出とバックグラウンドアップロード
- **API サーバー** (Docker Compose): メタデータ管理(PostgreSQL)+ ストレージ層(ローカル FS → S3 互換に差し替え可能)
- **Web UI**: 外出先からのタイムライン閲覧(Phase 2、既定は Tailscale 経由で非公開)
