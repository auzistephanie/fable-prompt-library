# CLAUDE.md — fable-prompt（Prompt Library Dashboard）

本 repo = Fable Prompt Compiler 嘅 Prompt Library **對外靜態 dashboard 網站**（`index.html`／`dashboard.html`），唔係 skill 正本，都唔係 Prompt Library 內容本身嘅正本。

## ⚙️ Standards（MANDATORY — 正本：`stephanie-personal/docs/ai-governance/06-STANDARDS.md`，改規則只改正本）

Push（`github_push.py` 永不 git CLI・HTTPS・一次 run 一 commit）・寫入分流（改動記錄 → `CHANGELOG.md` **頂部**，唔准 append 落本檔；本檔上限 100 行/6KB）・清理 mv `_to_delete/`・改舊檔先 `.bak-YYYYMMDD`・方向性決定先 preview・改完以用家身份 run 一次先報完成・governance 00–05（派 subagent 先讀 01+03；報完成前過 02 §R2；冇 mount stephanie-personal → 叫 Stephanie 連埋）。詳文＋例外表 → 正本。

## 文件路由（三個地方各管一件事，唔好搞錯分工）

- **本 repo**：淨係 `index.html`／`dashboard.html` 呢個對外 dashboard 靜態頁 + push script，冇 Prompt Library 內容檔案。
- **Skill 正本**（編譯 pipeline、觸發詞、quality-dna）：`stephanie-personal/.claude/skills/fable-prompt/`，唔喺本 repo，改 skill 邏輯要去嗰邊，唔好喺呢度改。
- **Prompt Library 內容**（`index.md`、`<類型>-<slug>.md`、`lessons.md`）：存喺 Fable Prompt project docs，唔喺本 git repo 檔案樹入面（待核實：實際存放路徑，README 冇列明）。

## 開工前防撞（session lock — 本 repo 2026-07-15 出過 concurrent-push overlap 事故）

任何 session（Cowork 或本機 Claude Code）開工前一定要跑：
```bash
bash "/Users/stephanieau/Desktop/Stephanie-Google Drive/dev/stephanie-personal/scripts/session-lock.sh" check "/Users/stephanieau/Desktop/Stephanie-Google Drive/dev/fable-prompt"
```
`CLEAR`／`EXPIRED` → 跟住行 `acquire` 先開工；`ACTIVE` → 停手話畀 Stephanie 知邊部機開緊工，唔好自己決定搶。收工／報「完成」前 `release`。正本 → `01-DISPATCH.md` §7。

## 架構／關鍵檔案

- root：`README.md`、`index.html`、`dashboard.html`（兩份現時都係 20897 bytes，`index.html` 改動時間較新——（待核實：邊份先係正本、兩者係咪要保持同步，README 冇提及））、`scripts/github_push.py`、`.env`、`.gitignore`。
- GitHub：`github.com/auzistephanie/fable-prompt-library`（依 `stephanie-portfolio` CLAUDE.md 記錄）。
- 部署：Vercel project `fable-prompt-library`（帳戶 `auzistephanie`）。**GitHub push 唔會自動觸發 Vercel deploy**——GitHub auto-deploy 試過，俾 sandbox 網絡限制擋住，已擱置；想 re-deploy 要 Stephanie 攞一次 Vercel token，cloud sandbox 唔保留 token。

## 開發

```bash
cd "/Users/stephanieau/Desktop/Stephanie-Google Drive/dev/fable-prompt"
python3 -m http.server 8935   # 本機開 index.html / dashboard.html 睇 render
```

## ✅ 完成前檢查（本 repo 專屬 DoD；通用四格 → 02-JUDGMENT §R2）

1. 改咗 `index.html`／`dashboard.html` → 瀏覽器實開嚟驗 render，唔准假設「改咗個 tag 應該得」
2. 同一次改咗兩份 html → 核對係咪要同步一致（見上面（待核實）；冇答案就問 Stephanie，唔好自己假設邊份係正本）
3. Push：`python3 scripts/github_push.py "<msg>"`＋核實 GitHub HEAD（→ Standards §S1）；記住 push ≠ deploy（Vercel 要另手動）
