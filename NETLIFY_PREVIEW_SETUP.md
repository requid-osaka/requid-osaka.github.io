# Netlify で「公開前のみ」パスワード共有する安全な手順

ご指摘の通り、`netlify.toml` に `Basic-Auth = "user:password"` を直接書くと、
リポジトリ（GitHub）上に認証情報が残るため不適切です。

このリポジトリでは **認証情報をコード管理しない** 方針に変更し、
パスワード設定は Netlify 管理画面側で行う運用にします。

## 1) Netlify に接続
1. Netlify でこの GitHub リポジトリを新規サイトとして接続
2. Build command は空欄（静的サイトのため）
3. Publish directory は `.`

## 2) パスワード保護は Netlify 管理画面で設定
- Netlify の Site settings からアクセス制御（Password Protection / Access Control）を設定
- 認証情報は Netlify 側にのみ保存し、GitHub には保存しない

## 3) 公開前レビューの運用
- 公開前レビュー用のブランチ（例: `staging`）をデプロイ
- メンバーに URL とパスワードを安全な経路で共有
- 必要に応じて本番サイトとはサイト分離（preview 用サイトと production 用サイト）

## 4) 本番公開時
- 本番サイトではパスワード保護を無効化する、または本番専用サイトを使用
- 認証情報は定期的にローテーション

## 補足
- 以前の `netlify.toml` 方式（Basic-Auth 直書き）は削除済みです。
