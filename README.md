# Fable Prompt Compiler — 系統總覽

最後更新：2026-07-12

## 呢個係咩

一個 loop-engineering 驅動嘅 prompt 編譯器：Stephanie 喺 Fable Prompt project 度打一句平時嘅 idea，Claude（透過 `fable-prompt` skill）自動編譯成一條可以直接 copy 落 Opus/Sonnet 用嘅高質量 prompt，並可以存入 Prompt Library、喺網上 dashboard 瀏覽。

## 組成部分

### 1. Skill：`fable-prompt`
安裝喺 Cowork skill 目錄（唔係 project doc，日後 session 需要重新確認佢存在）。

**編譯 pipeline（4 個階段，每次都會跑）：**
1. **Intent Parse** — 判斷屬於邊類（寫作/內容、Code/網頁、分析/研究、文件/簡報），讀對應 pattern 檔案 + `quality-dna.md` + project 入面嘅 `lessons.md`
2. **Spec Expansion Loop** — 補晒所有規格 slot（受眾、語氣、結構、長度、禁止清單），冇講嘅位用最大機率預設並列做 assumption；只有真正有分歧先問一條問題
3. **Prompt 組裝** — 固定結構：角色／任務／規格／質量標準 Rubric／**Self-Refine Loop**（逼目標 model 自評自改先出街）／輸出格式
4. **Critique Loop** — 出街前用 3 個角度（歧義／漏 spec／rubric 具體度）自我攻擊，最多改 3 輪

觸發詞：「prompt:」「幫我整條 prompt」「編譯」「變做 prompt」，或喺呢個 project 度打任何 task idea（預設當你想要 prompt，唔係想要成品）。

### 2. Prompt Library（project docs）
- `prompt-library/index.md` — 索引表 + 網站連結
- `prompt-library/<類型>-<slug>.md` — 每條 prompt 一個檔（原始 idea、完整 prompt、assumptions、評分、效果筆記）
- `prompt-library/lessons.md` — 進化機制沉澱位

而家有 3 條 prompt：LinkedIn post（v2，已進化，★★★★☆）、定價分析（v1，未評）、IG Reels（v1，未評）。

### 3. Dashboard（正式網站）
🌐 **https://fable-prompt-library.vercel.app**（Vercel project `fable-prompt-library`，帳戶 `auzistephanie`）

**已知限制**：Cloud sandbox 唔保留 Vercel token，每次入庫/進化想 re-deploy 要 Stephanie 攞一次 token。GitHub auto-deploy 曾經試過但俾 sandbox 網絡限制擋住，已擱置。

### 4. 本機檔案
存喺 `~/Desktop/Stephanie-Google Drive/dev/fable-prompt/`（呢個 dashboard.html 就係一份靜態備份）。

## 用法快速參考

| 你講 | 會發生咩事 |
|---|---|
| 打一句 idea | 編譯出一條 prompt，附 assumptions |
| 「入庫」 | 存入 Prompt Library |
| 「換題重用」 | 攞返舊 prompt 結構，換題 |
| 「呢條出得好/唔好，因為…」 | 進化：更新 prompt + 記低教訓 |
| 「update dashboard」 | 重新產生網站（需要 Vercel token） |
