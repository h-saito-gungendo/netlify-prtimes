# PRtimes リダイレクト計測フォルダ

メールマガジンからのクリック数を GA4 で計測するための転送ページ一式。

## 転送先
https://prtimes.jp/main/html/rd/p/000000005.000153682.html

## 構成
| ファイル | 役割 |
|---|---|
| index.html | GA4計測 → PR TIMES へ自動転送するページ |
| netlify.toml | Netlify のビルド／リダイレクト設定 |
| _headers | CSP・noindex ヘッダ |
| package.json | ESM 指定 |
| netlify.code-workspace | VS Code 用ワークスペース |

## 使い方
1. このフォルダを Netlify にドラッグ&ドロップ（または Git 連携）でデプロイ。
2. 発行された URL（例: https://xxxx.netlify.app/）をメルマガ本文のリンク先にする。
3. GA4 → レポート → リアルタイム／イベント で `click_redirect` と `page_view` を確認。

## 変更したい箇所
- index.html 冒頭の `var TARGET` … 転送先URL
- Measurement Protocol の `params` … campaign / source / medium / content
  （現在: campaign='prtimes_202507', source='mailmagazine', medium='email'）
- 測定ID `G-M5FHJ3J8GH` と api_secret は、ほぼ日用と同じものを流用しています。
  別プロパティで集計する場合は差し替えてください。

## 注意
- 複数のメルマガで使い回す場合は、フォルダを複製して `campaign` 値を変えると
  GA4上で配信ごとのクリック数を分離できます。
