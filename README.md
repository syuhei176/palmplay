# 手・指で遊ぶ webカメラゲーム 🖐️

webカメラで手・指の動きを検知して遊ぶゲーム集。バックエンド/ビルド不要。

- **[index.html](index.html) — Hand Slash 🍉**: 人差し指を振って果物を斬るフルーツニンジャ風。💣 を避けて60秒スコアアタック。最大4手の協力プレイ対応。
- **[shooter.html](shooter.html) — Shuriken Shooter 🥷**: 奥から迫る敵 👹 を手裏剣で撃つシューティング。👌 つまんで離すと発射。遠近スケーリングで奥行きを表現。両手対応。
- **[racing.html](racing.html) — Hand Racer 🏎️**: 両手でハンドルを握って回すと曲がれる擬似3Dレース。🪙 を集めて 🚧 を避け、60秒で距離を稼ぐ。アクセルは自動。
- **[tamaire.html](tamaire.html) — Tama-ire 🧺**: 足元の紅白玉を手ですくって弾き、左右に動くカゴに入れる玉入れ。手のひら全体（21点）が当たり判定。両手OKの60秒スコアアタック（ベストスコア保存）。
- **[ohajiki.html](ohajiki.html) — Ohajiki Battle 🔵🔴**: 2人対戦のはじき出しおはじき。👌 自分の色の玉をつまんで振って離すと弾き飛ぶ。相手の玉を盤外へ落とせ。左の人＝青／右の人＝赤、90秒で残数勝負。
- **[gunsurvivor.html](gunsurvivor.html) — Gun Survivor 🔫🧟**: 指ガンで撃つガンサバイバー風レールシューター。👉 人差し指で照準・👍 親指を倒すと発砲、頭を撃てば一撃ボーナス。弾切れは画面下を狙ってリロード。One Euro Filter＋エイムアシストで“狙える感”を出した体力サバイバル（ベストスコア保存）。
- **[freethrow.html](freethrow.html) — Free Throw 🏀**: バスケのフリースロー。ボールを持って実際にシュートするように手を振り上げて放つ。振り上げの速さ＝アーチの強さ（左ゲージの緑が適正）、手の左右＝狙い。放物線で奥のゴールへ。スウィッシュ✨・バンク🟦判定＆連続で倍率UP、60秒チャレンジ（ベストスコア保存）。
- **[cockpit.html](cockpit.html) — Hand Cockpit ✈️**: コックピット視点の3Dフライト（Three.js）。✊左手＝スロットルレバー（上げて加速）、✊右手＝操縦桿（手前に引く＝機首上げ／左右に振る＝バンク旋回）。Vrまで加速→ROTATEで離陸、その後は**自由飛行**。窓の外には自機の機首・回るプロペラ・主翼が見え、テクスチャ地面・滑走路・雲・太陽でリアルな空に。旋回して**出発した滑走路へ帰投**し、**PAPI／ND（ナビ表示）**を見ながら降下して**🛬着陸**（接地の降下率でGREASER/FIRM/HARDを採点）。失速・ハードランディング・墜落注意。カメラ無しでもキーボード（W/S・↑/↓・←/→）で操作可。

## 技術
- [MediaPipe Hand Landmarker](https://ai.google.dev/edge/mediapipe) … ブラウザ上で動く手検出AI（CDN読み込み）
- Canvas 2D … 描画・当たり判定（`cockpit.html` のみ [Three.js](https://threejs.org/) で3D描画＋Canvas 2DでHUD）
- **バックエンド/ビルド不要。`index.html` 1枚で動作**

## 遊び方（起動）
webカメラは `localhost` か `https` でしか使えないため、ローカルサーバー経由で開く。

```sh
# このディレクトリで
python3 -m http.server 8000
```

ブラウザで <http://localhost:8000> を開き、「スタート」→ カメラを「許可」。

> Node派なら `npx serve .` でもOK。

## 操作
- 人差し指の先を素早く動かして果物を斬る（ゆっくりだと斬れない）
- 連続で斬るとコンボでスコアUP
- 💣 を斬るとライフ -1（3つでゲームオーバー）

## 調整したい場合（`index.html` 内）
- `GRAVITY` … 果物の飛ぶ高さ・落下速度
- `spawnObject()` の `isBomb` 確率 … 爆弾の出現率
- スポーン間隔 `interval` … 難易度カーブ
- `numHands` … 検出する手の数
