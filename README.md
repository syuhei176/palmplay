# Palmplay 🖐️ — 手・指で遊ぶ webカメラゲーム集

webカメラに映る手・指の動きだけで遊ぶブラウザゲーム集。**バックエンド／ビルド不要**、HTML 1枚ずつで動きます。

🎮 **遊ぶ → <https://palmplay.syuhei176.com>**

トップページ（[index.html](index.html)）は各ゲームへのランチャーです。目玉は両手ハンドルの3Dレースと、操縦桿を握るコックピットフライトの2本。

## 🏎️✈️ 目玉

- **[racing.html](racing.html) — Hand Kart 3D 🏎️**: 両手でハンドルを握って回すと曲がれる擬似3Dレース（Three.js）。🪙 を集めて 🚧 を避け、60秒で距離を稼ぐ。アクセルは自動、ライバルと順位を競う。
- **[cockpit.html](cockpit.html) — Hand Cockpit ✈️**: コックピット視点の3Dフライト（Three.js）。✊左手＝スロットルレバー、✊右手＝操縦桿（手前に引く＝機首上げ／傾け＝バンク旋回）。Vr まで加速→ROTATE で離陸し**自由飛行**。窓の外には自機の機首・回るプロペラ・主翼が見え、**夕景**の空・テクスチャ地面・滑走路・窓明かりのビル・雲でリアルに。旋回して**出発した滑走路へ帰投**し、**PAPI／ND（ナビ表示）**を見ながら降下して **🛬 着陸**（接地の降下率で GREASER/FIRM/HARD 採点）。失速・ハードランディング注意。カメラ無しでもキーボード（W/S・↑/↓・←/→）で操作可。

## そのほかのゲーム

- **[slash.html](slash.html) — Hand Slash 🍉**: 人差し指を振って果物を斬るフルーツニンジャ風。💣 を避けて60秒スコアアタック。最大4手の協力プレイ対応。
- **[shooter.html](shooter.html) — Shuriken Shooter 🥷**: 奥から迫る敵 👹 を手裏剣で撃つシューティング。👌 つまんで離すと発射。遠近スケーリングで奥行きを表現。両手対応。
- **[tamaire.html](tamaire.html) — Tama-ire 🧺**: 足元の紅白玉を手ですくって弾き、左右に動くカゴに入れる玉入れ。手のひら全体（21点）が当たり判定。両手OKの60秒スコアアタック（ベストスコア保存）。
- **[ohajiki.html](ohajiki.html) — Ohajiki Battle 🔵🔴**: 2人対戦のはじき出しおはじき。👌 自分の色の玉をつまんで振って離すと弾き飛ぶ。相手の玉を盤外へ落とせ。左の人＝青／右の人＝赤、90秒で残数勝負。
- **[gunsurvivor.html](gunsurvivor.html) — Gun Survivor 🔫🧟**: 指ガンで撃つガンサバイバー風レールシューター。👉 人差し指で照準・👍 親指を倒すと発砲、頭を撃てば一撃ボーナス。弾切れは画面下を狙ってリロード。One Euro Filter＋エイムアシストで“狙える感”を出した体力サバイバル（ベストスコア保存）。
- **[freethrow.html](freethrow.html) — Free Throw 🏀**: バスケのフリースロー。ボールを持って実際にシュートするように手を振り上げて放つ。振り上げの速さ＝アーチの強さ（左ゲージの緑が適正）、手の左右＝狙い。放物線で奥のゴールへ。スウィッシュ✨・バンク🟦判定＆連続で倍率UP、60秒チャレンジ（ベストスコア保存）。

## 技術

- [MediaPipe Hand Landmarker](https://ai.google.dev/edge/mediapipe) … ブラウザ上で動く手検出AI（CDN読み込み）
- 描画は **Canvas 2D**。`racing.html` と `cockpit.html` は [Three.js](https://threejs.org/) で3D描画＋Canvas 2D で HUD
- バックエンド／ビルド／npm 不要。各ページは単体の `.html` で完結

## ローカルで動かす

webカメラは `localhost` か `https` でしか使えないため、ローカルサーバー経由で開く。

```sh
# このディレクトリで
python3 -m http.server 8000
# Node 派なら: npx serve .
```

ブラウザで <http://localhost:8000> を開き、ゲームを選んで「スタート」→ カメラを「許可」。

## デプロイ（Cloudflare Pages）

静的ファイルをそのまま [Cloudflare Pages](https://pages.cloudflare.com/) にアップロードしている（[.assetsignore](.assetsignore) で `.claude` などを除外）。

```sh
npx wrangler pages deploy . --project-name=palmplay
```

→ デモ: <https://palmplay.syuhei176.com>（`palmplay` Pages プロジェクトにカスタムドメインを割当。`*.pages.dev` でも配信）

## 構成

```
index.html        ランチャー（トップページ）
racing.html       Hand Kart 3D（目玉）
cockpit.html      Hand Cockpit（目玉）
slash.html        Hand Slash
shooter.html / tamaire.html / ohajiki.html / gunsurvivor.html / freethrow.html
loading-*.png     ローディング画面のスプラッシュ画像
```
