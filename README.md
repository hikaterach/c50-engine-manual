# C50 エンジン マニュアルプラットフォーム

C50エンジンのオーバーホール及び組み立て方のマニュアルを管理・閲覧・編集できるWebプラットフォームです。

## 🎯 プロジェクト概要

このプラットフォームは、C50エンジンの整備情報を中央集約し、チームでの協働編集・進捗管理・リアルタイムコミュニケーションを実現します。

### 主な機能

- 📚 **マニュアル管理** - オーバーホール・組み立て手順の一元管理
- 👥 **ユーザー管理** - Google、Microsoft、Emailでの認証
- 🔐 **ロール管理** - 閲覧者、編集者、管理者の3段階
- 📊 **進捗管理** - チームの作業進捗を可視化
- 💬 **チャット機能** - リアルタイムコミュニケーション
- 👨‍👩‍👧‍👦 **グループ管理** - チーム単位での権限管理

## 🛠️ 技術スタック

- **フロントエンド:** Next.js 14 + React + TypeScript + Tailwind CSS
- **バックエン��:** Node.js + Express + TypeScript
- **データベース:** PostgreSQL
- **認証:** OAuth 2.0 (Google, Microsoft) + Email/Password
- **リアルタイム通信:** Socket.io
- **コンテナ化:** Docker

## 📁 プロジェクト構造

```
c50-engine-manual/
├── frontend/                 # Next.js フロントエンド
│   ├── app/                  # ページ・レイアウト
│   ├── components/           # React コンポーネント
│   ├── lib/                  # ユーティリティ・API クライアント
│   └── styles/               # スタイル定義
├── backend/                  # Express バックエンド
│   ├── src/
│   │   ├── routes/           # API ルート
│   │   ├── controllers/      # ビジネスロジック
│   │   ├── services/         # 外部サービス連携
│   │   ├── middleware/       # ミドルウェア（認証など）
│   │   ├── models/           # データベースモデル
│   │   └── config/           # 設定ファイル
│   └── tests/                # テスト
├── database/                 # PostgreSQL
│   └── migrations/           # マイグレーションファイル
├── docker-compose.yml        # Docker 設定
└── docs/                     # ドキュメント
```

## 🚀 クイックスタート

### 前提条件
- Node.js 18+
- Docker & Docker Compose
- PostgreSQL 15+

### セットアップ

```bash
# リポジトリをクローン
git clone https://github.com/hikaterach/c50-engine-manual.git
cd c50-engine-manual

# Docker でサービスを起動
docker-compose up -d

# 依存パッケージをインストール
cd frontend && npm install
cd ../backend && npm install

# 環境変数を設定
cp backend/.env.example backend/.env
cp frontend/.env.example frontend/.env

# データベースのマイグレーション
cd backend && npm run migrate

# 開発サーバーを起動
cd frontend && npm run dev
cd ../backend && npm run dev
```

## 📋 主要な機能要件

### ユーザー認証・管理
- [ ] Google OAuth ログイン
- [ ] Microsoft OAuth ログイン
- [ ] Email/パスワード登録・ログイン
- [ ] パスワードリセット機能
- [ ] ユーザープロフィール管理

### ロール・権限管理
- [ ] 閲覧者ロール
- [ ] 編集者ロール
- [ ] 管理者ロール
- [ ] 管理者による権限管理画面
- [ ] ロールベースアクセス制御（RBAC）

### マニュアル・コンテンツ管理
- [ ] マニュアル閲覧機能
- [ ] マニュアル編集機能（編集者以上）
- [ ] バージョン管理・履歴追跡
- [ ] リッチテキストエディタ
- [ ] ファイル・画像アップロード

### グループ・チーム管理
- [ ] グループ作成・管理
- [ ] ユーザーをグループに追加
- [ ] グループごとの権限設定

### 進捗管理
- [ ] タスク・マイルストーン管理
- [ ] 進捗ステータス表示
- [ ] グループ別進捗ダッシュボード

### チャット機能
- [ ] ダイレクトメッセージ（1対1）
- [ ] グループチャット
- [ ] リアルタイムメッセージング
- [ ] メッセージ履歴

## 🔐 セキュリティ

- JWTトークンベース認証
- HTTPS/TLS通信
- CSRF対策
- SQL インジェクション対策
- XSS対策
- Rate limiting

## 📞 サポート

問題が発生した場合は、[Issues](https://github.com/hikaterach/c50-engine-manual/issues) で報告してください。

## 📄 ライセンス

MIT License
