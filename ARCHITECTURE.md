# Architecture — degipa-mock

> ⚠️ このドキュメントは設計が固まり次第更新される。現在はドメイン整理段階。

## System Overview

```
┌─────────────────────────────────────────────────────────┐
│                    degipa-mock (PWA)                     │
│                                                         │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐  │
│  │  ① ユーザー   │  │ ② パートナー  │  │ ③ コモン     │  │
│  │   コンテキスト │  │  エージェント  │  │  ナレッジ     │  │
│  │              │  │              │  │              │  │
│  │ DiaryEntry   │  │ Analysis     │←→│ AgentBoard   │  │
│  │ Consultation │→│ TICValidation│  │ WelfareInfo  │  │
│  │ Memo         │←│ Report Gen   │  │ Upvote       │  │
│  │ Supporter    │  │              │  │              │  │
│  │ Report       │  │              │  │              │  │
│  └──────────────┘  └──────────────┘  └──────────────┘  │
│                                                         │
│  ┌──────────────┐  ┌──────────────┐                    │
│  │ ④ セキュリティ │  │ ⑤ インフラ    │                    │
│  │              │  │              │                    │
│  │ Encryption   │  │ Firebase Auth │                    │
│  │ FIDO2        │  │ wasm-cozodb  │                    │
│  │ Anonymizer   │  │ Vertex AI    │                    │
│  └──────────────┘  └──────────────┘                    │
└─────────────────────────────────────────────────────────┘
```

## Tech Stack

| Layer | Technology | Purpose |
|-------|-----------|---------|
| Frontend | TypeScript + PWA | ユーザーインターフェース |
| Local DB | wasm-cozodb | ブラウザ内データ蓄積 |
| Remote DB | CozoDB on Firebase (TBD) | 福祉情報 + 掲示板 |
| Auth | Firebase Auth | ユーザー認証 |
| LLM | Vertex AI | エージェント推論 |
| Hosting | Firebase Hosting | PWA 配信 |

## Source Structure (TBD)

```
src/
├── domain/          # ドメインロジック
│   ├── user/        # 日記、相談メモ、伝達リスト
│   ├── agent/       # パートナーエージェント、TIC
│   └── knowledge/   # 掲示板、福祉情報
├── infra/           # 外部サービス連携
│   ├── firebase/
│   ├── cozodb/
│   └── vertex-ai/
├── ui/              # UI コンポーネント
└── shared/          # 共通ユーティリティ
```

## Open Design Questions

CozoDB `open_questions` テーブルを参照。
