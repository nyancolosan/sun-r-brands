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
  shop.html      sun_r handmade shop（COMING SOON）    マスタード
  creative.html  sun_r creative（アプリ）               グレージュ
  build.html     sun_r build（キッチン施工・COMING SOON） オレンジ
  images/        ロゴ（手描きの花：black/blue/orange/yellow/greige）、OGP画像（og-*.png）
wrangler.jsonc   Cloudflare 設定（name: sun-r-brands）
```

| ブランド | 色（ロゴ／帯） | 文字用の濃い色 | 行き先 |
|---|---|---|---|
| sun_r nail | `#134CA5`（青い花 `logo-blue.svg`。nail サイトのロゴと同じ） | `#134CA5` | **外部サイト** https://sun-r-nail.pages.dev/ |
| sun_r handmade shop | `#E5BD42`（帯の文字は黒） | `#7E6100` | shop.html |
| sun_r creative | `#9A8C7E`（帯も同色・文字は黒） | `#6B5F53` | creative.html |
| sun_r build | `#E2712A`（帯 `#AE5112`） | `#AE5112` | build.html |

共通：背景 生成り `#F8F7F3`／本文 黒 `#111111`／英字 Pacifico（つづけ字の筆記体風・1スタイルのみ）／和文 Noto Sans JP（2026-11-23 に Jost／Zen Kaku Gothic New から変更。英字は Smooch Sans・Science Gothic・Caveat・Knewave・Boogaloo・Sue Ellen Francisco を経て Pacifico に）。波の音は**入れない**（nail サイト専用）。

## 公開前の仕上げ（済み）

1. nail へのリンク：`data-nail-link` の href はすべて `https://sun-r-nail.pages.dev/`（index.html 3か所、shop.html・creative.html・build.html 各1か所、404.html 2か所）。nail は別サイトなので `target="_blank" rel="noopener"` で新しいタブで開く。nail 側のフッターにも brands へ戻るリンクあり
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
- トップに ABOUT（見出しは「ABOUT」のラベルだけ。中身は 屋号 sun_r／代表 門林 由佳／事業内容）。個人事業で法人化していないため肩書きは「代表」（「代表取締役」は使わない。法人化したら変更）
- PWA／ホーム画面アイコン：`public/manifest.webmanifest`（名前 sun_r brands、短い名前 sun_r、start_url `/`）。アイコンは生成り背景に黒の花（`images/icon-192.png`・`icon-512.png`・`icon-maskable-512.png`、iPhone 用 `apple-touch-icon.png` 180px）。全ページの `<head>` から読み込み。各ページのタブのアイコン（favicon）はブランド色の花
- スマホ向けの演出：一覧（トップのブランド・ABOUT、shop／build の項目、creative のアプリ）は `.stagger` で1行ずつ順に浮き上がる。トップのブランドの花・S/TOOL アイコンは `.pop` で表示時にポップ、タップ中に傾く（iOS で :active を効かせるため空の touchstart を登録）。「視差効果を減らす」がオンなら全部止まり、最初から表示される
- creative のアプリは個人事業「patch」（代表 門林 玲）が開発・提供。creative.html の各アプリに「by patch」、WORKS の説明文と meta description に patch を明記、ページ下に ABOUT（屋号 patch／代表 門林 玲／事業内容／アプリ）
- build のページ文言（施工内容・施工事例は準備中）は仮。オーナーから会社情報・問い合わせ先が届いたら差し替え
