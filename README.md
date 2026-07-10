# untetheredsky.github.io
bread formula calculator and levain builder
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1, viewport-fit=cover">
<meta name="theme-color" content="#221E19">
<meta name="apple-mobile-web-app-capable" content="yes">
<meta name="apple-mobile-web-app-status-bar-style" content="black-translucent">
<title>Formula Book</title>
<style>
:root{
  --ink:#221E19;
  --ink2:#3A352D;
  --paper:#F5F4F1;
  --card:#FFFFFF;
  --line:#DCD9D2;
  --dim:#6E685E;
  --sack:#2F4E8C;        /* flour-sack blue: water & primary actions */
  --sack-soft:#E4EAF5;
  --rye:#8C5A19;         /* pre-fermented flour bronze */
  --rye-soft:#F1E7D6;
  --danger:#9C3325;
  --radius:8px;
  --mono:ui-monospace,"SF Mono",Menlo,Consolas,"Liberation Mono",monospace;
  --disp:"Futura","Futura PT","Century Gothic","Avenir Next","Trebuchet MS",sans-serif;
  --body:"Futura","Futura PT","Century Gothic","Avenir Next",-apple-system,"Segoe UI",Roboto,Helvetica,Arial,sans-serif;
}
*{box-sizing:border-box;margin:0;padding:0}
html{-webkit-text-size-adjust:100%}
body{background:var(--paper);color:var(--ink);font-family:var(--body);font-size:16px;line-height:1.45}
#app{max-width:780px;margin:0 auto;padding:0 14px 90px}
button{font:inherit;cursor:pointer;border:none;background:none;color:inherit;-webkit-tap-highlight-color:transparent}
input,select,textarea{font:inherit;color:var(--ink);background:var(--card);border:1px solid var(--line);border-radius:6px;padding:9px 10px;width:100%}
input:focus,select:focus,textarea:focus,button:focus-visible{outline:2px solid var(--sack);outline-offset:1px}
input[type=number]{-moz-appearance:textfield}
input::-webkit-outer-spin-button,input::-webkit-inner-spin-button{-webkit-appearance:none;margin:0}

/* ---------- type ---------- */
.disp{font-family:var(--disp);text-transform:uppercase;letter-spacing:.05em;font-weight:700}
.eyebrow{font-family:var(--disp);text-transform:uppercase;letter-spacing:.14em;font-size:11px;color:var(--dim);font-weight:700}
.num{font-family:var(--mono);font-variant-numeric:tabular-nums}

/* ---------- header ---------- */
header.top{display:flex;align-items:center;justify-content:space-between;gap:10px;padding:18px 2px 14px}
header.top h1{font-family:var(--disp);text-transform:uppercase;letter-spacing:.06em;font-size:22px;line-height:1.1}
header.top .sub{font-size:12px;color:var(--dim);margin-top:2px}
.backlink{font-family:var(--disp);text-transform:uppercase;letter-spacing:.1em;font-size:12px;font-weight:700;color:var(--sack);padding:8px 0;display:inline-block}

/* ---------- buttons ---------- */
.btn{display:inline-flex;align-items:center;justify-content:center;gap:6px;min-height:42px;padding:8px 16px;border-radius:var(--radius);font-family:var(--disp);text-transform:uppercase;letter-spacing:.05em;font-size:13px;font-weight:700;background:var(--sack);color:#fff}
.btn.ghost{background:transparent;color:var(--sack);border:1.5px solid var(--sack)}
.btn.quiet{background:transparent;color:var(--dim);border:1.5px solid var(--line)}
.btn.danger{background:transparent;color:var(--danger);border:1.5px solid var(--danger)}
.btn.small{min-height:34px;padding:4px 12px;font-size:12px}
.btnrow{display:flex;flex-wrap:wrap;gap:8px}

/* ---------- library ---------- */
.libgrid{display:flex;flex-direction:column;gap:10px;margin-top:6px}
.reccard{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);padding:14px;display:block;width:100%;text-align:left}
.reccard h3{font-family:var(--disp);text-transform:uppercase;letter-spacing:.04em;font-size:17px}
.reccard .cat{font-size:12px;color:var(--dim);margin-top:1px}
.reccard .chips{display:flex;flex-wrap:wrap;gap:6px;margin-top:9px}
.chip{font-family:var(--mono);font-size:12px;padding:3px 8px;border-radius:99px;background:var(--paper);border:1px solid var(--line)}
.chip.hyd{background:var(--sack-soft);border-color:var(--sack);color:var(--sack);font-weight:600}
.chip.pff{background:var(--rye-soft);border-color:var(--rye);color:var(--rye);font-weight:600}
.empty{padding:36px 16px;text-align:center;color:var(--dim);border:1.5px dashed var(--line);border-radius:var(--radius)}

/* ---------- tag strip (signature) ---------- */
.tagstrip{background:var(--ink);color:#F2EFE9;border-radius:var(--radius);padding:14px 14px 12px;margin:12px 0;display:grid;grid-template-columns:repeat(4,1fr);gap:8px;position:relative;overflow:hidden}
.tagstrip::after{content:"";position:absolute;left:0;right:0;top:0;height:3px;background:repeating-linear-gradient(90deg,var(--sack) 0 14px,transparent 14px 22px)}
.tag .v{font-family:var(--mono);font-size:clamp(17px,4.6vw,26px);font-weight:600;line-height:1.1}
.tag .v.blue{color:#9BB9EA}
.tag .v.bronze{color:#D8A45B}
.tag .l{font-family:var(--disp);text-transform:uppercase;letter-spacing:.12em;font-size:9.5px;color:#A39C90;margin-top:3px;font-weight:700}
.hydbar{grid-column:1/-1;height:5px;background:#3A352D;border-radius:3px;overflow:hidden;margin-top:2px}
.hydbar i{display:block;height:100%;background:var(--sack)}
.scalednote{grid-column:1/-1;font-size:11px;color:#D8A45B;font-family:var(--mono)}

/* ---------- sections & cards ---------- */
section.card{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);padding:14px;margin:12px 0}
section.card>h2{font-family:var(--disp);text-transform:uppercase;letter-spacing:.1em;font-size:13px;font-weight:700;color:var(--ink2);padding-bottom:9px;border-bottom:1px solid var(--line);margin-bottom:11px;display:flex;justify-content:space-between;align-items:center;gap:8px}
section.card>h2 .hint{font-family:var(--body);text-transform:none;letter-spacing:0;font-weight:400;font-size:12px;color:var(--dim)}
.fieldgrid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.fieldgrid .full{grid-column:1/-1}
label.f{display:block;font-size:12px;color:var(--dim);margin-bottom:4px}

/* ---------- ingredient rows ---------- */
.ingrow{display:grid;grid-template-columns:minmax(0,1fr) 84px 96px 34px;gap:6px;margin-bottom:7px;align-items:center}
.ingrow input.g{text-align:right;font-family:var(--mono)}
.ingrow select{padding:9px 4px;font-size:14px}
.xbtn{width:34px;height:38px;border-radius:6px;color:var(--dim);border:1px solid var(--line);font-size:16px;line-height:1}
.addrow{margin-top:4px}
.subtot{font-family:var(--mono);font-size:13px;color:var(--dim);text-align:right;padding:4px 2px 0}

/* ---------- tables ---------- */
table.formula{width:100%;border-collapse:collapse;font-size:14.5px}
table.formula th{font-family:var(--disp);text-transform:uppercase;letter-spacing:.1em;font-size:10.5px;color:var(--dim);text-align:left;padding:6px 6px;border-bottom:1.5px solid var(--ink)}
table.formula th.r,table.formula td.r{text-align:right}
table.formula td{padding:7px 6px;border-bottom:1px solid var(--line)}
table.formula td.r{font-family:var(--mono)}
table.formula tr.totalrow td{border-top:2px solid var(--ink);border-bottom:none;font-weight:700}
table.formula tr.hydrow td{border-bottom:none;color:var(--sack);font-weight:700}
table.formula tr.sub td{color:var(--dim);font-size:13px}
.tagline{font-size:12px;color:var(--dim);margin-top:8px}

/* ---------- scale panel ---------- */
.scalegrid{display:grid;grid-template-columns:1fr 1fr auto;gap:8px;align-items:end}
.scalegrid .or{grid-column:1/-1;text-align:center;font-family:var(--disp);text-transform:uppercase;letter-spacing:.14em;font-size:11px;color:var(--dim);padding:2px 0}
.factornote{margin-top:10px;font-family:var(--mono);font-size:13px;color:var(--rye)}

/* ---------- process ---------- */
.procgrid{display:grid;grid-template-columns:1fr 1fr;gap:10px}
.procgrid .full{grid-column:1/-1}
textarea{min-height:70px;resize:vertical}

/* ---------- sheet (print view) ---------- */
.sheet{background:var(--card);border:1px solid var(--line);border-radius:var(--radius);padding:20px 18px;margin-top:12px}
.sheet h1{font-family:var(--disp);text-transform:uppercase;letter-spacing:.04em;font-size:24px}
.sheet .meta{font-family:var(--mono);font-size:12.5px;color:var(--dim);margin-top:3px}
.sheet h2{font-family:var(--disp);text-transform:uppercase;letter-spacing:.12em;font-size:12.5px;margin:18px 0 7px;border-bottom:1.5px solid var(--ink);padding-bottom:4px}
.sheet .procline{font-size:13.5px;padding:3px 0;display:flex;gap:8px}
.sheet .procline b{font-family:var(--disp);text-transform:uppercase;letter-spacing:.08em;font-size:11px;min-width:118px;color:var(--ink2);padding-top:2px}
.sheetstats{display:flex;gap:16px;flex-wrap:wrap;margin-top:10px;padding:10px 12px;background:var(--paper);border-radius:6px}
.sheetstats div .v{font-family:var(--mono);font-weight:700;font-size:17px}
.sheetstats div .v.blue{color:var(--sack)}
.sheetstats div .v.bronze{color:var(--rye)}
.sheetstats div .l{font-family:var(--disp);text-transform:uppercase;letter-spacing:.1em;font-size:9.5px;color:var(--dim)}

/* ---------- levain builder blocks ---------- */
.buildblock{margin-bottom:14px;padding:12px 12px 8px;border-radius:6px;border-left:4px solid}
.buildblock table.formula td{border-bottom-color:rgba(140,105,30,.28)}
.buildblock .eyebrow{color:#7A5A14}

/* ---------- gold-tinted formula cards ---------- */
section.card.gold1{background:rgba(214,150,30,.07);border-left:4px solid rgba(163,108,15,.35)}
section.card.gold2{background:rgba(214,150,30,.22);border-left:4px solid rgba(163,108,15,.85)}
.gold1 table.formula td,.gold2 table.formula td{border-bottom-color:rgba(140,105,30,.28)}
.gold1>h2,.gold2>h2{border-bottom-color:rgba(140,105,30,.35)}

/* ---------- misc ---------- */
.banner{background:var(--rye-soft);border:1px solid var(--rye);color:var(--rye);border-radius:var(--radius);padding:10px 12px;font-size:13.5px;margin:10px 0}
.footerbar{position:fixed;bottom:0;left:0;right:0;background:linear-gradient(transparent,var(--paper) 30%);padding:18px 14px 16px;display:flex;justify-content:center;gap:8px;pointer-events:none}
.footerbar .btn{pointer-events:auto;box-shadow:0 2px 10px rgba(34,30,25,.18)}
.hiddenfile{display:none}

@media (max-width:560px){
  .ingrow{grid-template-columns:minmax(0,1fr) 74px 88px 32px}
  .tagstrip{grid-template-columns:repeat(2,1fr)}
}
@media (prefers-reduced-motion:no-preference){
  .reccard{transition:border-color .15s}
  .reccard:active{border-color:var(--sack)}
}
@media print{
  body{background:#fff}
  #app{max-width:none;padding:0}
  .no-print,.footerbar,header.top{display:none!important}
  .sheet{border:none;padding:0;margin:0}
  .sheetstats{border:1px solid #999}
}
</style>
</head>
<body>
<div id="app"></div>
<input type="file" id="importFile" class="hiddenfile" accept="application/json">
<script>
"use strict";
/* =============== storage =============== */
const LS_KEY = "formulaBook.v1";
let storageOk = true;
try {
  localStorage.setItem("__fb_probe__", "1");
  localStorage.removeItem("__fb_probe__");
} catch (e) { storageOk = false; }

function uid(){ return Date.now().toString(36) + Math.random().toString(36).slice(2,7); }

function seedRecipe(){
  return {
    id: uid(),
    name: "Open-Crumb Table Loaf",
    category: "Sourdough",
    yieldLoafG: 850,
    yieldCount: 20,
    ingredients: [
      { id: uid(), name: "Bread flour", grams: 8000, type: "flour" },
      { id: uid(), name: "Water", grams: 5600, type: "liquid" },
      { id: uid(), name: "Salt", grams: 190, type: "salt" }
    ],
    levain: {
      enabled: true,
      rows: [
        { id: uid(), name: "Bread flour", grams: 1600, type: "flour" },
        { id: uid(), name: "Water", grams: 1600, type: "liquid" }
      ],
      starterGrams: 320,
      starterHydration: 100
    },
    soakers: [],
    process: {
      mix: "4 min low / 3 min medium (spiral)",
      doughTemp: "78°F target",
      bulk: "4.5 hr @ 76–78°F",
      folds: "3 coil folds — 30 / 60 / 90 min",
      divide: "Divide 850g, light preshape, 20 min rest",
      shape: "Batard, seam-side up in banneton",
      proof: "Retard 12–14 hr @ 38°F",
      bake: "Deck 480°F — 20 min steam, 20–24 min dry",
      steam: "Full steam at load, vent at 20 min"
    },
    notes: "Example formula — edit or delete. Starter flour/water are counted in true totals."
  };
}

function blankRecipe(){
  return {
    id: uid(), name: "", category: "",
    yieldLoafG: null, yieldCount: null,
    ingredients: [
      { id: uid(), name: "Bread flour", grams: null, type: "flour" },
      { id: uid(), name: "Water", grams: null, type: "liquid" },
      { id: uid(), name: "Salt", grams: null, type: "salt" }
    ],
    levain: { enabled: false, rows: [], starterGrams: null, starterHydration: 100 },
    soakers: [],
    process: { mix:"", doughTemp:"", bulk:"", folds:"", divide:"", shape:"", proof:"", bake:"", steam:"" },
    notes: ""
  };
}

function loadDB(){
  if (storageOk) {
    try {
      const raw = localStorage.getItem(LS_KEY);
      if (raw) return JSON.parse(raw);
    } catch(e) {}
  }
  return { recipes: [seedRecipe()] };
}
let db = loadDB();

function defaultLevain(){
  return { id: uid(), name: "", target: 3520, surplus: 100, hydration: 100,
    starterGrams: 50, starterHydration: 100, builds: 2, inoculation: null,
    flours: [{ id: uid(), name: "Bread flour", pct: 100 }] };
}
if (!db.levains){
  db.levains = [];
  if (db.lb){
    const lv = Object.assign(defaultLevain(), db.lb);
    lv.name = lv.name || "Levain";
    db.levains.push(lv);
    delete db.lb;
  }
}
if (!db.levains.length){
  const lv = defaultLevain();
  lv.name = "Table loaf levain";
  db.levains.push(lv);
}

let saveTimer = null;
function save(){
  if (!storageOk) return;
  clearTimeout(saveTimer);
  saveTimer = setTimeout(() => {
    try { localStorage.setItem(LS_KEY, JSON.stringify(db)); } catch(e) {}
  }, 250);
}

/* =============== state =============== */
const ui = { view: "library", recipeId: null, factor: 1 };

function currentRecipe(){ return db.recipes.find(r => r.id === ui.recipeId) || null; }

/* =============== math =============== */
const TYPES = ["flour","liquid","salt","inclusion","other"];
const TYPE_LABEL = { flour:"Flour", liquid:"Liquid", salt:"Salt", inclusion:"Inclusion", other:"Other" };

function n(v){ const x = parseFloat(v); return isFinite(x) && x > 0 ? x : 0; }

function starterSplit(grams, hyd){
  const g = n(grams), h = n(hyd);
  if (!g) return { flour: 0, water: 0 };
  const flour = g / (1 + h/100);
  return { flour, water: g - flour };
}

function compute(r){
  let flour = 0, water = 0, preFlour = 0, dough = 0;
  const agg = new Map();
  function addAgg(name, grams, type, order){
    const key = (name || "").trim().toLowerCase() || "(unnamed)";
    const cur = agg.get(key);
    if (cur) { cur.grams += grams; }
    else agg.set(key, { name: (name||"").trim() || "(unnamed)", grams, type, order });
  }
  function absorb(rows, isLevain){
    (rows||[]).forEach(row => {
      const g = n(row.grams);
      if (!g) { if((row.name||"").trim()) addAgg(row.name, 0, row.type, typeOrder(row.type)); return; }
      dough += g;
      if (row.type === "flour"){ flour += g; if (isLevain) preFlour += g; }
      else if (row.type === "liquid"){ water += g; }
      addAgg(row.name, g, row.type, typeOrder(row.type));
    });
  }
  function typeOrder(t){ return { flour:0, liquid:1, salt:2, inclusion:4, other:5 }[t] ?? 5; }

  absorb(r.ingredients, false);

  let levainTotal = 0, starterF = 0, starterW = 0;
  if (r.levain && r.levain.enabled){
    absorb(r.levain.rows, true);
    levainTotal = (r.levain.rows||[]).reduce((s,x)=>s+n(x.grams),0);
    const sp = starterSplit(r.levain.starterGrams, r.levain.starterHydration);
    starterF = sp.flour; starterW = sp.water;
    const sg = n(r.levain.starterGrams);
    if (sg){
      flour += sp.flour; water += sp.water; preFlour += sp.flour;
      dough += sg; levainTotal += sg;
      // fold the starter's flour & water into the matching aggregated rows
      const levFlourRow = (r.levain.rows||[]).filter(x => x.type === "flour" && (x.name||"").trim())
        .sort((a,b) => n(b.grams) - n(a.grams))[0];
      const levLiqRow = (r.levain.rows||[]).filter(x => x.type === "liquid" && (x.name||"").trim())
        .sort((a,b) => n(b.grams) - n(a.grams))[0];
      if (sp.flour) addAgg(levFlourRow ? levFlourRow.name : "Flour", sp.flour, "flour", 0);
      if (sp.water) addAgg(levLiqRow ? levLiqRow.name : "Water", sp.water, "liquid", 1);
    }
  }

  const soakerTotals = [];
  (r.soakers||[]).forEach(s => {
    absorb(s.rows, false);
    soakerTotals.push({ id: s.id, name: s.name, total: (s.rows||[]).reduce((t,x)=>t+n(x.grams),0) });
  });

  const hyd = flour ? (water/flour)*100 : 0;
  const pff = flour ? (preFlour/flour)*100 : 0;

  const rows = Array.from(agg.values()).sort((a,b)=> a.order - b.order || b.grams - a.grams);

  return { flour, water, hyd, pff, dough, levainTotal, starterF, starterW, soakerTotals, rows };
}

function fg(g, factor){ return Math.round(g * factor).toLocaleString(); }
function fp(p){ return (Math.round(p*10)/10).toFixed(1); }

/* =============== html helpers =============== */
function esc(s){ return String(s ?? "").replace(/[&<>"']/g, c => ({"&":"&amp;","<":"&lt;",">":"&gt;",'"':"&quot;","'":"&#39;"}[c])); }
function attr(s){ return esc(s); }

/* =============== renderers =============== */
const app = document.getElementById("app");

function render(scrollTop = true){
  if (ui.view === "library") renderLibrary();
  else if (ui.view === "recipe") renderRecipe();
  else if (ui.view === "sheet") renderSheet();
  else if (ui.view === "lblib") renderLBLib();
  else if (ui.view === "lb") renderLB();
  else if (ui.view === "lbsheet") renderLBSheet();
  if (scrollTop) window.scrollTo(0, 0);
}

function rerenderInPlace(){
  const y = window.scrollY;
  render(false);
  window.scrollTo(0, y);
}

function storageBanner(){
  return storageOk ? "" :
    `<div class="banner no-print">Saving is unavailable in this preview. Download this file and open it in your phone or computer's browser — recipes will then save automatically.</div>`;
}

function renderLibrary(){
  const cards = db.recipes.map(r => {
    const c = compute(r);
    return `<button class="reccard" data-action="open" data-id="${attr(r.id)}">
      <h3>${esc(r.name) || "Untitled formula"}</h3>
      ${r.category ? `<div class="cat">${esc(r.category)}</div>` : ""}
      <div class="chips">
        <span class="chip hyd num">${fp(c.hyd)}% hyd</span>
        ${c.pff > 0 ? `<span class="chip pff num">${fp(c.pff)}% PFF</span>` : ""}
        <span class="chip num">${fg(c.dough,1)} g dough</span>
      </div>
    </button>`;
  }).join("");

  app.innerHTML = `
    <header class="top">
      <div>
        <h1>Formula Book</h1>
        <div class="sub">Baker's percentages, true hydration, batch scaling</div>
      </div>
    </header>
    ${storageBanner()}
    <div class="libgrid">
      ${cards || `<div class="empty">No formulas yet. Start your first one below.</div>`}
    </div>
    <section class="card no-print">
      <h2>Library backup</h2>
      <div class="btnrow">
        <button class="btn quiet small" data-action="export">Export JSON</button>
        <button class="btn quiet small" data-action="import">Import JSON</button>
      </div>
      <div class="tagline">Export regularly — your library lives in this browser only.</div>
    </section>
    <div class="footerbar no-print">
      <button class="btn ghost" style="background:var(--paper)" data-action="openlb">Levain builder</button>
      <button class="btn" data-action="new">+ New formula</button>
    </div>`;
}

function ingRowHTML(row, section, soakerId){
  const opts = TYPES.map(t => `<option value="${t}" ${row.type===t?"selected":""}>${TYPE_LABEL[t]}</option>`).join("");
  return `<div class="ingrow">
    <input type="text" placeholder="Ingredient" value="${attr(row.name)}"
      data-sec="${section}" ${soakerId?`data-soaker="${attr(soakerId)}"`:""} data-row="${attr(row.id)}" data-field="name">
    <input type="text" class="g num" inputmode="decimal" placeholder="g" value="${row.grams ?? ""}"
      data-sec="${section}" ${soakerId?`data-soaker="${attr(soakerId)}"`:""} data-row="${attr(row.id)}" data-field="grams" aria-label="grams">
    <select data-sec="${section}" ${soakerId?`data-soaker="${attr(soakerId)}"`:""} data-row="${attr(row.id)}" data-field="type">${opts}</select>
    <button class="xbtn" data-action="delrow" data-sec="${section}" ${soakerId?`data-soaker="${attr(soakerId)}"`:""} data-row="${attr(row.id)}" aria-label="Remove row">✕</button>
  </div>`;
}

function tagStripHTML(r, c){
  const hydW = Math.max(0, Math.min(100, c.hyd));
  return `
  <div class="tagstrip">
    <div class="tag"><div class="v blue num">${fp(c.hyd)}%</div><div class="l">True hydration</div></div>
    <div class="tag"><div class="v bronze num">${fp(c.pff)}%</div><div class="l">Pre-fermented flour</div></div>
    <div class="tag"><div class="v num">${fg(c.flour, ui.factor)} g</div><div class="l">Total flour</div></div>
    <div class="tag"><div class="v num">${fg(c.dough, ui.factor)} g</div><div class="l">Total dough</div></div>
    <div class="hydbar"><i style="width:${hydW}%"></i></div>
    ${ui.factor !== 1 ? `<div class="scalednote">Scaled ×${(Math.round(ui.factor*1000)/1000)} — entered weights unchanged</div>` : ""}
  </div>`;
}

function overallTableHTML(c){
  const body = c.rows.map(row => `
    <tr>
      <td>${esc(row.name)}</td>
      <td class="r num">${fg(row.grams, ui.factor)}</td>
      <td class="r num">${c.flour ? fp(row.grams / c.flour * 100) : "—"}%</td>
    </tr>`).join("");
  return `<table class="formula">
    <thead><tr><th>Ingredient</th><th class="r">Grams</th><th class="r">Baker's %</th></tr></thead>
    <tbody>
      ${body || `<tr><td colspan="3" style="color:var(--dim)">Add ingredients to see the formula.</td></tr>`}
      <tr class="totalrow"><td>Total flour</td><td class="r num">${fg(c.flour, ui.factor)}</td><td class="r num">100.0%</td></tr>
      <tr class="hydrow"><td>True hydration</td><td class="r num">${fg(c.water, ui.factor)}</td><td class="r num">${fp(c.hyd)}%</td></tr>
    </tbody>
  </table>
  <div class="tagline">All flour and water from levain, starter, and soakers is rolled into these totals.</div>`;
}

function finalMixTableHTML(r, c){
  let body = (r.ingredients||[]).filter(x => n(x.grams) || (x.name||"").trim()).map(x => `
    <tr>
      <td>${esc(x.name) || "(unnamed)"}</td>
      <td class="r num">${fg(n(x.grams), ui.factor)}</td>
      <td class="r num">${c.flour ? fp(n(x.grams)/c.flour*100) : "—"}%</td>
    </tr>`).join("");
  if (r.levain && r.levain.enabled && c.levainTotal){
    body += `<tr>
      <td><b>Levain</b> <span style="color:var(--dim);font-size:12.5px">(entire build)</span></td>
      <td class="r num">${fg(c.levainTotal, ui.factor)}</td>
      <td class="r num">${c.flour ? fp(c.levainTotal/c.flour*100) : "—"}%</td>
    </tr>`;
  }
  c.soakerTotals.forEach(s => {
    if (!s.total) return;
    body += `<tr>
      <td><b>${esc(s.name) || "Soaker"}</b> <span style="color:var(--dim);font-size:12.5px">(entire soak)</span></td>
      <td class="r num">${fg(s.total, ui.factor)}</td>
      <td class="r num">${c.flour ? fp(s.total/c.flour*100) : "—"}%</td>
    </tr>`;
  });
  return `<table class="formula">
    <thead><tr><th>Into the mixer</th><th class="r">Grams</th><th class="r">% of flour</th></tr></thead>
    <tbody>
      ${body || `<tr><td colspan="3" style="color:var(--dim)">Nothing to mix yet.</td></tr>`}
      <tr class="totalrow"><td>Total dough</td><td class="r num">${fg(c.dough, ui.factor)}</td><td class="r num"></td></tr>
    </tbody>
  </table>
  <div class="tagline">Levain and soaker flour/water are already subtracted from the mixer amounts above them.</div>`;
}

function yieldReadoutHTML(r){
  const c = compute(r);
  const dough = c.dough * ui.factor;
  if (!dough) return "Add ingredients to see yield.";
  const lg = n(r.yieldLoafG), ct = n(r.yieldCount);
  const parts = [];
  if (lg > 0) parts.push(`At <b>${Math.round(lg).toLocaleString()} g</b> per loaf, current dough (${fg(c.dough, ui.factor)} g) yields <b>${(Math.round(dough/lg*10)/10).toLocaleString()}</b> loaves`);
  if (ct > 0) parts.push(`Split into <b>${Math.round(ct).toLocaleString()}</b> loaves → <b>${Math.round(dough/ct).toLocaleString()} g</b> each`);
  if (!parts.length) return "Enter a loaf weight or count to see the yield of the current dough.";
  return parts.join("<br>");
}

function refreshYieldReadout(){
  const z = document.getElementById("yieldReadout");
  const r = currentRecipe();
  if (z && r) z.innerHTML = yieldReadoutHTML(r);
}

function computedZoneHTML(r){
  const c = compute(r);
  return tagStripHTML(r, c)
    + `<section class="card gold1"><h2>Overall formula <span class="hint">true percentages</span></h2>${overallTableHTML(c)}</section>`
    + `<section class="card gold2"><h2>Final mix <span class="hint">what goes in the spiral</span></h2>${finalMixTableHTML(r, c)}</section>`;
}

function renderRecipe(){
  const r = currentRecipe();
  if (!r){ ui.view = "library"; return renderLibrary(); }
  const lev = r.levain || (r.levain = { enabled:false, rows:[], starterGrams:null, starterHydration:100 });

  const soakersHTML = (r.soakers||[]).map(s => `
    <section class="card">
      <h2>
        <input type="text" style="max-width:60%;font-family:var(--disp);text-transform:uppercase;letter-spacing:.06em;font-weight:700;border:none;background:transparent;padding:0"
          value="${attr(s.name)}" placeholder="SOAKER NAME" data-sec="soakername" data-soaker="${attr(s.id)}">
        <button class="btn danger small" data-action="delsoaker" data-soaker="${attr(s.id)}">Remove</button>
      </h2>
      ${(s.rows||[]).map(row => ingRowHTML(row, "soaker", s.id)).join("")}
      <button class="btn ghost small addrow" data-action="addrow" data-sec="soaker" data-soaker="${attr(s.id)}">+ Ingredient</button>
      <div class="subtot">Soak total: ${fg((s.rows||[]).reduce((t,x)=>t+n(x.grams),0), 1)} g entered</div>
    </section>`).join("");

  app.innerHTML = `
    <header class="top no-print">
      <div>
        <button class="backlink" data-action="back">← Library</button>
        <h1>${esc(r.name) || "Untitled formula"}</h1>
      </div>
      <button class="btn ghost small" data-action="sheet">Formula sheet</button>
    </header>
    ${storageBanner()}

    <div id="computedZone">${computedZoneHTML(r)}</div>

    <section class="card no-print">
      <h2>Formula details</h2>
      <div class="fieldgrid">
        <div class="full"><label class="f">Name</label><input type="text" value="${attr(r.name)}" data-sec="meta" data-field="name" placeholder="e.g. Seeded Country Loaf"></div>
        <div><label class="f">Category</label><input type="text" value="${attr(r.category)}" data-sec="meta" data-field="category" placeholder="Sourdough, Enriched…"></div>
        <div><label class="f">Yield (loaf g × count)</label>
          <div style="display:flex;gap:6px">
            <input type="text" inputmode="decimal" class="num" value="${r.yieldLoafG ?? ""}" data-sec="meta" data-field="yieldLoafG" placeholder="850" aria-label="loaf grams">
            <input type="text" inputmode="decimal" class="num" value="${r.yieldCount ?? ""}" data-sec="meta" data-field="yieldCount" placeholder="20" aria-label="loaf count">
          </div>
        </div>
      </div>
    </section>

    <section class="card no-print">
      <h2>Final dough <span class="hint">mixer additions only</span></h2>
      ${(r.ingredients||[]).map(row => ingRowHTML(row, "dough")).join("")}
      <button class="btn ghost small addrow" data-action="addrow" data-sec="dough">+ Ingredient</button>
    </section>

    <section class="card no-print">
      <h2>Levain build
        <button class="btn ${lev.enabled ? "quiet" : "ghost"} small" data-action="togglelevain">${lev.enabled ? "Remove levain" : "+ Add levain"}</button>
      </h2>
      ${lev.enabled ? `
        ${(lev.rows||[]).map(row => ingRowHTML(row, "levain")).join("")}
        <button class="btn ghost small addrow" data-action="addrow" data-sec="levain">+ Ingredient</button>
        <div class="fieldgrid" style="margin-top:12px">
          <div><label class="f">Mature starter (g)</label><input type="text" inputmode="decimal" class="num" value="${lev.starterGrams ?? ""}" data-sec="levmeta" data-field="starterGrams" placeholder="320"></div>
          <div><label class="f">Starter hydration (%)</label><input type="text" inputmode="decimal" class="num" value="${lev.starterHydration ?? ""}" data-sec="levmeta" data-field="starterHydration" placeholder="100"></div>
        </div>
        <div class="tagline">The starter's own flour and water are counted in total flour and true hydration.</div>
      ` : `<div class="tagline">No levain — straight dough or yeasted formula.</div>`}
    </section>

    ${soakersHTML}
    <div class="no-print" style="margin:12px 0">
      <button class="btn ghost small" data-action="addsoaker">+ Add soaker / porridge</button>
    </div>

    <section class="card no-print">
      <h2>Scale batch</h2>
      <div class="scalegrid">
        <div><label class="f">Loaf weight (g)</label><input type="text" inputmode="decimal" class="num" id="scLoaf" data-sec="scalecalc" value="${r.yieldLoafG ?? ""}" placeholder="850"></div>
        <div><label class="f">Loaf count</label><input type="text" inputmode="decimal" class="num" id="scCount" data-sec="scalecalc" value="${r.yieldCount ?? ""}" placeholder="20"></div>
        <button class="btn small" data-action="scaleyield">Scale</button>
        <div class="or">— or —</div>
        <div style="grid-column:1/3"><label class="f">Target total flour (g)</label><input type="text" inputmode="decimal" class="num" id="scFlour" placeholder="22680 = one 50 lb bag"></div>
        <button class="btn small" data-action="scaleflour">Scale</button>
      </div>
      <div class="tagline" id="yieldReadout" style="margin-top:10px">${yieldReadoutHTML(r)}</div>
      ${ui.factor !== 1 ? (() => {
        const csc = compute(r);
        return `
        <div class="banner" style="margin-top:12px">Scaled ×${Math.round(ui.factor*1000)/1000} — every table on this page now shows <b>${fg(csc.dough, ui.factor)} g</b> total dough (<b>${fg(csc.flour, ui.factor)} g</b> flour). Your entered weights are unchanged.</div>
        <div class="btnrow" style="margin-top:8px">
          <button class="btn ghost small" data-action="bakein">Save scaled weights as the recipe</button>
          <button class="btn quiet small" data-action="resetscale">Reset view</button>
        </div>`;
      })() : ""}
    </section>

    <section class="card no-print">
      <h2>Process</h2>
      <div class="procgrid">
        <div><label class="f">Mix (time / speed)</label><input type="text" value="${attr(r.process.mix)}" data-sec="proc" data-field="mix"></div>
        <div><label class="f">Target dough temp</label><input type="text" value="${attr(r.process.doughTemp)}" data-sec="proc" data-field="doughTemp"></div>
        <div><label class="f">Bulk (time & temp)</label><input type="text" value="${attr(r.process.bulk)}" data-sec="proc" data-field="bulk"></div>
        <div><label class="f">Fold schedule</label><input type="text" value="${attr(r.process.folds)}" data-sec="proc" data-field="folds"></div>
        <div><label class="f">Divide & preshape</label><input type="text" value="${attr(r.process.divide)}" data-sec="proc" data-field="divide"></div>
        <div><label class="f">Final shape</label><input type="text" value="${attr(r.process.shape)}" data-sec="proc" data-field="shape"></div>
        <div><label class="f">Proof</label><input type="text" value="${attr(r.process.proof)}" data-sec="proc" data-field="proof"></div>
        <div><label class="f">Bake (temp / time)</label><input type="text" value="${attr(r.process.bake)}" data-sec="proc" data-field="bake"></div>
        <div class="full"><label class="f">Steam</label><input type="text" value="${attr(r.process.steam)}" data-sec="proc" data-field="steam"></div>
        <div class="full"><label class="f">Notes</label><textarea data-sec="proc" data-field="notes_free">${esc(r.notes)}</textarea></div>
      </div>
    </section>

    <section class="card no-print">
      <h2>Manage</h2>
      <div class="btnrow">
        <button class="btn quiet small" data-action="duplicate">Duplicate</button>
        <button class="btn danger small" data-action="delete">Delete formula</button>
      </div>
    </section>`;
}

function renderSheet(){
  const r = currentRecipe();
  if (!r){ ui.view = "library"; return renderLibrary(); }
  const c = compute(r);
  const f = ui.factor;
  const today = new Date().toLocaleDateString();

  const procRows = [
    ["Mix", r.process.mix], ["Dough temp", r.process.doughTemp], ["Bulk", r.process.bulk],
    ["Folds", r.process.folds], ["Divide", r.process.divide], ["Shape", r.process.shape],
    ["Proof", r.process.proof], ["Bake", r.process.bake], ["Steam", r.process.steam]
  ].filter(x => (x[1]||"").trim())
   .map(x => `<div class="procline"><b>${x[0]}</b><span>${esc(x[1])}</span></div>`).join("");

  const levDetail = (r.levain && r.levain.enabled) ? `
    <h2>Levain build</h2>
    <table class="formula"><tbody>
      ${(r.levain.rows||[]).filter(x=>n(x.grams)).map(x=>`<tr><td>${esc(x.name)}</td><td class="r num">${fg(n(x.grams),f)} g</td></tr>`).join("")}
      ${n(r.levain.starterGrams)?`<tr><td>Mature starter (${n(r.levain.starterHydration)}%)</td><td class="r num">${fg(n(r.levain.starterGrams),f)} g</td></tr>`:""}
      <tr class="totalrow"><td>Levain total</td><td class="r num">${fg(c.levainTotal,f)} g</td></tr>
    </tbody></table>` : "";

  const soakDetail = (r.soakers||[]).filter(s => (s.rows||[]).some(x=>n(x.grams))).map(s => `
    <h2>${esc(s.name)||"Soaker"}</h2>
    <table class="formula"><tbody>
      ${(s.rows||[]).filter(x=>n(x.grams)).map(x=>`<tr><td>${esc(x.name)}</td><td class="r num">${fg(n(x.grams),f)} g</td></tr>`).join("")}
      <tr class="totalrow"><td>Total</td><td class="r num">${fg((s.rows||[]).reduce((t,x)=>t+n(x.grams),0),f)} g</td></tr>
    </tbody></table>`).join("");

  const doughScaled = c.dough * f;
  let yieldStat = "";
  const ylg = n(r.yieldLoafG), yct = n(r.yieldCount);
  if (doughScaled && ylg > 0){
    yieldStat = `<div><div class="v num">${(Math.round(doughScaled/ylg*10)/10).toLocaleString()} × ${Math.round(ylg).toLocaleString()} g</div><div class="l">Loaves × weight</div></div>`;
  } else if (doughScaled && yct > 0){
    yieldStat = `<div><div class="v num">${Math.round(yct).toLocaleString()} × ${Math.round(doughScaled/yct).toLocaleString()} g</div><div class="l">Loaves × weight</div></div>`;
  }

  app.innerHTML = `
    <header class="top no-print">
      <button class="backlink" data-action="backrecipe">← Back to editing</button>
      <button class="btn small" data-action="print">Print</button>
    </header>
    <div class="sheet">
      <h1>${esc(r.name) || "Untitled formula"}</h1>
      <div class="meta">${esc(r.category)}${r.category?" · ":""}${r.yieldLoafG && r.yieldCount ? `${r.yieldLoafG} g × ${r.yieldCount}` : ""}${ui.factor!==1?` · scaled ×${Math.round(ui.factor*1000)/1000}`:""} · ${today}</div>
      <div class="sheetstats">
        <div><div class="v blue num">${fp(c.hyd)}%</div><div class="l">True hydration</div></div>
        <div><div class="v bronze num">${fp(c.pff)}%</div><div class="l">Pre-fermented flour</div></div>
        <div><div class="v num">${fg(c.flour,f)} g</div><div class="l">Total flour</div></div>
        <div><div class="v num">${fg(c.dough,f)} g</div><div class="l">Total dough</div></div>
        ${yieldStat}
      </div>
      <h2>Final mix</h2>
      ${finalMixTableHTML(r, c)}
      <h2>Overall formula</h2>
      ${overallTableHTML(c)}
      ${levDetail}
      ${soakDetail}
      ${procRows ? `<h2>Process</h2>${procRows}` : ""}
      ${(r.notes||"").trim() ? `<h2>Notes</h2><div style="font-size:13.5px;white-space:pre-wrap">${esc(r.notes)}</div>` : ""}
    </div>`;
}

/* =============== levain builder =============== */
function computeLB(lb){
  const target = n(lb.target), surplus = n(lb.surplus), h = n(lb.hydration);
  const S0in = n(lb.starterGrams), h0 = n(lb.starterHydration);
  const inoc = n(lb.inoculation);
  const N = Math.min(6, Math.max(1, Math.round(n(lb.builds)) || 1));
  const W = target + surplus;
  const out = { ok: false, warnings: [], builds: [], W, N };
  if (!W || !h){
    out.warnings.push("Enter a target amount and hydration to see the schedule.");
    return out;
  }
  let S0, k;
  if (inoc > 0){
    k = 1 + (1 + h/100) / (inoc/100);
    S0 = W / Math.pow(k, N);
    out.solvedStarter = S0;
  } else {
    S0 = S0in;
    if (!S0){
      out.warnings.push("Enter a starting starter amount — or set a target inoculation % and the starter amount will be solved for you.");
      return out;
    }
    if (W <= S0){
      out.warnings.push("Target is smaller than your starting starter — nothing to build.");
      return out;
    }
    k = Math.pow(W / S0, 1 / N);
  }
  out.k = k;
  out.inocNominal = (1 + h/100) / (k - 1) * 100;
  if (k > 12) out.warnings.push("Each build grows ×" + fp(k) + " — a big jump per feed. Consider more builds or more starting starter.");
  else if (k < 1.4) out.warnings.push("Feeds are small relative to the seed — this levain will move fast. Consider fewer builds or less starting starter.");

  let flours = (lb.flours || []).filter(x => (x.name||"").trim() && n(x.pct) > 0);
  const psum = flours.reduce((s,x) => s + n(x.pct), 0);
  if (!flours.length) flours = [{ name: "Flour", pct: 100 }];
  const norm = flours.map(x => ({ name: x.name, frac: n(x.pct) / (psum || 100) }));
  if (psum && Math.abs(psum - 100) > 0.01)
    out.warnings.push("Flour ratios sum to " + fp(psum) + "% — they've been normalized to 100%.");

  let F = S0 / (1 + h0/100), Wt = S0 - F, M = S0;
  for (let i = 1; i <= N; i++){
    const Mi = (i === N) ? W : S0 * Math.pow(k, i);
    const Ftar = Mi / (1 + h/100), Wtar = Mi - Ftar;
    let fF = Ftar - F, fW = Wtar - Wt;
    if (fF < -0.5 || fW < -0.5){
      out.warnings.push("Build " + i + " would need negative flour or water — your starter hydration (" + h0 + "%) is too far from the target for this build size.");
    }
    fF = Math.max(0, fF); fW = Math.max(0, fW);
    const split = norm.map(x => ({ name: x.name, g: Math.round(fF * x.frac) }));
    const diff = Math.round(fF) - split.reduce((s,x) => s + x.g, 0);
    if (split.length) split[0].g += diff;
    out.builds.push({
      i,
      carry: Math.round(M),
      split,
      water: Math.round(fW),
      total: Math.round(Mi),
      rf: M ? fF / M : 0,
      rw: M ? fW / M : 0,
      inoc: fF > 0 ? (M / fF) * 100 : 0
    });
    F = Ftar; Wt = Wtar; M = Mi;
  }
  out.ok = true;
  return out;
}

function currentLevain(){ return db.levains.find(x => x.id === ui.levainId) || null; }

function lbResultsHTML(lv){
  const res = computeLB(lv);
  let html = res.warnings.map(w => `<div class="banner">${esc(w)}</div>`).join("");
  if (!res.ok) return html;
  if (res.solvedStarter != null){
    const sg = Math.round(res.solvedStarter * 10) / 10;
    html += `<div class="banner">Target inoculation <b>${fp(n(lv.inoculation))}%</b> → begin with <b>${sg.toLocaleString()} g</b> mature starter. While this is set, the starter-amount field is ignored.</div>`;
  }
  const blocks = res.builds.map(b => {
    const frac = res.N > 1 ? (b.i - 1) / (res.N - 1) : 1;
    const bg = (0.06 + 0.30 * frac).toFixed(3);
    const bd = (0.30 + 0.70 * frac).toFixed(3);
    return `
    <div class="buildblock" style="background:rgba(214,150,30,${bg});border-left-color:rgba(163,108,15,${bd})">
      <div class="eyebrow" style="margin-bottom:5px">Build ${b.i} &nbsp;·&nbsp; inoc ${fp(b.inoc)}% &nbsp;·&nbsp; seed 1 : ${fp(b.rf)} flour : ${fp(b.rw)} water</div>
      <table class="formula"><tbody>
        <tr><td>${b.i === 1 ? "Mature starter" : "All of build " + (b.i - 1)}</td><td class="r num">${b.carry.toLocaleString()} g</td></tr>
        ${b.split.map(s => `<tr><td>${esc(s.name)}</td><td class="r num">${s.g.toLocaleString()} g</td></tr>`).join("")}
        <tr><td>Water</td><td class="r num">${b.water.toLocaleString()} g</td></tr>
        <tr class="totalrow"><td>After build ${b.i}</td><td class="r num">${b.total.toLocaleString()} g</td></tr>
      </tbody></table>
    </div>`;
  }).join("");
  html += `<section class="card">
    <h2>Build schedule <span class="hint">grows ×${fp(res.k)} each build</span></h2>
    ${blocks}
    <div class="tagline"><b>${fg(n(lv.target),1)} g</b> goes to the dough · <b>${fg(n(lv.surplus),1)} g</b> stays back as your starter.</div>
  </section>`;
  return html;
}

function refreshLB(){
  const zone = document.getElementById("lbResults");
  const lv = currentLevain();
  if (zone && lv) zone.innerHTML = lbResultsHTML(lv);
}

function renderLB(){
  const lb = currentLevain();
  if (!lb){ ui.view = "lblib"; return renderLBLib(); }
  const flourRows = lb.flours.map(x => `
    <div class="ingrow" style="grid-template-columns:minmax(0,1fr) 84px 34px">
      <input type="text" placeholder="Flour" value="${attr(x.name)}" data-sec="lbflour" data-row="${attr(x.id)}" data-field="name">
      <input type="text" class="g num" inputmode="decimal" placeholder="%" value="${x.pct ?? ""}" data-sec="lbflour" data-row="${attr(x.id)}" data-field="pct" aria-label="percent of flour">
      <button class="xbtn" data-action="lbdelflour" data-row="${attr(x.id)}" aria-label="Remove flour">✕</button>
    </div>`).join("");
  app.innerHTML = `
    <header class="top no-print">
      <div>
        <button class="backlink" data-action="openlb">← Levains</button>
        <h1>${esc(lb.name) || "Untitled levain"}</h1>
        <div class="sub">Work backward from the levain your dough needs</div>
      </div>
      <button class="btn ghost small" data-action="lbsheet">Formula sheet</button>
    </header>
    ${storageBanner()}
    <section class="card no-print">
      <h2>Targets</h2>
      <div class="fieldgrid">
        <div class="full"><label class="f">Name</label>
          <input type="text" value="${attr(lb.name)}" data-sec="lb" data-field="name" placeholder="e.g. Rye levain — Saturday bake"></div>
        <div><label class="f">Levain needed for the dough (g)</label>
          <input type="text" inputmode="decimal" class="num" value="${lb.target ?? ""}" data-sec="lb" data-field="target" placeholder="3520"></div>
        <div><label class="f">Surplus to keep back (g)</label>
          <input type="text" inputmode="decimal" class="num" value="${lb.surplus ?? ""}" data-sec="lb" data-field="surplus" placeholder="100"></div>
        <div><label class="f">Levain hydration (%)</label>
          <input type="text" inputmode="decimal" class="num" value="${lb.hydration ?? ""}" data-sec="lb" data-field="hydration" placeholder="100"></div>
        <div><label class="f">Number of builds (1–6)</label>
          <input type="text" inputmode="numeric" class="num" value="${lb.builds ?? ""}" data-sec="lb" data-field="builds" placeholder="2"></div>
        <div><label class="f">Starting mature starter (g)</label>
          <input type="text" inputmode="decimal" class="num" value="${lb.starterGrams ?? ""}" data-sec="lb" data-field="starterGrams" placeholder="50"></div>
        <div><label class="f">Starter hydration (%)</label>
          <input type="text" inputmode="decimal" class="num" value="${lb.starterHydration ?? ""}" data-sec="lb" data-field="starterHydration" placeholder="100"></div>
        <div class="full"><label class="f">Target inoculation % — optional, solves the starter amount for you</label>
          <input type="text" inputmode="decimal" class="num" value="${lb.inoculation ?? ""}" data-sec="lb" data-field="inoculation" placeholder="e.g. 25"></div>
      </div>
      <div class="tagline">Inoculation = mature seed as a % of each feed's flour. Lower % = slower, longer builds; higher % = faster.</div>
    </section>
    <section class="card no-print">
      <h2>Flour mix <span class="hint">% of each feed's flour</span></h2>
      ${flourRows}
      <button class="btn ghost small addrow" data-action="lbaddflour">+ Flour</button>
    </section>
    <div id="lbResults">${lbResultsHTML(lb)}</div>
    <section class="card no-print">
      <h2>Manage</h2>
      <div class="btnrow">
        <button class="btn quiet small" data-action="duplevain">Duplicate</button>
        <button class="btn danger small" data-action="dellevain">Delete levain</button>
      </div>
    </section>`;
}

function renderLBLib(){
  const cards = db.levains.map(lv => {
    const res = computeLB(lv);
    const total = n(lv.target) + n(lv.surplus);
    return `<button class="reccard" data-action="openlevain" data-id="${attr(lv.id)}">
      <h3>${esc(lv.name) || "Untitled levain"}</h3>
      <div class="chips">
        <span class="chip hyd num">${fp(n(lv.hydration))}% hyd</span>
        <span class="chip num">${fg(total,1)} g</span>
        <span class="chip num">${res.N} build${res.N === 1 ? "" : "s"}</span>
        ${res.ok ? `<span class="chip pff num">×${fp(res.k)} / build</span>` : ""}
      </div>
    </button>`;
  }).join("");
  app.innerHTML = `
    <header class="top">
      <div>
        <button class="backlink" data-action="back">← Library</button>
        <h1>Levain Builder</h1>
        <div class="sub">Build schedules for each of your starters</div>
      </div>
    </header>
    ${storageBanner()}
    <div class="libgrid">
      ${cards || `<div class="empty">No levains yet. Start one below.</div>`}
    </div>
    <div class="footerbar no-print">
      <button class="btn" data-action="newlevain">+ New levain</button>
    </div>`;
}

function renderLBSheet(){
  const lv = currentLevain();
  if (!lv){ ui.view = "lblib"; return renderLBLib(); }
  const res = computeLB(lv);
  const today = new Date().toLocaleDateString();
  const total = n(lv.target) + n(lv.surplus);
  const buildTables = res.ok ? res.builds.map(b => `
    <h2>Build ${b.i} <span style="font-family:var(--mono);font-weight:400;letter-spacing:0;text-transform:none;font-size:11.5px;color:var(--dim)">&nbsp;inoc ${fp(b.inoc)}% · seed 1 : ${fp(b.rf)} flour : ${fp(b.rw)} water</span></h2>
    <table class="formula"><tbody>
      <tr><td>${b.i === 1 ? "Mature starter" : "All of build " + (b.i - 1)}</td><td class="r num">${b.carry.toLocaleString()} g</td></tr>
      ${b.split.map(s => `<tr><td>${esc(s.name)}</td><td class="r num">${s.g.toLocaleString()} g</td></tr>`).join("")}
      <tr><td>Water</td><td class="r num">${b.water.toLocaleString()} g</td></tr>
      <tr class="totalrow"><td>After build ${b.i}</td><td class="r num">${b.total.toLocaleString()} g</td></tr>
    </tbody></table>`).join("")
    : res.warnings.map(w => `<div class="banner">${esc(w)}</div>`).join("");
  app.innerHTML = `
    <header class="top no-print">
      <button class="backlink" data-action="backlbedit">← Back to editing</button>
      <button class="btn small" data-action="print">Print</button>
    </header>
    <div class="sheet">
      <h1>${esc(lv.name) || "Untitled levain"}</h1>
      <div class="meta">Starter: ${fg(res.solvedStarter != null ? res.solvedStarter : n(lv.starterGrams),1)} g @ ${fp(n(lv.starterHydration))}% · ${today}</div>
      <div class="sheetstats">
        <div><div class="v num">${fg(total,1)} g</div><div class="l">Total levain</div></div>
        <div><div class="v blue num">${fp(n(lv.hydration))}%</div><div class="l">Hydration</div></div>
        ${res.ok ? `<div><div class="v bronze num">${fp(res.inocNominal)}%</div><div class="l">Inoculation</div></div>` : ""}
        <div><div class="v num">${res.N}</div><div class="l">Builds</div></div>
        ${res.ok ? `<div><div class="v num">×${fp(res.k)}</div><div class="l">Growth / build</div></div>` : ""}
      </div>
      ${buildTables}
      ${res.ok ? `<h2>Yield</h2>
      <div class="procline"><b>To the dough</b><span class="num">${fg(n(lv.target),1)} g</span></div>
      <div class="procline"><b>Surplus kept</b><span class="num">${fg(n(lv.surplus),1)} g</span></div>` : ""}
    </div>`;
}

/* =============== updates =============== */
function findRow(r, sec, soakerId, rowId){
  if (sec === "dough") return (r.ingredients||[]).find(x => x.id === rowId);
  if (sec === "levain") return ((r.levain&&r.levain.rows)||[]).find(x => x.id === rowId);
  if (sec === "soaker"){
    const s = (r.soakers||[]).find(s => s.id === soakerId);
    return s ? (s.rows||[]).find(x => x.id === rowId) : null;
  }
  return null;
}

function refreshComputed(){
  const zone = document.getElementById("computedZone");
  const r = currentRecipe();
  if (zone && r) zone.innerHTML = computedZoneHTML(r);
  refreshYieldReadout();
}

app.addEventListener("input", e => {
  const t = e.target;
  const sec = t.dataset.sec;
  if (!sec) return;

  if (sec === "lb"){
    const lv = currentLevain(); if (!lv) return;
    const fld = t.dataset.field;
    if (fld === "name") lv.name = t.value;
    else lv[fld] = t.value === "" ? null : parseFloat(t.value);
    save(); refreshLB(); return;
  }
  if (sec === "lbflour"){
    const lv = currentLevain(); if (!lv) return;
    const row = lv.flours.find(x => x.id === t.dataset.row);
    if (row){
      if (t.dataset.field === "pct") row.pct = t.value === "" ? null : parseFloat(t.value);
      else row.name = t.value;
    }
    save(); refreshLB(); return;
  }

  const r = currentRecipe();
  if (!r) return;

  if (sec === "meta"){
    const fld = t.dataset.field;
    if (fld === "yieldLoafG" || fld === "yieldCount"){
      r[fld] = t.value === "" ? null : parseFloat(t.value) || null;
      save(); refreshYieldReadout();
      const sc = document.getElementById(fld === "yieldLoafG" ? "scLoaf" : "scCount");
      if (sc) sc.value = t.value;
      return;
    }
    r[fld] = t.value;
    save(); return;
  }
  if (sec === "scalecalc"){
    const v = t.value === "" ? null : parseFloat(t.value) || null;
    if (t.id === "scLoaf") r.yieldLoafG = v; else r.yieldCount = v;
    save(); refreshYieldReadout();
    return;
  }
  if (sec === "proc"){
    const fld = t.dataset.field;
    if (fld === "notes_free") r.notes = t.value;
    else r.process[fld] = t.value;
    save(); return;
  }
  if (sec === "levmeta"){
    r.levain[t.dataset.field] = t.value === "" ? null : parseFloat(t.value);
    save(); refreshComputed(); return;
  }
  if (sec === "soakername"){
    const s = (r.soakers||[]).find(s => s.id === t.dataset.soaker);
    if (s) s.name = t.value;
    save(); refreshComputed(); return;
  }
  const row = findRow(r, sec, t.dataset.soaker, t.dataset.row);
  if (!row) return;
  const fld = t.dataset.field;
  if (fld === "grams") row.grams = t.value === "" ? null : parseFloat(t.value);
  else row[fld] = t.value;
  save(); refreshComputed();
});

app.addEventListener("change", e => {
  const t = e.target;
  if (t.tagName === "SELECT" && t.dataset.sec){
    const r = currentRecipe(); if (!r) return;
    const row = findRow(r, t.dataset.sec, t.dataset.soaker, t.dataset.row);
    if (row){ row.type = t.value; save(); refreshComputed(); }
  }
});

app.addEventListener("click", e => {
  const btn = e.target.closest("[data-action]");
  if (!btn) return;
  const act = btn.dataset.action;
  const r = currentRecipe();

  if (act === "open"){ ui.recipeId = btn.dataset.id; ui.view = "recipe"; ui.factor = 1; render(); }
  else if (act === "new"){
    const nr = blankRecipe();
    db.recipes.unshift(nr); save();
    ui.recipeId = nr.id; ui.view = "recipe"; ui.factor = 1; render();
  }
  else if (act === "back"){ ui.view = "library"; ui.factor = 1; render(); }
  else if (act === "backrecipe"){ ui.view = "recipe"; render(); }
  else if (act === "sheet"){ ui.view = "sheet"; render(); }
  else if (act === "print"){ window.print(); }
  else if (act === "export"){
    const blob = new Blob([JSON.stringify(db, null, 2)], { type: "application/json" });
    const a = document.createElement("a");
    a.href = URL.createObjectURL(blob);
    a.download = "formula-book-backup.json";
    a.click();
    setTimeout(()=>URL.revokeObjectURL(a.href), 2000);
  }
  else if (act === "import"){ document.getElementById("importFile").click(); }
  else if (act === "openlb"){ ui.view = "lblib"; render(); }
  else if (act === "openlevain"){ ui.levainId = btn.dataset.id; ui.view = "lb"; render(); }
  else if (act === "newlevain"){
    const lv = defaultLevain();
    db.levains.unshift(lv); save();
    ui.levainId = lv.id; ui.view = "lb"; render();
  }
  else if (act === "lbsheet"){ ui.view = "lbsheet"; render(); }
  else if (act === "backlbedit"){ ui.view = "lb"; render(); }
  else if (act === "duplevain"){
    const lv = currentLevain(); if (!lv) return;
    const copy = JSON.parse(JSON.stringify(lv));
    copy.id = uid();
    copy.name = (copy.name || "Untitled") + " (copy)";
    copy.flours.forEach(x => x.id = uid());
    db.levains.unshift(copy); save();
    ui.levainId = copy.id; render();
  }
  else if (act === "dellevain"){
    const lv = currentLevain(); if (!lv) return;
    if (confirm("Delete this levain? This can't be undone.")){
      db.levains = db.levains.filter(x => x.id !== lv.id);
      save(); ui.view = "lblib"; ui.levainId = null; render();
    }
  }
  else if (act === "lbaddflour"){
    const lv = currentLevain(); if (!lv) return;
    lv.flours.push({ id: uid(), name: "", pct: null });
    save(); rerenderInPlace();
  }
  else if (act === "lbdelflour"){
    const lv = currentLevain(); if (!lv) return;
    lv.flours = lv.flours.filter(x => x.id !== btn.dataset.row);
    save(); rerenderInPlace();
  }
  else if (!r) { return; }
  else if (act === "addrow"){
    const sec = btn.dataset.sec;
    const nrow = { id: uid(), name: "", grams: null, type: sec === "levain" ? "flour" : "other" };
    if (sec === "dough") r.ingredients.push(nrow);
    else if (sec === "levain") r.levain.rows.push(nrow);
    else if (sec === "soaker"){
      const s = r.soakers.find(s => s.id === btn.dataset.soaker);
      if (s) s.rows.push(nrow);
    }
    save(); rerenderInPlace();
  }
  else if (act === "delrow"){
    const sec = btn.dataset.sec, rid = btn.dataset.row;
    if (sec === "dough") r.ingredients = r.ingredients.filter(x => x.id !== rid);
    else if (sec === "levain") r.levain.rows = r.levain.rows.filter(x => x.id !== rid);
    else if (sec === "soaker"){
      const s = r.soakers.find(s => s.id === btn.dataset.soaker);
      if (s) s.rows = s.rows.filter(x => x.id !== rid);
    }
    save(); rerenderInPlace();
  }
  else if (act === "togglelevain"){
    r.levain.enabled = !r.levain.enabled;
    if (r.levain.enabled && !r.levain.rows.length){
      r.levain.rows = [
        { id: uid(), name: "Bread flour", grams: null, type: "flour" },
        { id: uid(), name: "Water", grams: null, type: "liquid" }
      ];
      if (r.levain.starterHydration == null) r.levain.starterHydration = 100;
    }
    save(); rerenderInPlace();
  }
  else if (act === "addsoaker"){
    r.soakers.push({ id: uid(), name: "", rows: [
      { id: uid(), name: "", grams: null, type: "other" },
      { id: uid(), name: "Water", grams: null, type: "liquid" }
    ]});
    save(); rerenderInPlace();
  }
  else if (act === "delsoaker"){
    if (confirm("Remove this soaker?")){
      r.soakers = r.soakers.filter(s => s.id !== btn.dataset.soaker);
      save(); rerenderInPlace();
    }
  }
  else if (act === "scaleyield"){
    const lg = parseFloat(document.getElementById("scLoaf").value);
    const ct = parseFloat(document.getElementById("scCount").value);
    const c = compute(r);
    if (lg > 0 && ct > 0 && c.dough > 0){
      ui.factor = (lg * ct) / c.dough;
      r.yieldLoafG = lg; r.yieldCount = ct; save();
      rerenderInPlace();
    }
  }
  else if (act === "scaleflour"){
    const tf = parseFloat(document.getElementById("scFlour").value);
    const c = compute(r);
    if (tf > 0 && c.flour > 0){ ui.factor = tf / c.flour; rerenderInPlace(); }
  }
  else if (act === "resetscale"){ ui.factor = 1; rerenderInPlace(); }
  else if (act === "bakein"){
    const f = ui.factor;
    const scaleRow = x => { if (x.grams != null) x.grams = Math.round(n(x.grams) * f); };
    (r.ingredients||[]).forEach(scaleRow);
    if (r.levain){
      (r.levain.rows||[]).forEach(scaleRow);
      if (r.levain.starterGrams != null) r.levain.starterGrams = Math.round(n(r.levain.starterGrams) * f);
    }
    (r.soakers||[]).forEach(s => (s.rows||[]).forEach(scaleRow));
    ui.factor = 1; save(); rerenderInPlace();
  }
  else if (act === "duplicate"){
    const copy = JSON.parse(JSON.stringify(r));
    copy.id = uid();
    copy.name = (copy.name || "Untitled") + " (copy)";
    copy.ingredients.forEach(x => x.id = uid());
    if (copy.levain) copy.levain.rows.forEach(x => x.id = uid());
    copy.soakers.forEach(s => { s.id = uid(); s.rows.forEach(x => x.id = uid()); });
    db.recipes.unshift(copy); save();
    ui.recipeId = copy.id; render();
  }
  else if (act === "delete"){
    if (confirm("Delete this formula? This can't be undone.")){
      db.recipes = db.recipes.filter(x => x.id !== r.id);
      save();
      ui.view = "library"; ui.recipeId = null; ui.factor = 1; render();
    }
  }
});

document.getElementById("importFile").addEventListener("change", e => {
  const file = e.target.files[0];
  if (!file) return;
  const reader = new FileReader();
  reader.onload = () => {
    try {
      const data = JSON.parse(reader.result);
      if (!data || !Array.isArray(data.recipes)) throw new Error("bad format");
      let added = 0, updated = 0;
      data.recipes.forEach(inc => {
        const i = db.recipes.findIndex(x => x.id === inc.id);
        if (i >= 0){ db.recipes[i] = inc; updated++; }
        else { db.recipes.push(inc); added++; }
      });
      save(); render();
      alert(`Import complete — ${added} added, ${updated} updated.`);
    } catch(err){
      alert("Couldn't read that file. It should be a JSON export from this tool.");
    }
  };
  reader.readAsText(file);
  e.target.value = "";
});

render();
</script>
</body>
</html>
