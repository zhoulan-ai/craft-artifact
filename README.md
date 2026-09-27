# 產成文物（craft-artifact）

一個 Claude Skill：把你跟 Claude 討論完的分析、企劃、系統說明或會議紀錄，產成一份**打開就看得懂的單檔 HTML 頁面**，叫做「文物」。

## 它解決什麼

跟 AI 討論完，結論常常散在一長串對話裡，要轉給同事或過幾天自己回頭看都很吃力。這個 Skill 讓 Claude 每次都用同一套結構產出：

- **結論放最前面**：不往下捲也知道整份在講什麼
- **數字都有出處**：推論會標「推論」，沒有真實數據就不放
- **顏色有固定意思**：琥珀＝現況、藍＝目標、紅＝落差與風險、綠＝已完成、紫＝只存在人腦裡的東西
- **能畫圖就不做表，能做表就不寫文字**：流程用圖、對照用表
- **每個步驟都寫「怎麼算做完」**
- **需要你做決定時，頁尾會有作答區**：直接點選項、寫補充，按「複製回覆」貼回對話

## 安裝

**claude.ai**
1. 下載 [craft-artifact.zip](https://github.com/zhoulan-ai/craft-artifact/raw/main/craft-artifact.zip)（不用解壓縮）。
2. 設定 → Capabilities → Skills → 上傳 skill，選這個 zip。
3. 在新對話裡說「產成文物 skill 的版本標記是什麼？」，回答「v3.2 公開版」就代表裝好了。

**Claude Code**
在終端機執行（所有專案都能用）：

```bash
git clone https://github.com/zhoulan-ai/craft-artifact.git ~/.claude/skills/craft-artifact
```

之後要更新，到那個資料夾執行 `git pull`。只想給單一專案用，就改放在專案的 `.claude/skills/` 底下。

## 怎麼用

討論告一段落後說：「**產成文物**」，或「做成一頁讓我看懂」。

Claude 會先判斷這次是診斷、企劃、系統說明還是紀錄，選對應的骨架，**分析做完才開始排版**。分析不夠時，它會先問你或先補分析，不會先做出一個好看但沒內容的頁面。

## 換成你自己的（客製點清單）

| 要改什麼 | 改哪裡 |
|---|---|
| 讀者是誰、用什麼語言、輸出放哪 | `SKILL.md` 最後一節「你的參數」 |
| 你習慣的觸發說法 | `SKILL.md` 開頭 description |
| 品牌色 | `assets/tokens.css` 開頭的 `:root`（五種語意的用途不要換） |
| 字體 | `assets/components.md` 第 9 節與 `tokens.css` 的 `font-family` |

## 檔案

| 檔案 | 內容 |
|---|---|
| `SKILL.md` | 規則本體：骨架、作答區、五個原則、自檢清單 |
| `assets/tokens.css` | 配色與基礎元件樣式 |
| `assets/components.md` | 各元件的 HTML／SVG 骨架：數據帶、泳道流程圖、步驟卡、作答區等 |
| `LICENSE` | 授權聲明 |
| `craft-artifact.zip` | 上面這些檔案打包好的版本，給 claude.ai 上傳用 |

## 作者

周浪 Lan，協助工作室把營運導入 AI 協作。我自己是 [STRONG FLOW 純浪力量](https://strongflow.tw)共同創辦人，在台南經營兩間重量訓練與器械皮拉提斯工作室；這份 Skill 是我們把工作室營運交給 AI 協作之後，每天實際在用的其中一份。

- 更多 Skill：[github.com/zhoulan-ai](https://github.com/zhoulan-ai)
- 想讓你的工作室也這樣運作：[ji3g4106@gmail.com](mailto:ji3g4106@gmail.com)
- 官網：[https://strongflow.tw](https://strongflow.tw)

## 授權

[CC BY 4.0](https://creativecommons.org/licenses/by/4.0/deed.zh-hant)：可以自由使用、修改、轉傳，包含商業用途。轉傳或改作時，請標註：

> 原作：周浪 Lan｜STRONG FLOW 純浪力量（https://strongflow.tw）
