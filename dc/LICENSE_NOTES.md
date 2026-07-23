# DCレーン 素材ライセンス台帳

取得日: 2026-07-23  
更新: 2026-07-23（v2.1 社長FB反映・再走）  
用途: 箕面DC採用LP（recruit-lp-v2/dc）作業風景イメージのみ  
注意: 作業風景はすべて「※写真はイメージです」表示。実在DC事業者の特定に使える写真は不使用。

---

## 1. 作業風景（dc/img/）— v2.1 採用

| ファイル | 取得元 | ライセンス | 条件 | 取得日 | 用途 |
|----------|--------|------------|------|--------|------|
| hero_electrical.jpg | AI生成（openai/gpt-image-2） | 生成物・社内利用 | プロンプト概要: 建設中建物内部・天井ケーブルトレイに色付き電気ケーブル・明るい自然光・人物なし・ロゴなし・文字なし・日本の現場風。候補複数からケーブル密度が高く一目で電気工事と分かる1枚を採用しJPEG化 | 2026-07-23 | FVヒーロー |
| hero_elec_cables.jpg | AI生成（openai/gpt-image-2） | 同上 | プロンプト概要: 同上系統。トレイにケーブル束が載った建設中屋内。WORKモザイク用 | 2026-07-23 | 仕事内容 |
| work_cable_tray.jpg | AI生成（openai/gpt-image-2） | 同上 | プロンプト概要: カーブするメタルケーブルトレイ＋カラーケーブル、建設中の商業建物内、人物なし | 2026-07-23 | 仕事内容ワイド |
| work_panel_v21.jpg | AI生成（openai/gpt-image-2） | 同上 | プロンプト概要: 建設現場の分電盤／配線準備・整理された電線と電線管・明るい屋内・人物顔なし・ロゴなし・文字なし。JPEG化 | 2026-07-23 | 仕事内容（盤） |
| work_cable_pull_v21.jpg | AI生成（openai/gpt-image-2） | 同上 | プロンプト概要: 建設中屋内でケーブルトレイへ色付きケーブルを通す手元（顔なし）・仮設照明・ロゴなし・文字なし。JPEG化 | 2026-07-23 | 仕事内容（通線） |
| work_wires_hand.jpg | https://www.pexels.com/photo/257736/（images.pexels.com/photos/257736/…） | Pexels License | 無料・商用可・クレジット不要（任意推奨）。再販・無償再配布制限あり。手元と盤は写るが顔なし | 2026-07-23 | 仕事内容（盤・配線） |

### 補助生成物（採用候補・残置、HTML未使用可）
| ファイル | 取得元 | 備考 |
|----------|--------|------|
| hero_electrical_v21.jpg / hero_elec_a〜e.png | AI生成 | ヒーロー選定用バリエーション |
| work_cable_tray_v21.jpg/.png | AI生成 | トレイ候補 |
| work_cables_close_v21.jpg | AI生成 | クローズアップ候補 |
| work_cable_tray2.jpg / work_site_bright.jpg | AI生成 | v2.1初期候補。最終モザイクでは panel / pull を優先 |

### ライセンス原文リンク
- Unsplash License: https://unsplash.com/license
- Pexels License: https://www.pexels.com/license/

### 加工方針（v2.1）
- ヒーロー／WORKのダークオーバーレイを軽量化（明るい印象を優先、文字可読性はグラデ下端で維持）
- CSSで軽い彩度・コントラスト調整のみ
- HTML上に「※写真はイメージです」を必ず表示
- 顔がはっきり写るもの・実在DC事業者ロゴが特定できるものは不使用（盤写真のメーカー刻印は許容範囲で使用）

---

## 2. v2.0 で使用・v2.1で不使用（ファイルは残置）

| ファイル | 取得URL | ライセンス | 備考 |
|----------|---------|------------|------|
| hero_server.jpg | Unsplash photo-1558494949-ef010cbdcc31 | Unsplash License | 暗いサーバルーム。v2.1ヒーロー不採用 |
| work_rack.jpg | Unsplash photo-1597852074816-d933c7d2b988 | Unsplash License | HDD寄り。WORKから外す |
| work_cables2.jpg | Pexels 325229 | Pexels License | サーバルーム列。WORKから外す |
| work_cables3.jpg | Pexels 2881229 | Pexels License | NWパッチ寄り。補助候補として残置 |
| work_server2.jpg | Pexels 1148820 | Pexels License | サーバー列。WORKから外す |

---

## 3. 自社写真（相対参照 ../assets/）— v2.1 参照

既存レーン共通アセット。ライセンスは自社撮影・既存運用に準拠。  
**assets本体は変更しない。**

| 参照パス | 用途 | 選定理由 |
|----------|------|----------|
| img/dorm_room.jpg（元: ../assets/osaka_v2_room_c.webp） | 寮個室（主力） | 部屋全体が分かるワイド。文字オーバーレイなし。dc/imgへJPEGコピー |
| img/dorm_meal.jpg（元: ../assets/osaka_v2_meal_c.webp） | 食事 | 文字なしの食事セット |
| img/dorm_sauna.jpg（元: ../assets/osaka_v2_sauna_b.webp） | サウナ | 木製サウナ室内が明確。**文字バッジなし**（sauna_aはラベル付きのため不採用） |
| img/dorm_gym.jpg（元: ../assets/osaka_v2_gym.webp） | 筋トレルーム | 寮アメニティ追加。顔なし |
| ../assets/dog.jpg | 看板犬 | **小タイルのみ・ヒーロー禁止** |
| ../assets/building.jpg | 会社外観 | 会社セクション主力 |
| img/life_meal.jpg（元: ../assets/osaka_v2_meal_a.webp） | 会社セクション補強 | 食事付きの訴求（小バッジあり） |
| img/life_facility.jpg（元: ../assets/osaka_v2_facility_ad.webp） | 会社／暮らし補強 | シャワー・サウナ入口。顔なし（募集バッジあり・設備実写として使用） |

### v2.0から差し替えたもの
- room_v2.jpg → アップすぎで部屋全体が不明 → osaka_v2_room_c.webp
- hero_sauna_v2.jpg → サウナ判別が弱い疑い → osaka_v2_sauna_b.webp（明確なサウナ室内・文字なし）
- meal_v2.jpg → osaka_v2_meal_c.webp（同等クリーン）

---

## 4. 不使用とした候補
- 写真AC: ログイン必須のためスキップ
- 顔が判別できる職人ストック（Unsplash電気工など）: 不使用
- osaka_v2_* の文字入り meal_collage / gym_ad / room_ad 等: 数字・他現場条件が混ざるため主力不採用（facility_adは設備実写として会社補強のみ）
- dog のヒーロー配置: 禁止維持
