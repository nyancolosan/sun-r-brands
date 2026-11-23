# sun_r brands — ブランドサイト 引き継ぎ

## 作業ルール
- 変更を push（＝公開サイトに反映）したら、返信に必ず公開URLを添える（変更したページのURL。両サイトに関わる場合は両方）
  - sun_r brands：https://sun-r-brands.pages.dev/（/shop・/creative・/build）
  - sun_r nail：https://sun-r-nail.pages.dev/
- sun_r nail と sun_r brands は連動させる。片方を変えたら、もう片方に関わる部分（nail のロゴ・表示名・色・URL・説明文、フッターのブランドナビ、brands のトップの nail の行など）も同じ作業の中で更新し、両方を push する（リポジトリ：`nyancolosan/sun-r-nail`／`nyancolosan/sun-r-brands`）


「sun_r」ブランドの総合サイト。**ネイルサロンのサイト（sun_r nail）とは別のサイト**として Cloudflare で公開する。
sun_r nail は別サイト・別リポジトリだが、上の作業ルールのとおり関連する変更は両方に反映する。

## 構成

```
public/
  index.html     ブランドトップ（4ブランドの入口）     黒の花
  shop.html      sun_r stitch（旧 handmade shop・COMING SOON）  マスタード
  creative.html  sun_r useful（旧 creative・アプリ）            グレージュ
  build.html     sun_r renovation（旧 build・キッチン施工・COMING SOON） オレンジ
  images/        ロゴ（手描きの花：black/blue/orange/yellow/greige）、OGP画像（og-*.png）
wrangler.jsonc   Cloudflare 設定（name: sun-r-brands）
```

| ブランド | 色（ロゴ／帯） | 文字用の濃い色 | 行き先 |
|---|---|---|---|
| sun_r nail | `#134CA5`（青い花 `logo-blue.svg`。nail サイトのロゴと同じ） | `#134CA5` | **外部サイト** https://sun-r-nail.pages.dev/ |
| sun_r stitch（旧 handmade shop） | `#E5BD42`（帯の文字は黒） | `#7E6100` | shop.html |
| sun_r useful（旧 creative） | `#9A8C7E`（帯も同色・文字は黒） | `#6B5F53` | creative.html |
| sun_r renovation（旧 build） | `#E2712A`（帯 `#AE5112`） | `#AE5112` | build.html |

共通：背景 生成り `#F8F7F3`／本文 黒 `#111111`／英字 League Spartan Regular（オーナー支給の TTF を woff2 に変換し `public/fonts/league-spartan-regular.woff2` から自前で配信。SIL OFL）／和文 Noto Sans JP（2026-11-23 に Jost／Zen Kaku Gothic New から変更。英字は Smooch Sans・Science Gothic・Caveat・Knewave・Boogaloo・Sue Ellen Francisco・Pacifico・Abril Fatface・Cinzel・Special Elite・Mrs Saint Delafield・Abril Fatface を経て League Spartan に）。波の音は**入れない**（nail サイト専用）。

## ブランド名（2026-11-23 変更）
- sun_r の頭文字にそろえて改名：s＝**stitch**（旧 handmade shop）／u＝**useful**（旧 creative）／n＝**nail**／_＝つなぐ線／r＝**renovation**（旧 build）
- 並び順はどこでも stitch・useful・nail・renovation（ヘッダー・フッター・トップの一覧・ヒーローのラベル）
- URL（/shop・/creative・/build）とファイル名は変えていない（共有済みリンクを壊さないため）
- 各ページのキャッチ（PRESERVED FLOWER & HANDMADE／APPS & TOOLS／KITCHEN CONSTRUCTION）や説明文はそのまま

## 公開前の仕上げ（済み）

1. nail へのリンク：`data-nail-link` の href はすべて `https://sun-r-nail.pages.dev/`（index.html 5か所〈ヘッダーナビ・ヒーローの NAIL・ブランド一覧・NAME の n・フッター〉、shop.html・creative.html・build.html 各1か所、404.html 2か所）。nail は別サイトなので `target="_blank" rel="noopener"` で新しいタブで開く。nail 側のフッターにも brands へ戻るリンクあり
2. OGP／canonical：各ページの `<head>` に追加済み。URL は `https://sun-r-brands.pages.dev` の絶対URL（canonical は `/`・`/shop`・`/creative`・`/build`）。og:image は `images/og-brands.png`／`og-shop.png`／`og-creative.png`／`og-build.png`（1200×630、生成り背景＋花のロゴ＋ブランド名）
3. 404ページ：`public/404.html`（黒の花＋「ページが見つかりません」＋トップへ戻る）。どのURLでも表示されるので画像・リンクは `/` 始まりの絶対パス

## デプロイ（sun_r nail と同じ：Cloudflare Pages + GitHub 自動デプロイ）

- 公開URL：https://sun-r-brands.pages.dev/
- GitHub `nyancolosan/sun-r-brands` の `main` に push すると自動でデプロイされる
- Pages 設定：プロジェクト名 `sun-r-brands`／フレームワークなし／ビルドコマンドなし／ビルド出力ディレクトリ `public`
- 初回だけダッシュボードで接続：Workers & Pages → 作成 → Pages → Git に接続 → `nyancolosan/sun-r-brands` を選び、上の設定で保存
- 割り当てられたURLが `sun-r-brands.pages.dev` でない場合や独自ドメインを使う場合は、各ページの canonical・og:url・og:image の URL を差し替える
- `wrangler.jsonc` は Workers で配信する場合の設定（Pages 公開では未使用）

## 変更しないこと
- デザイン（色・フォント・余白・アニメーション）
- ロゴは 2026-11-23 に R から手描きの花に変更（オーナー提供の最新版 zip の `logo-black/blue/orange/yellow.svg`）。花びらの白いハイライトは生成り `#F8F7F3`。ロゴにはブランド番号を入れない
- creative の S/TOOL は公開済み：https://stool.nyancolosan.workers.dev/ へ新しいタブでリンク。アイコンは S/TOOL の PWA アイコン（192px）を `images/app-stool.png` として使用
- creative のアプリ説明文は仮。オーナーから文言・公開URL（Web版・App Store）が届いたら差し替え／リンク追加。非公開GitHubリポジトリにはリンクしない
- shop の Instagram は handmade 専用アカウント（https://www.instagram.com/sun___r292324/）。ヘッダーと NEWS の帯の2か所

## 確認項目（公開後）
- 375px／1280px で横スクロールが出ない
- トップの nail の行・ナビ「NAIL」・フッターの「sun_r nail」が https://sun-r-nail.pages.dev/ に飛ぶ
- shop／creative のヘッダーのロゴを押すとブランドトップに戻る

## 補足
- 色の割り当ては 2026-11 に変更（handmade→マスタード、creative→グレー→グレージュ、build→オレンジ）
- `logo-greige.svg`（creative）は zip に無いので、青い花の `#134CA5` を `#9A8C7E` に置き換えて作成
- 名前の由来（トップの NAME セクション、ブランド一覧と ABOUT の間）：s＝stitch（handmade shop）／u＝useful（creative）／n＝nail（nail）／_＝link（all brands・4つをつなぐ）／r＝renovation（build）。文字の色は各ブランドの花（ロゴ）と同じ色：s #E5BD42／u #9A8C7E／n #134CA5／_ #111111／r #E2712A。PC は5列、スマホ（600px 以下）は縦に並ぶ。各マスは各ブランドへのリンク（_ は #brands へ）。ヒーローの「NAIL・HANDMADE・CREATIVE・BUILD」もそれぞれのページへのリンク
- トップに ABOUT（見出しは「ABOUT」のラベルだけ。中身は 屋号 sun_r／代表 門林 由佳／事業内容）。個人事業で法人化していないため肩書きは「代表」（「代表取締役」は使わない。法人化したら変更）
- PWA／ホーム画面アイコン：`public/manifest.webmanifest`（名前 sun_r brands、短い名前 sun_r、start_url `/`）。アイコンは生成り背景に黒の花（`images/icon-192.png`・`icon-512.png`・`icon-maskable-512.png`、iPhone 用 `apple-touch-icon.png` 180px）。全ページの `<head>` から読み込み。各ページのタブのアイコン（favicon）はブランド色の花
- スマホ向けの演出：一覧（トップのブランド・ABOUT、shop／build の項目、creative のアプリ）は `.stagger` で1行ずつ順に浮き上がる。トップのブランドの花・S/TOOL アイコンは `.pop` で表示時にポップ、タップ中に傾く（iOS で :active を効かせるため空の touchstart を登録）。「視差効果を減らす」がオンなら全部止まり、最初から表示される
- creative のアプリは個人事業「patch」（代表 門林 玲）が開発・提供。creative.html の各アプリに「by patch」、WORKS の説明文と meta description に patch を明記、ページ下に ABOUT（屋号 patch／代表 門林 玲／事業内容／アプリ）
- stitch（shop.html）の PRODUCTS「作品」：SR01・SR02・SR03（`images/products/sr01〜03.webp`。オーナー支給の写真から、外周につながる白背景だけを抜いた透過 WebP・長辺720px）。枠や背景色はなし（生成りの背景にそのまま置く）。大きさは正方形のエリアに object-fit: contain でそろえる。価格・購入リンクは未定なので「準備中」表示。PC 3列／タブレット 2列／420px 以下 1列
- build のページ文言（施工内容・施工事例は準備中）は仮。オーナーから会社情報・問い合わせ先が届いたら差し替え
