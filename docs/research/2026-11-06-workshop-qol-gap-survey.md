# RimWorld QoL MOD 空白領域調査

調査日: 2026-11-06（数値はすべてこの日に Steam Workshop から取得）
対象: RimWorld（appid 294100）の Steam Workshop。手元の本体は R2 の `1.7.4985 rev1269`

---

## 結論

1. **新しいQoL MODを作る余地はある。** 1.6公開（2025-07-11）より後に新しく作られたQoL MODが、1年余りで10万〜22万の購読者を集めている。ただし、思いつきやすい機能はほぼすでにある。差がつくのは「バニラのUIを作り直す」「既存MODを高速な形で一から書き直す」といった方向。
2. **長く更新されていないMODを組み合わせて作り直すこともできる。** ただし対象は思ったより少ない。有名な放棄MODの多くは、有志がすでに継続版を出している（1.7対応済みのものも多い）。いま実際に空いているのは次の二つ。
   - **継続版の作者まで更新を止めた「二重の放置」**：Owlchemist の元MOD → FerrisCG の継続版、という系統。
   - **後継のない1〜3万購読規模の小さなUI系MOD**
3. **一番のねらい目は「UI・表示・通知」系をまとめたスイート（複数機能をまとめたMOD）。** 1.7（Waylithエンジン）で壊れたという報告が集中しているのはUI層で、その中に作者が止まっているMODがある。
4. **コードを流用できるかどうかはライセンス次第。** 改変禁止（CC BY-NC-ND）のMODもある。ライセンスが書かれていないものは、一から書き直す前提で考える。

---

## 1. 前提：1.7の現状

- 2026-10-12 に Ludeon が **Update 1.7 を発表**。Unity から自社製の **Waylith Engine** へ移行した。公式発表では、速度は2〜4倍、「ほとんどのMODは無修正で動く」「黄色の警告はバージョン番号が変わっただけ」。発表時点では **unstable ベータブランチのみで、メインは1.6のまま**。その後（〜10-26）の公式告知に、メインブランチへの配信の発表は見当たらない。
- Workshop 全体：表示対象 64,932件。`Mod`＋`1.6` タグが **25,789件**、`Mod`＋`1.7` タグが **9,303件**（発表から約3.5週間）。
- 1.7タグが付いていない＝壊れている、ではない。人気作者の中には「1.7が正式公開されたら正式対応する」と書いている人もいる（RimHUD の作者コメント）。古いMODに1.7タグだけ付ける Mlie の **No Version Warning**（16.6万購読）もある。

### 1.7で実際に壊れたという報告（コメント欄、2026-10-12以降）

| MOD | 購読者 | 報告内容 |
|---|---:|---|
| Allow Tool | 1,388,841 | 「1.7 has broken this mod」「My gizmos are gone under 1.7」 |
| Toggleable Readouts Continued | 84,874 | UIが消え、`GUIContent.m_Text` のエラーが連続して出る |
| Toggleable Overlays Continued | 78,949 | 有効にするとUIが出なくなり、操作できない |
| Door Clearance Continued | 83,695 | 1.7.4984 でエラー（ログ付きの報告） |
| Defensive Positions | 627,900 | 「not working in the 1.7 beta」 |
| Hunt for Me | 141,334 | 「Broken in 1.7 beta」 |
| Prepatcher | 359,991 | 動かない → Performance Fish や MultiFloors も道連れ |
| Graphics Settings+ | — | Waylith上でテクスチャ読み込みが null を返す（RimHUD のコメント欄の報告） |

ただし、コミュニティの動きはとても速い。数日で非公式の1.7版が出ている：
- Achtung! 1.7（10-23）
- EdB Prepare Carefully Expanded (1.7)（10-27）
- Hunt for Me (Unofficial 1.7)（10-31）
- Smart Farming 1.7（11-03）
- Defensive Positions (1.7 Fix)（11-05）
- While you're up 1.7（11-05）

Allow Tool には直接の1.7移植版がない。代わりに、一から書き直された **Keyz' Allow Utilities**（84,701購読・1.7対応）が受け皿になっている。

---

## 2. 調査方法と範囲

1. Workshop の閲覧ページ（総購読者数順）から **上位7,500件**（全期間の購読者がおよそ2.1万以上）を取得。`GetPublishedFileDetails` で説明文全文も取得した。うち MOD は 6,685件。
2. 対応バージョンタグの最大値が1.5以下のMOD（2,201件）について、QoLらしさをキーワードで点数化し、目視でQoL系の **133件** を選んだ。
3. 133件それぞれを、1.6タグ・1.7タグ付きで Workshop 検索し、題名の似た後継版を照合。
4. 後継版が見つからなかったものと、1.6止まりの人気QoL MOD 70件は、**コメント欄（最新60件）** を取得した。代替MODへのリンク、1.7で壊れたという報告、更新を求める声を確認した。
5. 継続版の作者ごとに、最後の更新日と1.7タグの有無を集計した。

---

## 3. Q1：新しくQoL MODを作る余地

### 根拠1：1.6以降に作られた新しいQoL MODが伸びている

上位7,500件のうち1.6以降に作られたMODは1,115件。キーワード判定でQoLらしいものは225件あり（RimTalk のようなQoLでないものも少し混ざる）、そのうち題名が継続版らしいものは29件だけ。**残り約9割は新規作品**。

| MOD | 購読者 | 作成日 | 内容の方向 |
|---|---:|---|---|
| Nice Plants Menu | 219,926 | 2026-03-14 | 栽培メニューの情報を見やすく作り直し |
| Nice Inventory Tab | 190,211 | 2025-11-21 | 持ち物タブを作り直し |
| Loading Progress | 172,282 | 2025-07-27 | 起動の各段階の進み具合を表示 |
| Better Architect Menu | 120,258 | 2025-09-07 | 建築メニューにサブカテゴリと並べ替えを追加 |
| Mine Sight | 103,761 | 2026-07-22 | 採掘指定中に鉱石を強調し、鉱脈をまとめて指定 |
| Resource Delivery Helper | 97,776 | 2026-04-01 | 設計図に重ねると必要資材を表示 |
| Health Display | 95,015 | 2025-07-11 | 健康タブの上に状態を図で表示 |
| Keyz' Allow Utilities | 84,701 | 2025-07-13 | 既存の大型MOD（Allow Tool）を一から高速に書き直し |
| Architect Menu Optimizer | 83,525 | 2026-04-02 | 大量MOD環境での建築メニューの描画を軽くする |
| Clean Command Bar / Clean Research Sort | 59,513 / 58,974 | 2026 | ボタンが多すぎる下部バーの整理 / 研究ツリーの自動整列 |

（Perspective Shift〔104,855〕も1.6以降の作品だが、WASDで操作するアドベンチャーモードでQoLではないため、表から除いた。）

伸びている作品には共通点がある。**バニラのUI（メニュー・タブ・バー）を、情報量や使いやすさの面で作り直すこと**と、**定番機能や重い画面を高速に書き直すこと**である。

### 根拠2：ただし、競争は激しい

- 「quality of life」の1.7タグ付き検索だけで 1,128件ある。
- **Mlie** が上位7,500件のうち340件を持ち、そのうち272件が継続版。1.7タグ付きはすでに205件、現在の購読者は合計約1,000万。人気MODが放置されても、すぐに誰かが引き継ぐ構造になっている。
- 1.7で壊れたMODも、上の通り数日で非公式版が出ている。「1.7で壊れたから空いた」という状況は長く続かない。

---

## 4. Q2：長く更新されていないMODを組み合わせて作り直す

### 4-1. 有名な放棄MODの多くは、すでに継続版がある

133件中 **94件** に、購読者1,000以上の後継版（1.6／1.7タグ付き）が見つかった。そのうち **60件** は後継版がすでに1.7タグ付き。

| 元のMOD（最終対応） | 後継版 | 購読者 | 1.7 |
|---|---|---:|:-:|
| Replace Stuff（1.5） | Replace Stuff - Continued | 522,879 | ✓ |
| Search and Destroy（1.4） | Search and Destroy (Continued) | 265,006 | ✓ |
| QualityBuilder（1.5） | QualityBuilder Unofficial 1.6 | 211,597 | ✓ |
| Smart Medicine（1.5） | Smart Medicine - Continued | 190,810 | ✓ |
| Smarter Deconstruction（1.4） | …(Continued) | 167,526 | ✓ |
| Blueprints（1.5） | Blueprints Forked - 1.6 / Universal Blueprints | 208,715 / 83,665 | ✗ / ✓ |
| Medical Tab / Work Tab / Colony Manager（1.4） | Continued / Continued / Redux | 4.5万 / 4.9万 / 4.4万 | ✓ / ✗ / ✓ |

**ここを作り直しても勝ち目は薄い。**

後継版のない39件のうち、残りの多くは次のどれかに当たる。
- **バニラに取り込まれた**（作者やユーザーの記述による）：Share The Load（1.5）、Show Draftees Weapon（1.4）、Conduit Deconstruct（1.6）、Simple Search Bar（1.3）、Ruined by temperature filter（1.6）。Where is my weapon? は1.5で部分的に取り込まれたが、うまく働かないことがあるらしい（Forced Rearmament の説明文による）。
- **機能の違う代替MODに置き換わった**：
  - Keep Bed Ownership → Sensible Bed Ownership（7.8万）
  - Startup impact → Loading Progress（17.2万・1.7）
  - Textile Stats → Stuff List (Continued)（4.6万・1.7）
  - Convert Then Recruit → Custom Prisoner Interactions（5.1万）
  - Improve This → Simple Improve（6.7千）
  - Where is my weapon? → Forced Rearmament（2.2万・1.7）

### 4-2. 実際に空いているもの（A）：継続版も放置されている

継続版の作者 **FerrisCG** は、**最後の更新が 2025-07-28**。上位7,500件に18件あるが、**1.7タグ付きは0件**、プロフィールはオフラインのまま。元はすべて Owlchemist のMODで、ソースは GitHub（`github.com/Owlchemist/...`）にある。

| 継続版 | 購読者 | 1.7での状況 | 別の1.7版 |
|---|---:|---|---|
| Smart Farming Continued | 147,514 | 「1.7?」の声 | Smart Farming 1.7（262購読、11-03） |
| Mid-Save-Saver Continued | 123,419 | 1.7で動作報告あり | なし |
| Toggleable Readouts Continued | 84,874 | **壊れている（UIが消える）** | **なし** |
| Door Clearance Continued | 83,695 | **エラー報告あり** | **なし** |
| Toggleable Overlays Continued | 78,949 | **壊れている（UIが出ない）** | **なし** |
| Toggleable Shields Continued | 64,494 | 不明 | なし |
| Signs and Comments Continued | 19,462 | — | …Fixed Fixed（1.2万・1.7） |
| Clean Pathfinding 2 Continued | 50,775（1.5止まり） | — | [1.6/1.7] Fork（1.6万） |

なお、Door Clearance は放置された **Don't Block Door**（201,016購読）の受け皿にもなっている。Don't Block Door のコメント欄では、1.7で壊れたという報告と、Door Clearance を勧めるリンクが何度も出てくる。

### 4-3. 実際に空いているもの（B）：後継のない小さなUI系MOD

| MOD | 購読者 | 最終対応 | 状況 | ライセンス表記 |
|---|---:|---|---|---|
| Begone, Message!（メッセージを右クリックで消す） | 32,649 | 1.4 | 1.6で「便利」「動かない」の両方の報告。後継なし | GitHub にソース（ライセンス未確認） |
| CorpseTab（死体一覧タブ） | 30,080 | 1.4 | 1.6／1.7で動作報告あり（NVW の一覧に掲載） | **CC BY-NC-ND 4.0（改変禁止）** |
| Compatibility On Hover | 28,881 | 1.5 | 1.6で動作報告あり | CC BY 4.0 |
| Vanilla UI Expanded（UIの総合MOD） | 26,522 | 1.3 | 「今でも恋しい」という声。部分的な代替のみ | CC BY-NC-SA 4.0 |
| SlaveBar（コロニストバーの表示切替） | 24,973 | 1.5 | 1.7で「まだ動く」報告と「切替が効かない」報告 | 表記なし |
| Fixable Mood Debuffs Alert | 16,420 | 1.4 | 代替の Mood Alerts（7千・1.6止まり） | **MIT（流用歓迎と明記）** |
| Research Info | 12,849 | 1.4 | 代替の Show Research ETA（5.4千・1.6止まり） | GitHub（ライセンス未確認） |
| Weight price（重さあたりの価格） | 12,018 | 1.4 | 後継なし | 表記なし |
| Show Fertility on Health Tab | 11,538 | 1.4 | 1.7で「健康タブが空になる」報告あり | 表記なし |
| WM Smarter food selection | 8,848 | 1.2 | 「動物の食事を制御する代替がない」という声 | 表記なし |

（NVW = No Version Warning）

---

## 5. 推奨：作るなら何を組み合わせるか

### 案1（第一候補）：UI・表示・通知の総合QoL MOD

組み合わせる機能：
- Toggleable Readouts：左上の資源一覧を絞り込み、描画も軽くする
- Toggleable Overlays：ラベルをマウスを重ねたときだけ表示
- Begone, Message!：メッセージを右クリックで消す
- Fixable Mood Debuffs Alert：すぐ直せる気分低下の警告
- Show Fertility on Health Tab：健康タブに妊孕性を表示
- Research Info：研究台に研究の進み具合と残り時間を表示
- Weight price：取引・キャラバン画面に重さあたりの価格を表示

この組み合わせを勧める理由：
- 元のMODと継続版の作者がどちらも止まっていて、1.7用の代替が見つからない（Toggleable 系）。
- Waylith で壊れやすいのはUI層で、壊れたという報告もここに集まっている。
- どの機能も規模が小さく、一人で長く保守できる。
- 伸びている新作MOD（Nice ○○ Tab 系など）と同じく「バニラUIの改善」の流れに乗れる。

**機能ごとに個別にオン・オフできることは必須。** Vanilla UI Expanded の作者も、作り直しの最優先事項として「各モジュールを個別に切り替えられること」を挙げていた。

### 案2：ドア・物の置き場所

Door Clearance の機能（ドアのマスに物を置かない）を一から書き直す。購読者の合計が大きい（Don't Block Door 20万＋Door Clearance 8.4万）。ただし機能が1つだけなので、総合MODに入れるより単独で出すほうが探されやすい。

### 避けるべきもの

Replace Stuff、Smart Medicine、Work Tab などの作り直し。どれもすでに継続版があり、作者も活動中なので、重複するだけになる。

---

## 6. 法的・実務上の注意

- **CC BY-NC-ND**（Don't Block Door、CorpseTab）は改変物の配布を禁じている。コードも画像も使わず、機能だけを独自に書き直すこと。
- **ライセンスが書かれていない**MODは、権利者がすべての権利を持っている前提で扱う。流用せず、一から書き直す。前例もある。
  - Keyz' Allow Utilities：説明文に「not a fork… from scratch implementation」と明記
  - Simple Improve：「ライセンスがないので完全に独自のコードで書いた」とコメントで説明
- **MIT**（Fixable Mood Debuffs Alert）や **CC BY**（Compatibility On Hover）は、著作権表示とライセンス表示を残せば流用できる。Where is my weapon? は「CC BY-NC-SA」と「MIT」を併記しているが、どちらがコードに適用されるかは説明文からは読み取れない。**CC BY-NC-SA**（Vanilla UI Expanded）は非営利・同一ライセンスの条件付きで流用できる。
- GitHub のリポジトリのライセンス（Owlchemist、Begone Message、Research Info など）は、**このセッションでは確認していない**。流用する場合は、各リポジトリの LICENSE を確認すること。
- 継続版の多くは「元のMODと同じ packageId を使う」方式をとっている。自作の総合MODでは、元のMODや継続版を `incompatibleWith` に入れて、同じ処理が二重にかからないようにする。

---

## 7. 確かさと限界

- 調べたのは上位7,500件（全体の約12%）だけ。小さなMODの中の空白は見ていない。
- QoL系の判定はキーワードと目視によるもので、見落としがありうる。
- 後継版の判定は、題名の類似とコメント欄のリンクに基づく。名前のまったく違う代替は見落としている可能性がある。
- 「1.7で壊れた」はユーザーのコメントによる報告で、ゲームを起動して確かめてはいない。
- バニラに取り込まれたかどうかは、作者やユーザーの記述によるものが中心。R2の静的索引で `Verse.Message` のクリック処理を調べたが、右クリックで消す機能がバニラにあるかは確定できなかった。

---

## 出典

- Ludeon 公式告知「Announcing the Waylith Engine and Update 1.7」（2026-10-12）: https://steamstore-a.akamaihd.net/news/externalpost/steam_community_announcements/1846018067941786
- Steam Workshop（RimWorld）: https://steamcommunity.com/workshop/browse/?appid=294100
- Workshop の各MODページ: `https://steamcommunity.com/sharedfiles/filedetails/?id=<ID>`
  - Toggleable Readouts Continued 3261317086
  - Toggleable Overlays Continued 3261316725
  - Door Clearance Continued 3261310587
  - Don't Block Door 1691076769
  - Allow Tool 761421485
  - Keyz' Allow Utilities 3524716849
  - Begone, Message! 1951637504
  - SlaveBar 3019111152
  - Fixable Mood Debuffs Alert 1307316672
  - Show Fertility on Health Tab 2879306896
  - Research Info 2290462337
  - Weight price 2363887111
  - No Version Warning 2599504692
- R2 `rimworld-17/research/vanilla-1.7.4985-audited/`（本体のバージョン確認、`Verse.Message` の静的呼び出しの確認）
