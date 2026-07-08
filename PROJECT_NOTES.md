# TSM GOLF ランディングページ — プロジェクトノート

> 別のPCからでもこのプロジェクトの状況・決定事項・残タスクが分かるようにまとめた資料。
> 最終更新: 2026-07-08

---

## 1. これは何か

**福岡・博多のマンツーマンゴルフレッスン「TSM GOLF」の1ページLP（ランディングページ）。**
コーチである **砥綿（とわた／TOWATA）コーチ** の唯一無二の経歴（ゴルフ場のボール拾い→フロント→支配人→クラブクラフトマン→コーチ、格闘技20年、指導3,000人超）を"売り"にして、LINEでの無料相談・予約につなげる構成。

- 実体は `index.html` 1枚（HTML+CSS+JSすべて内包）＋ 画像 ＋ `robots.txt` / `sitemap.xml`。
- フレームワーク不使用。ビルド工程なし。ファイルをそのまま配信するだけ。

---

## 2. 公開・リポジトリ・ホスティング情報

| 項目 | 値 |
|---|---|
| 公開URL（本番） | https://golf-lp-towata.vercel.app |
| ホスティング | Vercel（プロジェクト名: `golf-lp-towata` / チーム: `golfami-s-projects`） |
| Gitリモート `origin` | https://github.com/prosperlian-eng/towata-lp |
| Gitリモート `swingmatrix` | https://github.com/swingmatrix-LP/towata-lp |
| メインブランチ | `main` |
| ローカルの場所 | `~/Desktop/towata_lp`（このMac上） |

> 注: リポジトリ名・URLは旧名 `towata` 由来のまま。屋号は「TSM GOLF」に変更済みだが、
> リポジトリ名やVercelプロジェクト名は実害がないのでそのまま運用している。

---

## 3. 変更・デプロイの手順（重要）

別PCで作業する場合：

```bash
# 1. クローン（初回のみ）
git clone https://github.com/prosperlian-eng/towata-lp.git
cd towata-lp

# 2. index.html を編集（本体はこれ1枚）

# 3. GitHubへ反映
git add -A && git commit -m "変更内容" && git push origin main

# 4. 本番デプロイ（Vercel CLIが必要: npm i -g vercel → vercel login）
vercel --prod --yes
```

- `vercel --prod --yes` を実行すると `golf-lp-towata.vercel.app` に即反映される。
- Vercel設定は `vercel.json`（`{ "cleanUrls": true }` のみ）。

---

## 4. ブランド方針（重要な決定事項）

**屋号＝「TSM GOLF」／ 主役＝「砥綿コーチ」** の二層構造。

- 事業の看板（タイトル・ロゴ・フッター・SEO情報）はすべて **TSM GOLF**。
- ただしコーチ個人の記述（プロフィール、「砥綿コーチが普通じゃない理由」等）は **あえて残す**。
  理由: このLPの最大の武器は"砥綿コーチの経歴"そのもの。名前を消すと売りが消える。
  （例えるなら「ブランド＝RIZAP／担当＝専属トレーナー」の関係）
- 画面上に残している「TOWATA」表記は**コーチ本人を指すもの**（alt文、`WHY TOWATA COACH`、
  「TOWATAコーチ本人が対応」）。これは意図的に保持。屋号の英語表記
  「Towata Golf Coaching」は TSM GOLF に修正済み。

### 名前の経緯（迷走したので記録）
- 元は「砥綿ゴルフコーチング」→ 一時「TMS GOLF」で作業 → **正しくは「TSM GOLF」**（綴り修正済み）。
- 「SwingMatrix」案もあったが、`.com`が取得済みで断念。

---

## 5. デザイン方針（決定事項と理由）

### フォント: 日本語はゴシックに統一
- 日本語は **Noto Sans JP（ゴシック）に統一**。明朝（Noto Serif JP）は全廃。
- 英語の飾りラベル（`ACCESS` `PLAN` 等）のみ **Cormorant Garamond**（上品なセリフ）を残す。
- 理由: 上位ゴルフレッスンLPは中高年ターゲットで**可読性最優先＝ゴシックが定番**
  （RIZAP GOLF等も同様）。明朝は細くて読みづらく、スポーツ指導には不向き。

### 改行（日本語の"泣き別れ"）対策
- 「単語の途中で改行される」問題を防ぐため、CSSで `word-break: auto-phrase`（文節改行）を採用。
- 加えて、句読点を含む見出し・重要コピーは `<span class="nw">…</span>`
  （`.nw { display:inline-block }`）で文節を塊にして、不自然な位置で折り返さないよう固定。
- モバイル用CSSで `word-break` が `normal` に戻っていたのが泣き別れの根本原因だった → 修正済み。

### ページ先頭表示
- URLを開いた時に必ずファーストビュー（ヒーロー）で表示されるよう、`<script>` 冒頭に
  「ハッシュ除去＋スクロール位置リセット」の処理を入れてある（`history.scrollRestoration='manual'` 等）。
  途中のセクションから表示される事故を防止。

---

## 6. 料金（現行）

**対面レッスン**
- 体験レッスン: 通常¥3,300 → **キャンペーン¥1,000**（税込）
- 通常レッスン 1回: **¥8,000**（税込）
- 3回チケット: **¥16,000**（税込・会員登録無料・1回あたり約¥5,333）
- ※別途場所代が必要（利用施設の料金に準じる）

**オンラインサポート**
- オンライン動画添削: **月額¥3,300**（税込・先着20名限定価格・今後改定予定）
- 内容: 動画添削＋改善ドリル 月2回 ／ Zoom個別相談 月1回30〜40分 ／ 公式LINEで随時質問対応
- ※支払い（決済方法）は予約時に個別案内

---

## 7. SEO 対応状況

`index.html` の `<head>` と別ファイルに実装済み：
- `meta description` / `keywords` / `author` / `canonical` / `robots`
- OGP（`og:*`）＋ Twitterカード（LINE/SNSシェア用。画像は `IMG_8377.jpg`）
- 構造化データ JSON-LD（`SportsActivityLocation`：業種・地域＝福岡市博多区・料金）
- `<h1>`（ヒーロー見出しをh1化）
- `robots.txt` ＋ `sitemap.xml`

---

## 8. 残タスク（TODO）

### ★最優先: 独自ドメイン取得
- **`tsmgolf.com` は空き（未登録）→ 早めに取得推奨**（`.com`が取れる貴重なケース）。
  取得先候補: Xserver Domain（日本語で簡単）/ Cloudflare（最安・英語）。
- 取得後にやること（ここは要作業）:
  1. Vercelに接続（`vercel domains add tsmgolf.com` → DNS設定）
  2. **サイト内のURL計8箇所を `tsmgolf.com` に書き換え**
     （`canonical` / `og:url` / `og:image` / `twitter:image` / JSON-LDの`url`・`image`
     ／ `sitemap.xml`の`<loc>` ／ `robots.txt`のSitemap行）。現状はすべて
     `golf-lp-towata.vercel.app` を指している。
  3. 旧URLから新ドメインへリダイレクト設定。
- ※ドメイン未取得のうちにURLを書き換えると、存在しないドメインを指してSEOが壊れるのでNG。**取得→接続してから書き換える**こと。

### 集客のための登録（ページ改善だけでは検索に載らない）
- **Google Search Console** 登録＆サイトマップ送信＆インデックス申請（これをしないと基本検索に出ない）。
  所有権確認は「HTMLタグ方式」が楽（発行されるmetaタグを`<head>`に貼る）。
- **Google ビジネスプロフィール**（Googleマップ）を「TSM GOLF／福岡市博多区／ゴルフ教室」で登録。
  → ゴルフレッスンの新規集客は、実はLPのSEOよりこれと**SNS動画（Reels/Shorts/TikTok）**が効く。

### 未確定・検討事項
- 拠点（対面レッスンの場所）の正式名称が未定（現状「拠点名 後ほど追加」表示、詳細はLINEで案内）。
- 「TSM」が何の略かは未確認（タイトル等に一言添えると訴求が上がる可能性）。

---

## 9. 作業ログ（このプロジェクトで行った主な変更）

新しい順（すべて本番反映・push済み）：

1. **フォント最適化** — 日本語を明朝混在からゴシック（Noto Sans JP）に統一。未使用フォント削除で軽量化。
2. **屋号の英語表記修正** — フッターの「Towata Golf Coaching」→「TSM GOLF」（直し漏れ修正）。
3. **リブランド** — 屋号を「TSM GOLF」に統一（日本語・英語とも）。コーチ名「砥綿コーチ」は保持。
   （途中「TMS GOLF」で入れたのを「TSM GOLF」に綴り修正）
4. **料金改定** — 通常1回 ¥7,700→¥8,000、3回券 ¥16,500→¥16,000（構造化データも更新）。
5. **SEO一式追加** — meta description / OGP / 構造化データ / h1 / robots.txt / sitemap.xml。
6. **改行(泣き別れ)修正** — word-breakをauto-phraseに、`.nw`で文節固定。決済方法の注記を追加。
7. **URL先頭表示の修正** — URLを開いた時に必ずヒーローで表示されるよう防御スクリプト追加。
   `vercel.json` の無効プロパティ（`public`）も削除。

（1〜7より前の初期状態: ヒーロー3枚スライドショー、オンラインセクションのダーク化、
料金プラン、LINE公式アカウント連携などは既に実装済みだった）
