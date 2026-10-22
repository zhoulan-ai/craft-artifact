# 元件骨架與使用規則

搭配 `tokens.css` 使用。每個元件都附「什麼時候用」——用錯地方比不用更傷。

## 目錄
1. 頁面骨架
2. 數據帶 stats
3. 泳道流程圖（現況推導用）
4. 鏈狀覆蓋圖（目標對照用）
5. 步驟卡 steps
6. 對照表與映射表
7. 重點框 callout
8. 可複製區塊 prompt
9. 字體引入
10. 作答區（要他拍板時）

---

## 1. 頁面骨架

```html
<nav><div class="wrap">
  <a href="#s1">① 章節名</a><a href="#s2">② 章節名</a>
</div></nav>

<header><div class="wrap">
  <p class="kicker">資料來源與範圍，一行</p>
  <h1>主標題，可換行</h1>
  <p class="lead">一句話結論：讀者不往下捲也知道整份在講什麼。點出核心矛盾或最重要的判斷，不是內容簡介。</p>
  <div class="stats">…數據帶（見 2）…</div>
</div></header>

<section id="s1"><div class="wrap">…</div></section>

<footer><div class="wrap">
  推導依據：（列出資料來源與筆數）。所有數字皆由資料計算得出；標示「需確認」者為資料無法單獨證實的推論。
</div></footer>
```

## 2. 數據帶 stats

什麼時候用：有 4～6 個「算得出來」的全局數字時。沒有真實數據就整個不放。

```html
<div class="stats">
  <div><b>102</b><span>指標名稱</span></div>
  <div><b>586 / 213 / 6</b><span>複合指標可用斜線</span></div>
  <div><b>0%</b><span>反常的數字放最後，製造懸念</span></div>
</div>
```

## 3. 泳道流程圖（SVG）

什麼時候用：要呈現「資訊在誰手上流動、在哪裡斷掉」。診斷型文物的招牌元件。
規則：
- 泳道由上而下＝資訊流向（例：客人 → 外部工具 → 我們的系統 → 人腦）。
- 「人腦／對話」永遠是最下面一條紫色道——沒有系統承接的事都放這裡，這是整張圖的洞察來源。
- 實線箭頭＝真實資訊流；**紅色虛線＝斷點**，一張圖最多 1～2 條，配一句紅字說明。
- 每個框：粗體主文字＋一行灰色補充。框寬 120–170，高 50–58。
- 圖下方必配 `.cap`，一句話講「這張圖要你看見什麼」。

骨架（依實際內容增減泳道與節點；lane 高度 110～150）：

```html
<div class="flow">
<svg viewBox="0 0 1000 520" xmlns="http://www.w3.org/2000/svg" role="img" aria-label="現況工作流程泳道圖">
  <defs>
    <marker id="ar" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0 0L10 5L0 10z" fill="#5F6673"/></marker>
    <marker id="arr" viewBox="0 0 10 10" refX="9" refY="5" markerWidth="7" markerHeight="7" orient="auto-start-reverse"><path d="M0 0L10 5L0 10z" fill="#C8102E"/></marker>
  </defs>
  <style>
    .lane{fill:#fff;stroke:#D5D9E0}
    .lanel{font:700 14px 'Noto Sans TC',sans-serif;fill:#1C1F26}
    .t{font:500 12.5px 'Noto Sans TC',sans-serif;fill:#1C1F26}
    .ts{font:400 11px 'Noto Sans TC',sans-serif;fill:#5F6673}
    .ln{stroke:#5F6673;stroke-width:1.4;fill:none;marker-end:url(#ar)}
    .lnr{stroke:#C8102E;stroke-width:1.4;fill:none;stroke-dasharray:5 4;marker-end:url(#arr)}
  </style>
  <!-- 泳道背景 -->
  <rect class="lane" x="0" y="0" width="1000" height="110"/>
  <text class="lanel" x="16" y="30">泳道名</text>
  <text class="ts" x="16" y="48">泳道副標</text>
  <!-- 節點：fill 用語意 soft 色、stroke 用語意主色 -->
  <rect x="120" y="35" width="130" height="50" rx="6" fill="#FBF3E4" stroke="#B7791F"/>
  <text class="t" x="185" y="56" text-anchor="middle">主文字</text>
  <text class="ts" x="185" y="73" text-anchor="middle">補充說明</text>
  <!-- 連線：同泳道橫向 H、跨泳道縱向 V -->
  <path class="ln" d="M250 60H300"/>
  <path class="ln" d="M185 85V145"/>
  <!-- 斷點（全圖最多 1~2 條） -->
  <path class="lnr" d="M430 170H820"/>
  <text class="ts" x="625" y="163" text-anchor="middle" fill="#C8102E">斷掉的是什麼資訊，一句話</text>
</svg>
<p class="cap">一句話：這張圖要讀者看見什麼。</p>
</div>
```

節點語意配色：現況系統 `fill="#FBF3E4" stroke="#B7791F"`；目標系統 `fill="#E7EFFB" stroke="#1F5FBF"`；人腦 `fill="#EEEAFD" stroke="#7A5AF5"`；外部或中性 `fill="#EEF0F3" stroke="#8A94A6"`；缺口 `fill="#FBE9EC" stroke="#C8102E"`。

## 4. 鏈狀覆蓋圖（SVG）

什麼時候用：目標系統有一條固定步驟鏈（如八步流程），要標出「對方已有／部分有／完全沒有」的覆蓋狀況。
規則：每步一個框，框的填色直接用語意色標覆蓋度（綠＝已有、琥珀＝部分、紅＝缺），框內第一行步驟名、第二行現況一句話。步驟間用箭頭串起，可折兩行。圖前放 `.legend`，圖後放 `.cap` 總結覆蓋率。

```html
<div class="legend">
  <span><i style="background:var(--ok)"></i>已有、可直接映射</span>
  <span><i style="background:var(--now)"></i>有、但結構不同</span>
  <span><i style="background:var(--gap)"></i>完全沒有</span>
</div>
<div class="flow">
<svg viewBox="0 0 1000 250" …>
  <rect x="20" y="30" width="200" height="64" rx="6" fill="#FBE9EC" stroke="#C8102E"/>
  <text class="st" x="120" y="55" text-anchor="middle">① 步驟名</text>
  <text class="sd" x="120" y="74" text-anchor="middle">現況：一句話</text>
  …
</svg>
<p class="cap">總結：幾步裡有幾步、缺的是哪一段。</p>
</div>
```

## 5. 步驟卡 steps

什麼時候用：行動計畫。每一步必有「完成訊號」，寫不出完成訊號就代表這一步還沒想清楚。
前置步驟（定規則、對齊認知）用 `class="zero"` 顯示為第 0 步。

```html
<ol class="steps">
  <li class="zero">
    <h3>定規則（誰、多久）</h3>
    <p>這一步的目的一句話。</p>
    <dl class="meta">
      <dt>要決定</dt><dd><ul><li>…</li></ul></dd>
      <dt>完成訊號</dt><dd>可驗證的狀態，不是「做完了」</dd>
    </dl>
  </li>
  <li>
    <h3>步驟名</h3>
    <dl class="meta">
      <dt>動作</dt><dd><ul><li>…</li></ul></dd>
      <dt>完成訊號</dt><dd>…</dd>
    </dl>
  </li>
</ol>
```

## 6. 對照表與映射表

- 模組對照（A 系統 vs B 現況）：欄位＝「我們的模組｜對方現況｜落差類型（用 .tag）｜整合動作」。
- 欄位映射：用 `.two` 放兩張並排的 `.db` 卡，欄位＝「來源｜目標｜規則」。
- 訊號表（從資料看出的行為）：欄位＝「訊號｜數據（td.num）｜代表什麼／要決定什麼」。
- 表格外層一律包 `<div class="tblwrap">` 保橫向捲動。

## 7. 重點框 callout

什麼時候用：一段必須被記住的判斷。一個 section 最多一個，超過就代表重點沒排序。
語意：`callout`（藍）＝原理與建議；`.now`＝對現況的判斷；`.gap`＝必須先拍板的難題／風險；`.ok`＝為什麼這樣做值得。
內文用 `<b>開頭短句：</b>` 起頭。

## 8. 可複製區塊 prompt

什麼時候用：交付提示詞、指令、規格書等要整段複製的文字。

```html
<button class="copybtn" onclick="copyPrompt()">複製</button>
<div class="prompt" id="prompt">…內容…</div>
<script>
function copyPrompt(){
  const t=document.getElementById('prompt').innerText;
  navigator.clipboard.writeText(t).then(()=>{
    const b=document.querySelector('.copybtn');b.textContent='已複製';
    setTimeout(()=>b.textContent='複製',1800);
  });
}
</script>
```

## 9. 字體引入

```html
<link href="https://fonts.googleapis.com/css2?family=Noto+Sans+TC:wght@400;500;700;900&display=swap" rel="stylesheet">
```

離線環境拿掉這行也要能讀（font-family 已含系統中文字體備援）。

**深色模式（選用）**：頁面的顏色全部走 token、沒有寫死的淺色時，在 tokens.css 後面接 `assets/tokens-dark.css`，就同時支援系統深色與檢視器的深色切換。表頭、程式碼底色這類 tokens.css 寫死的淺灰，頁面裡改成 token 再覆寫（例如自訂 `--th`、`--codebg` 兩個 token）。

## 10. 作答區（要他拍板時）

什麼時候用：這份文物的目的是讓他（決策人）做決定。規矩見 SKILL.md「要他拍板的文物」一節。樣式在 `tokens.css` 尾段（`.q`、`.opt`、`.tray`）。
題目用資料陣列寫，程式產生畫面——不要手刻每一題的 HTML（同一個結構手刻十次一定會漏）。

```html
<section id="ask"><div class="wrap">
  <h2>請你回答</h2>
  <p>點選項就好；有補充寫在每題下面的格子。答完按最下面的「複製回覆」，貼回對話給我。</p>
  <div id="qs"></div>
  <div class="tray">
    <div class="row">
      <span class="cnt" id="cnt">已回答 0 題</span>
      <button class="btn ghost" id="allrec" type="button">沒答的全部照推薦</button>
      <button class="btn ghost" id="clr" type="button">清空重答</button>
      <button class="btn" id="cp" type="button">複製回覆</button>
    </div>
    <textarea id="out" readonly aria-label="回覆內容，複製後貼回對話"></textarea>
  </div>
</div></section>

<script>
(function(){
var TITLE="＜專案名＞｜第 N 輪拍板回覆", KEY="＜專案代碼＞-r＜N＞";   // 每輪換 KEY
var Q=[
 {g:"分組小標（可省）"},
 {k:"甲", t:"題目，一句問句？", why:"一句話背景。", rec:0,          // rec＝推薦的選項序號；沒有推薦寫 -1
  d:"<p>長的來龍去脈放這裡，會收進「細節」折疊。</p>",               // 可省
  list:["84〈篇名〉","79〈篇名〉"],                                  // 可省；題目或選項提到「N 題／N 則」時必填，逐一列出
  o:["選項一","選項二","其他，寫在下面"], r:"推薦第一個：理由一句話。",
  s:[["我做：…","你做：…","你會看到：…"],["我做：…","你會看到：…"],[]]}   // 每個選項的後果三段；一個獨立問題＝一題，不把幾個問題的選項混在一題
];
var st={}; try{st=JSON.parse(localStorage.getItem(KEY)||"{}")||{}}catch(e){st={}}
function save(){try{localStorage.setItem(KEY,JSON.stringify(st))}catch(e){}}
var box=document.getElementById("qs"), num=["①","②","③","④","⑤","⑥","⑦","⑧","⑨","⑩"];
Q.forEach(function(q,qi){
  if(q.g){var h=document.createElement("p");h.className="grp";h.textContent=q.g;box.appendChild(h);return}
  var d=document.createElement("div");d.className="q";d.id="q-"+qi;
  var html='<h3><span class="k">'+q.k.charAt(0)+'</span><span>'+(q.k.length>1?"（"+q.k+"）":"")+q.t+'</span></h3>';
  if(q.why)html+='<p class="why">'+q.why+'</p>';
  if(q.d)html+='<details><summary>細節（點開看來龍去脈）</summary>'+q.d+'</details>';
  if(q.list)html+='<ul class="qlist">'+q.list.map(function(x){return '<li>'+x+'</li>'}).join('')+'</ul>';
  html+='<p class="note">'+q.r+'</p><div class="opts">';   // 推薦理由放選項正上方
  q.o.forEach(function(o,oi){var sx=(q.s&&q.s[oi]&&q.s[oi].length)?'<small class="steps">'+q.s[oi].map(function(x){return '<span>'+x+'</span>'}).join('')+'</small>':'';
    html+='<label class="opt"><input type="radio" name="r'+qi+'" id="r'+qi+'-'+oi+'" value="'+oi+'"><span class="t">'+num[oi]+' '+o+(oi===q.rec?'<span class="tag sys rec">推薦</span>':'')+sx+'</span></label>'});
  html+='</div><textarea id="n'+qi+'" placeholder="補充（可不填）" aria-label="'+q.k+' 的補充"></textarea>';
  d.innerHTML=html;box.appendChild(d);
  var s=st[qi]||{};
  if(s.o!=null){var el=document.getElementById("r"+qi+"-"+s.o);if(el)el.checked=true}
  if(s.n)document.getElementById("n"+qi).value=s.n;
  d.addEventListener("change",function(e){if(e.target.type==="radio"){st[qi]=st[qi]||{};st[qi].o=+e.target.value;save();render()}});
  d.addEventListener("input",function(e){if(e.target.tagName==="TEXTAREA"){st[qi]=st[qi]||{};st[qi].n=e.target.value;save();render()}});
});
function render(){
  var lines=[TITLE],n=0,total=0;
  Q.forEach(function(q,qi){
    if(q.g)return;total++;
    var s=st[qi]||{},has=s.o!=null||(s.n&&s.n.trim());
    document.getElementById("q-"+qi).classList.toggle("done",!!has);
    if(!has)return;n++;
    var l=q.k+"：";
    if(s.o!=null)l+=num[s.o]+(s.o===q.rec?"（照推薦）":"")+" "+q.o[s.o];   // 選項全文，不截字：截成「…」會讓讀者以為話不見了
    if(s.n&&s.n.trim())l+=(s.o!=null?"｜":"")+"補充："+s.n.trim();
    lines.push(l);
  });
  document.getElementById("cnt").textContent="已回答 "+n+" / "+total+" 題";
  document.getElementById("out").value=n?lines.join("\n"):"（還沒有回答）";
}
document.getElementById("allrec").addEventListener("click",function(){
  Q.forEach(function(q,qi){if(q.g||q.rec<0)return;var s=st[qi]||{};if(s.o==null){s.o=q.rec;st[qi]=s;var el=document.getElementById("r"+qi+"-"+q.rec);if(el)el.checked=true}});
  save();render();
});
document.getElementById("clr").addEventListener("click",function(){
  st={};save();box.querySelectorAll("input[type=radio]").forEach(function(i){i.checked=false});
  box.querySelectorAll("textarea").forEach(function(t){t.value=""});render();
});
document.getElementById("cp").addEventListener("click",function(){
  var o=document.getElementById("out"),b=this;
  function ok(){b.textContent="已複製，貼回對話";setTimeout(function(){b.textContent="複製回覆"},2200)}
  function fb(){o.removeAttribute("readonly");o.focus();o.select();try{document.execCommand("copy");ok()}catch(e){b.textContent="請手動全選複製"}o.setAttribute("readonly","")}
  if(navigator.clipboard&&navigator.clipboard.writeText){navigator.clipboard.writeText(o.value).then(ok,fb)}else fb();
});
render();
})();
</script>
```

注意：
- **每個選項要寫「選了會發生什麼」，固定三段「我做／你做／你會看到」**：題目物件加 `s:[["我做：…","你做：…","你會看到：…"], …]` 與 `o` 一一對應，畫面上放在選項字下方（`.opt .steps`）。推薦理由 `r` 放在選項正上方。一格裡有幾個獨立問題就拆幾個子題（各自單選）；選項或建議提到「N 題／N 則」時同一格要把那 N 個列出來。
- 「沒答的全部照推薦」會跳過 `rec:-1` 的題（只有他知道答案的那種）。
- 剪貼簿在某些環境被擋，所以一定要留「全選讓他手動複製」的退路。
- localStorage 在某些環境不可用，所有存取都包 try/catch；頁面沒有它也要能用。
- 多輪時頁首放「前幾輪你定了什麼」結果表（題｜結果｜因此確定的事），已定的題從 Q 陣列移除。
- `.qlist`（清單）與 `.steps`（三段後果，每段一行、灰字小號）的樣式在 `tokens.css` 尾段；沒有就補這兩條：`.qlist{margin:6px 0 0;padding-left:1.2em;font-size:.9rem;columns:2}` `.opt .steps{display:grid;gap:2px;margin-top:4px;font-size:.82rem;color:var(--muted)}`。
