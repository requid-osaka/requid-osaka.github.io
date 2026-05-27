# Netlify で「公開前のみ」パスワード共有する手順

このリポジトリには、`netlify.toml` で Basic 認証ヘッダーを付与する設定を追加しています。

## 1) Netlify に接続
1. Netlify でこの GitHub リポジトリを新規サイトとして接続
2. Build command は空欄（静的サイトのため）
3. Publish directory は `.`

## 2) 認証情報を変更
`netlify.toml` の以下を必ず変更してください。

- `preview`（ユーザー名）
- `change-this-password`（パスワード）

```toml
Basic-Auth = "preview:change-this-password"
```

## 3) メンバー限定共有の運用
- 公開前レビュー中: この設定を有効にしたブランチ（例: `staging`）を Netlify へデプロイし、URL と ID/PW をメンバーのみに共有
- 本番公開時: 
  - `Basic-Auth` を削除してデプロイ、または
  - 本番用サイトを別に分けて Basic 認証なしで配信

## 4) 注意点
- Basic 認証はブラウザ標準ダイアログです。
- この方式は手軽ですが、厳密なアクセス制御が必要な場合は Netlify のチーム向けアクセス制御機能を検討してください。
