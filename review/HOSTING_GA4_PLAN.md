# HOSTING + GA4 PLAN（秘密なし）

Date: 2026-07-15  
Agent: tsuki / Grok 4.5 field supervisor  
Scope: recruit-voice-web 恒久公開 + recruit-lp-v2 GA4

---

## 1. 現物調査結果（recruit-voice-web）

### 構成
| 項目 | 事実 |
|---|---|
| アプリ種別 | 静的HTML/JS + 薄い Node HTTP サーバー |
| 入口 | `server.js`（`http.createServer`） |
| ポート | **3101**（`start.ps1` コメントの 3100 は古い） |
| 静的配信 | `public/`（`index.html`, `app.js`） |
| API | `POST /token` のみ |
| 外部AI | xAI Realtime API（`api.x.ai`） |
| 秘密 | `XAI_API_KEY`（サーバー側のみ。ブラウザに出さない） |
| ブラウザ側WS | `wss://api.x.ai/v1/realtime?model=grok-voice-latest`（**サーバー経由ではなくブラウザ→xAI直接**） |
| サーバーWS/SSE | **なし**（HTTPのみ） |
| 状態保持 | なし（トークン発行は都度、通話状態はブラウザメモリ） |
| 常時プロセス要件 | node `server.js` + 公開用トンネル（cloudflared） |

### 通話フロー
1. LP → 通話ページ（同一タブ）
2. 通話ページが `POST /token` で ephemeral client secret を取得
3. ブラウザが xAI Realtime WebSocket に接続し音声会話
4. したがって **公開に必須なのは HTTP(S) 到達性**。公開経路自体に WebSocket 中継は不要（xAI向けWSはブラウザ直接）

### 調査時点の稼働
- `node server.js`（:3101）
- `cloudflared tunnel run kuro-line`（`line.kuro-ai.org` → 127.0.0.1:18790）※LINE代理。今回は非破壊維持
- 旧 quick tunnel `micro-tube-pace-tuning.trycloudflare.com`（一時）
- 既存ドメイン: **kuro-ai.org**（Cloudflare DNS、`line.kuro-ai.org` 稼働実績）

### package.json
- なし（素の Node 標準ライブラリのみ）

---

## 2. 恒久URL比較（実装適合性込み）

| 候補 | 月額目安 | 常時稼働 | コールドスタート | 秘密鍵 | 改修量 | 国内遅延 | 運用工数 | 音声本番適合 |
|---|---|---|---|---|---|---|---|---|
| **Cloudflare Named Tunnel + 独自サブドメイン（自宅Windows）** | **¥0**（Tunnel無料） | 可（PC/プロセス稼働時） | なし | ローカルENV | **最小**（DNS+config） | 良（NRT edge実績） | 低〜中 | **可。ただしPC依存** |
| 既存 quick tunnel (trycloudflare) | ¥0 | 不安定 | なし | 同上 | 0 | 良 | 低 | **本番不適**（URL変動・制限） |
| Railway / Fly / Render 常駐 | 約 $5–15/月 | 可 | 有料ならほぼなし（Render無料は15分sleep） | プラットフォームSecret | 中（デプロイ/ENV） | 海外寄り可 | 中 | 可（有料前提） |
| Cloudflare Workers | ¥0〜 | 可 | ほぼなし | Secrets | **大**（Node `http`/`https.request` をWorkers化） | 良 | 中 | 可能だが改修大 |
| CF Containers | 有料 | 可 | 低 | Secrets | 中 | 良 | 中 | 可だが新規課金 |

### 推奨（1つ）
**Cloudflare Named Tunnel + `voice.kuro-ai.org`（既存 kuro-ai.org）**

理由:
1. 既存資格（cloudflared login / cert / kuro-ai.org / NRT接続）で **追加課金・ドメイン購入なし**
2. 現行サーバー改修量ゼロ（HTTP reverse proxyのみ）
3. 音声の本丸WSはブラウザ→xAI直結なので、トンネルは「ページ配信 + /token」だけで足りる
4. Railway/Render/Flyは常時稼働に課金が要る。無料枠はコールドスタートで本番通話導線に不適
5. Workers化は動作可能だが、今の薄いNodeを書き直す必要があり過剰

### ただし重大リスク（正直評価）
Named Tunnel を **自宅Windows常駐**にする場合:
- PCスリープ/再起動/停電/Windows Update で **通話導線が落ちる**
- `node server.js` と `cloudflared` の2プロセス監視が必要
- これは「恒久URL」としては合格だが、「恒久可用性」としては **暫定本番**

**本番SLAを上げる次段（今回は未実施）:** 同じコードを Railway/Fly 常駐へ移し、`voice.kuro-ai.org` の向き先だけ切替。

---

## 3. 実装結果（Hosting）

### 実施済み
- Named Tunnel 作成: `recruit-voice`（ID: `cc8d0321-f2eb-4686-89f7-ceca486bddd1`）
- DNS CNAME:
  - `voice.kuro-ai.org` → 本トンネル
  - `call.kuro-ai.org` → 本トンネル（予備）
  - `recruit.kuro-ai.org` → 本トンネル（予備）
- 設定: `recruit-voice-web/cf_recruit_voice.yml`
- 稼働確認:
  - `https://voice.kuro-ai.org/` **200**
  - `POST https://voice.kuro-ai.org/token` **200**（value発行）
- 既存 `kuro-line` トンネル / 既存nodeプロセス方針: 非破壊維持
- LP 6ページの通話URLを `https://voice.kuro-ai.org/?src={lane}` に更新
  - lanes: main/grok/fugu/sol/terra/luna

### 注意（障害対応ログ）
- 作業中に旧 trycloudflare プロセスを誤停止 → quick tunnel は別URLで再起動済み
- 旧URL `micro-tube-pace-tuning.trycloudflare.com` は **もう使わない**（新恒久URLへ切替済み）
- 一時的に `server.js` が落ちていたため **3101 のみ再起動**（他プロセス非停止）

### 推奨公開URL
**https://voice.kuro-ai.org/**

---

## 4. GA4 調査・実装結果

### 既存探索
- リポジトリ / ワークスペースに **既存 Measurement ID（G-XXXXXXXX）なし**
- gog 認証アカウント: `roguresu001@gmail.com`
- 付与済みスコープ: gmail, calendar, chat, classroom, drive, docs, slides, contacts, tasks, sheets, people, forms, appscript
- **analytics / analytics.edit / analytics.readonly は未付与**
- gog に Analytics Admin コマンドなし
- よって API での GA4 プロパティ自動作成は **現状不可**
- ダミー Measurement ID の本番挿入は禁止のため **gtag 未挿入**

### 実装済み/未実装
| 項目 | 状態 |
|---|---|
| 既存GA4 ID探索 | 実施（見つからず） |
| GA4プロパティ作成 | **未実施**（権限不足） |
| gtag挿入 | **未実施**（ID未取得） |
| cta_click設計 | 設計済み（下記） |

### 取得後に入れる実装仕様（準備済み）
- 挿入位置: 各HTMLの `<!-- ANALYTICS_SLOT -->`
- 対象: root + grok/fugu/sol/terra/luna（6ページ）
- page_view: gtag 標準
- custom event: `cta_click`
  - `cta_type`: `call` | `line`
  - `lane`: `main` | `grok` | `fugu` | `sol` | `terra` | `luna`
  - `destination`: href
- 送らない: 氏名/電話番号/通話内容/PII

### 社長の最小1手（GA4）
1. ブラウザで https://analytics.google.com/ を開く  
2. 管理 → プロパティ作成  
   - 名前: `新滉建設 求人LP`  
   - タイムゾーン: `日本`  
   - 通貨: `JPY`  
3. データストリーム → ウェブ  
   - URL: `https://markun-japan.github.io/recruit-lp-v2/`  
4. 表示された **測定ID（G-XXXXXXXX）** をチャットへ貼る  

→ 受け取ったらこちらで6ページへ gtag + cta_click を即挿入・commit/push・Playwright検証する。

---

## 5. 差分・検証メモ

### LP更新
- 全通話CTAホスト: `https://voice.kuro-ai.org`
- `?src=` は各レーン維持（rootは `src=main`）
- LINE CTA不変: `https://lin.ee/XEVQvbw`
- 写真変更なし

### 疎通
- voice ページ 200
- token 200
- GitHub Pages 6URL は push後に再確認

### 残ブロッカー
1. Windows常駐依存（再起動耐性・監視・自動起動）
2. GA4 Measurement ID 未発行
3. 最終写真（指示どおり現状維持）
4. 旧 trycloudflare URL の完全退役周知

---

## 6. 結論

1. **推奨恒久URL: `https://voice.kuro-ai.org/`（Named Tunnel）**
2. **Hosting実装: 済み（DNS + tunnel + LP差し替え）**
3. **GA4実装: ID未取得のため未挿入。社長の測定ID共有が最小1手**
4. 音声本番として「安さ」は十分だが、可用性はPC常駐がボトルネック。次段は同一アプリのクラウド常駐移設を推奨。
