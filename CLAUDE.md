# sun_r brands — ブランドサイト 引き継ぎ

「sun_r」ブランドの総合サイト。**ネイルサロンのサイト（sun_r nail）とは別のサイト**として Cloudflare で公開する。
sun_r nail のサイト・リポジトリには手を入れないこと（nail は既存サイトのまま残す）。

## 構成

```
public/
  index.html     ブランドトップ（3ブランドの入口）     黒のR
  shop.html      sun_r handmade shop（COMING SOON）    オレンジ
  creative.html  sun_r creative（制作中のアプリ）       イエロー
  images/        ロゴ（R：black/blue/orange/yellow）、ブランド番号（num-23/07/24）
wrangler.jsonc   Cloudflare 設定（name: sun-r-brands）
```

| ブランド | 色（ロゴ／帯） | 文字用の濃い色 | 番号 | 行き先 |
|---|---|---|---|---|
| sun_r nail | `#134CA5` | `#134CA5` | 23 | **外部サイト** https://sun-r-nail.pages.dev/ |
| sun_r handmade shop | `#E2712A`（帯 `#AE5112`） | `#AE5112` | 07 | shop.html |
| sun_r creative | `#E5BD42`（帯の文字は黒） | `#7E6100` | 24 | creative.html |

共通：背景 生成り `#F8F7F3`／本文 黒 `#111111`／英字 Jost 400／和文 Zen Kaku Gothic New。波の音は**入れない**（nail サイト専用）。

## 公開前の仕上げ（済み）

1. nail へのリンク：`data-nail-link` の href はすべて `https://sun-r-nail.pages.dev/`（index.html 3か所、shop.html・creative.html 各1か所、404.html 2か所）。nail は別サイトなので `target="_blank" rel="noopener"` で新しいタブで開く。nail 側のフッターにも brands へ戻るリンクあり
2. OGP／canonical：各ページの `<head>` に追加済み。URL は `https://sun-r-brands.pages.dev` の絶対URL（canonical は `/`・`/shop`・`/creative`）。og:image は `images/og-brands.png`／`og-shop.png`／`og-creative.png`（1200×630、生成り背景＋Rロゴ＋ブランド名）
3. 404ページ：`public/404.html`（黒のR＋「ページが見つかりません」＋トップへ戻る）。どのURLでも表示されるので画像・リンクは `/` 始まりの絶対パス

## デプロイ（sun_r nail と同じ：Cloudflare Pages + GitHub 自動デプロイ）

- 公開URL：https://sun-r-brands.pages.dev/
- GitHub `nyancolosan/sun-r-brands` の `main` に push すると自動でデプロイされる
- Pages 設定：プロジェクト名 `sun-r-brands`／フレームワークなし／ビルドコマンドなし／ビルド出力ディレクトリ `public`
- 初回だけダッシュボードで接続：Workers & Pages → 作成 → Pages → Git に接続 → `nyancolosan/sun-r-brands` を選び、上の設定で保存
- 割り当てられたURLが `sun-r-brands.pages.dev` でない場合や独自ドメインを使う場合は、各ページの canonical・og:url・og:image の URL を差し替える
- `wrangler.jsonc` は Workers で配信する場合の設定（Pages 公開では未使用）

## 変更しないこと
- デザイン（色・フォント・余白・アニメーション）、ブランド番号の位置（Rの右脚の中・右下、生成り色）
- creative のアプリ説明文は仮。オーナーから文言・公開URL（Web版・App Store）が届いたら差し替え／リンク追加。非公開GitHubリポジトリにはリンクしない
- shop の Instagram リンクは仮で sun_r nail のアカウント（https://www.instagram.com/sun___r_nail/）

## 確認項目（公開後）
- 375px／1280px で横スクロールが出ない
- トップの nail の行・ナビ「NAIL」・フッターの「sun_r nail」が https://sun-r-nail.pages.dev/ に飛ぶ
- shop／creative のヘッダーのロゴを押すとブランドトップに戻る
