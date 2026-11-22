# sun_r brands — ブランドサイト 引き継ぎ

「sun_r」ブランドの総合サイト。**ネイルサロンのサイト（sun_r nail）とは別のサイト**として Cloudflare で公開する。
sun_r nail のサイト・リポジトリには手を入れないこと（nail は既存サイトのまま残す）。

## 構成

```
public/
  index.html     ブランドトップ（4ブランドの入口）     黒のR
  shop.html      sun_r handmade shop（COMING SOON）    マスタード
  creative.html  sun_r creative（アプリ）               グレージュ
  build.html     sun_r build（キッチン施工・COMING SOON） オレンジ
  images/        ロゴ（R：black/blue/orange/yellow/greige）、ブランド番号（num-23/07/24/1329）、OGP画像（og-*.png）
wrangler.jsonc   Cloudflare 設定（name: sun-r-brands）
```

| ブランド | 色（ロゴ／帯） | 文字用の濃い色 | 番号 | 行き先 |
|---|---|---|---|---|
| sun_r nail | `#134CA5` | `#134CA5` | 23 | **外部サイト** https://sun-r-nail.pages.dev/ |
| sun_r handmade shop | `#E5BD42`（帯の文字は黒） | `#7E6100` | 07 | shop.html |
| sun_r creative | `#9A8C7E`（帯も同色・文字は黒） | `#6B5F53` | 24 | creative.html |
| sun_r build | `#E2712A`（帯 `#AE5112`） | `#AE5112` | 1329 | build.html |

共通：背景 生成り `#F8F7F3`／本文 黒 `#111111`／英字 Jost 400／和文 Zen Kaku Gothic New。波の音は**入れない**（nail サイト専用）。

## 公開前の仕上げ（済み）

1. nail へのリンク：`data-nail-link` の href はすべて `https://sun-r-nail.pages.dev/`（index.html 3か所、shop.html・creative.html・build.html 各1か所、404.html 2か所）。nail は別サイトなので `target="_blank" rel="noopener"` で新しいタブで開く。nail 側のフッターにも brands へ戻るリンクあり
2. OGP／canonical：各ページの `<head>` に追加済み。URL は `https://sun-r-brands.pages.dev` の絶対URL（canonical は `/`・`/shop`・`/creative`・`/build`）。og:image は `images/og-brands.png`／`og-shop.png`／`og-creative.png`／`og-build.png`（1200×630、生成り背景＋Rロゴ＋ブランド名）
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
- creative の S/TOOL は公開済み：https://stool.nyancolosan.workers.dev/ へ新しいタブでリンク。アイコンは S/TOOL の PWA アイコン（192px）を `images/app-stool.png` として使用
- creative のアプリ説明文は仮。オーナーから文言・公開URL（Web版・App Store）が届いたら差し替え／リンク追加。非公開GitHubリポジトリにはリンクしない
- shop の Instagram は handmade 専用アカウント（https://www.instagram.com/sun___r292324/）。ヘッダーと NEWS の帯の2か所

## 確認項目（公開後）
- 375px／1280px で横スクロールが出ない
- トップの nail の行・ナビ「NAIL」・フッターの「sun_r nail」が https://sun-r-nail.pages.dev/ に飛ぶ
- shop／creative のヘッダーのロゴを押すとブランドトップに戻る

## 補足
- 色の割り当ては 2026-11 に変更（handmade→マスタード、creative→グレー→グレージュ、build→オレンジ）。番号画像の点々の色もブランド色に合わせてある
- `logo-greige.svg` は青ロゴの各色を「生成り↔ブランド色」の混色比率のまま `#9A8C7E` に置き換えて作成
- `num-1329.svg` の「3」「2」は num-23 の形をそのまま使い、「1」「9」は同じ太さ・丸みで描き起こし（マスクで点々を入れている）
- トップに ABOUT（見出しは「ABOUT」のラベルだけ。中身は 屋号 sun_r／代表 門林 由佳／事業内容）。個人事業で法人化していないため肩書きは「代表」（「代表取締役」は使わない。法人化したら変更）
- PWA／ホーム画面アイコン：`public/manifest.webmanifest`（名前 sun_r brands、短い名前 sun_r、start_url `/`）。アイコンは生成り背景に黒のR（`images/icon-192.png`・`icon-512.png`・`icon-maskable-512.png`、iPhone 用 `apple-touch-icon.png` 180px）。全ページの `<head>` から読み込み。各ページのタブのアイコン（favicon）はブランド色のRのまま
- スマホ向けの演出：一覧（トップのブランド・ABOUT、shop／build の項目、creative のアプリ）は `.stagger` で1行ずつ順に浮き上がる。トップのブランドのR・S/TOOL アイコンは `.pop` で表示時にポップ、タップ中に傾く（iOS で :active を効かせるため空の touchstart を登録）。「視差効果を減らす」がオンなら全部止まり、最初から表示される
- creative のアプリは個人事業「patch」（代表 門林 玲）が開発・提供。creative.html の各アプリに「by patch」、WORKS の説明文と meta description に patch を明記、ページ下に ABOUT（屋号 patch／代表 門林 玲／事業内容／アプリ）
- build のページ文言（施工内容・施工事例は準備中）は仮。オーナーから会社情報・問い合わせ先が届いたら差し替え
